# Exercise 3 : Random Worker (Go Routine + Channel + Context)

## Soal

Cari nama Wina di slice bernama usernames menggunakan worker (beberapa go routine) dan context wait timeout dengan catatan yang bekerja tidak harus worker ke-1 terlebih dahulu.

## Contoh Jawaban

```go
package main

import (
	"context"
	"fmt"
	"strings"
	"sync"
	"time"
)

var duration = 100*time.Millisecond
var wg = new(sync.WaitGroup)
var numberOfWorkers = 5
var start = time.Now()

func main() {
	ctx, cancel := context.WithTimeout(context.Background(), duration)
	defer cancel()
	
	checkNameWithChannelAndWorker(ctx)
}

func checkNameWithChannelAndWorker(ctx context.Context) {
	numOfBuffer := 5
	var channelUser = make(chan string, numOfBuffer)

	go func() {
		for i, username := range usernames {
			select{
				case <-ctx.Done():
					break
				default:
					channelUser <- username
			}
			if i == len(usernames) - 1 {
				close(channelUser)
			}
		}
		defer fmt.Println("end send data to channel")
	}()

	var channelUserFound = make(chan string, numOfBuffer)
	wg.Add(numberOfWorkers)
	for workerIndex := 0; workerIndex < numberOfWorkers; workerIndex++ {	
		var total int

		go func(workerIndex int) {
			for username := range channelUser {
				select {
				case <-ctx.Done():
					break
				default:
					if strings.Contains(strings.ToLower(username), "wina") {
						channelUserFound <- username
						total++
					}
				}
			}
						
			duration := time.Since(start)
			fmt.Println("worker -", workerIndex+1, "found", total, "of Wina. Done in", duration.Seconds(), "seconds")

			wg.Done()
		}(workerIndex)
	}

	wg.Wait()
}

var usernames []string = []string{
	"Aditya Ananta Putra",
	"ADNAN NUR JAILANI",
	"Afrila Zahra Prasetyo",
	"Aida Nirmala",
	"Amalia Rahma",
	"ANDINI DWI RIZKY PUTRI",
	"Angga Putra",
	"CAHAYA WIJAYA IJAM",
	"Dea Christina",
	"DEVITA NANDA OKTAVIA",
	"DEWI AYU LESTARI",
	"Dhevina Ananda Fitri",
	"DHEVY YANI RIZKI",
	"Dwi Mahani",
	"Eri Santosos",
	"Faiza Amalia Mahfudz",
	"FAUZIYATUNNISA",
	"Febriyanti Syabina",
	"Hafifah Nur Azmi Pratiwi",
	"Juliansyah Husien",
	"Kharisa Nur Aziza",
	"Lun Wina",
	"MAHREVA ROESTHA RAMADANIATY",
	"MUHAMMAD FADHILAH",
	"Muhammad Fatah Firdaus",
	"Muhammad Rafly Ahya",
	"Muhammad Rahmin Noor",
	"Muhammad Rivaldi",
	"Muhammad Rizky Rachmadhani",
	"Nadiah Nahdhah Islamiyah",
	"NOLA FEBRIANA SAPUTRI",
	"RAFADYAN REYHAN MARITZA WERAT",
	"Robby Satria",
	"Salshabilla Wahyu Anafi",
	"STEVI VIONI PAKULLA",
	"Winny Rahmah Nia",
}
```

```
D:\bootcamp-go\go-routine>go run main.go
end send data to channel
worker - 1 found 0 of Wina. Done in 0.0005516 seconds
worker - 2 found 0 of Wina. Done in 0.0005516 seconds
worker - 4 found 0 of Wina. Done in 0.0005516 seconds
worker - 3 found 1 of Wina. Done in 0.0005516 seconds
worker - 5 found 0 of Wina. Done in 0.0005516 seconds

D:\bootcamp-go\go-routine>go run main.go
end send data to channel
worker - 4 found 0 of Wina. Done in 0.0005427 seconds
worker - 2 found 0 of Wina. Done in 0.0005427 seconds
worker - 5 found 0 of Wina. Done in 0.0005427 seconds
worker - 1 found 1 of Wina. Done in 0.0005427 seconds
worker - 3 found 0 of Wina. Done in 0.0005427 seconds

D:\bootcamp-go\go-routine>go run main.go
end send data to channel
worker - 1 found 0 of Wina. Done in 0 seconds
worker - 4 found 1 of Wina. Done in 0 seconds
worker - 2 found 0 of Wina. Done in 0 seconds
worker - 3 found 0 of Wina. Done in 0 seconds
worker - 5 found 0 of Wina. Done in 0 seconds
```
