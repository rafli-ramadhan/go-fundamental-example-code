# Go Max Procs

Goroutine itu sebenarnya dijalankan di dalam Thread.

Untuk mengetahui berapa jumlah Thread, kita bisa menggunakan GOMAXPROCS -> bisa juga untuk mengubah jumlah thread atau mengambil jumlah thread -> Secara default, jumlah thread di Go-Lang itu sebanyak jumlah CPU di komputer kita.

```go
package main
 
import (
    "fmt"
    "runtime"
)

func main() {
    totalThread := runtime.GOMAXPROCS(-1)
    fmt.Println("Total Thread", totalThread)

    totalCpu := runtime.NumCPU()
    fmt.Println("CPU", totalCpu)

    totalGoroutine := runtime.NumGoroutine()
    fmt.Println("Num Goroutine", totalGoroutine)

    runtime.GOMAXPROCS(20)
    totalThread2 := runtime.GOMAXPROCS(-1)
    fmt.Println("Total Thread", totalThread2)

    totalCpu2 := runtime.NumCPU()
    fmt.Println("CPU", totalCpu2)

    totalGoroutine2 := runtime.NumGoroutine()
    fmt.Println("Num Goroutine", totalGoroutine2)
}
```

```
Total Thread 4
CPU 4
Num Goroutine 1
Total Thread 20
CPU 4
Num Goroutine 1
```
