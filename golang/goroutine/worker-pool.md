# Worker Pool

Kapan pakai worker pool? Jika task banyak / bukan sequential / tidak pakai mutex.

Contoh kasus call 3 API lalu proses jadi 1 Json, maka worker pool tidak perlu. Kalau call 10 API lalu proses jadi 1 Json, maka worker pool perlu.

```go
package main

import (
	"fmt"
	"math/rand"
	"sync"
	"time"
)

type Job struct {
	ID      int
	Payload string
}

type Result struct {
	JobID  int
	Output string
	Error  error
}

type WorkerPool struct {
	numWorkers int
	jobs       chan Job
	results    chan Result
	wg         sync.WaitGroup
}

func NewWorkerPool(numWorkers, bufferSize int) *WorkerPool {
	return &WorkerPool{
		numWorkers: numWorkers,
		jobs:       make(chan Job, bufferSize),
		results:    make(chan Result, bufferSize),
	}
}

func (wp *WorkerPool) Start() {
	for i := 1; i <= wp.numWorkers; i++ {
		wp.wg.Add(1)
		workerID := i
		go wp.worker(workerID)
	}
	
	go func() {
		wp.wg.Wait()
		close(wp.results)
	}()
}

func (wp *WorkerPool) worker(id int) {
	defer wp.wg.Done()

	for job := range wp.jobs {
		fmt.Printf("  [Worker %d] mengerjakan Job #%d (%s)\n", id, job.ID, job.Payload)

		output, err := process(job)

		wp.results <- Result{
			JobID:  job.ID,
			Output: output,
			Error:  err,
		}
	}

	fmt.Printf("  [Worker %d] selesai, channel jobs ditutup\n", id)
}

func (wp *WorkerPool) Submit(job Job) {
	wp.jobs <- job
}

func (wp *WorkerPool) Close() {
	close(wp.jobs)
}

func (wp *WorkerPool) Results() <-chan Result {
	return wp.results
}

func process(job Job) (string, error) {
	duration := time.Duration(100+rand.Intn(200)) * time.Millisecond
	time.Sleep(duration)
	return fmt.Sprintf("hasil dari '%s' (took %v)", job.Payload, duration), nil
}

func main() {
	const (
		numWorkers = 3
		numJobs    = 10
		bufferSize = 5
	)

	fmt.Printf("=== Worker Pool: %d workers, %d jobs ===\n\n", numWorkers, numJobs)
	start := time.Now()
	pool := NewWorkerPool(numWorkers, bufferSize)
	pool.Start()

	go func() {
		for i := 1; i <= numJobs; i++ {
			pool.Submit(Job{
				ID:      i,
				Payload: fmt.Sprintf("task-%d", i),
			})
		}
		pool.Close()
	}()
	
	fmt.Println("Hasil:")
	successCount := 0
	for result := range pool.Results() {
		if result.Error != nil {
			fmt.Printf("❌ Job #%d error: %v\n", result.JobID, result.Error)
		} else {
			fmt.Printf("Job #%d → %s\n", result.JobID, result.Output)
			successCount++
		}
	}

	fmt.Printf("\nSelesai: %d/%d job sukses dalam %v\n", successCount, numJobs, time.Since(start))
}
```

