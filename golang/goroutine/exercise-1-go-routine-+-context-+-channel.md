# Exercise 1 : Go Routine + Context + Channel

## Soal

Cari nama Wina di slice bernama usernames menggunakan go routine, channel dan context wait timeout.

## Contoh Jawaban

```go
package main

import (
	"context"
	"fmt"
	"strings"
	"time"
)

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

var duration = 100 * time.Millisecond
var numberOfWorkers = 5
var start = time.Now()

func main() {
	ctx, cancel := context.WithTimeout(context.Background(), duration)
	defer cancel()

	checkNameWithChannel(ctx)
}

func checkNameWithChannel(ctx context.Context) {
	numOfBuffer := 5
	var ch = make(chan string, numOfBuffer)

	go func() {
		fmt.Println("start send data to channel")
		for _, username := range usernames {
			ch <- username
		}
		fmt.Println("end send data to channel")
		close(ch)
	}()

	var total int
	fmt.Println("start receive data from channel")
	for i := range ch {
		select {
		case <-ctx.Done():
			break
		default:
			if strings.Contains(strings.ToLower(i), "wina") {
				total++
			}
		}
	}
	fmt.Println("end receive data from channel")

	fmt.Println("found", total, "of Wina. Done in", time.Since(start).Seconds(), "seconds")
}

```

```
start receive data from channel
start send data to channel
end send data to channel
end receive data from channel
found 1 of Wina. Done in 0 seconds
```
