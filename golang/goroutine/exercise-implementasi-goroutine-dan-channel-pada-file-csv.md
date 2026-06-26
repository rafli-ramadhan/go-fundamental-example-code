# Exercise : Implementasi Goroutine dan Channel pada File CSV

## Soal

Masukkan 1.000.000 data ke dalam 1 file csv menggunakan go routine dan channel.

## Contoh Jawaban

```go
package main

import (
	"encoding/csv"
	"fmt"
	"log"
	"math/rand"
	"os"
	"sync"
	"time"
)

var wg sync.WaitGroup
var m sync.Mutex

type userComment struct {
	name    string
	comment string
}

func main() {
	start := time.Now()
	totalWorker := 3
	userCommentChannel := make(chan userComment, 100)

	// generate data
	sliceName := []string{"Adli", "Bagus", "Rafli", "Lutfi"}
	go func() {
		for i := 1; i <= 1000000; i++ {
			userComment := userComment{
				name:    sliceName[rand.Intn(4)],
				comment: randomString(20),
			}
			userCommentChannel <- userComment
			if i == 1000000 {
				close(userCommentChannel)
			}
		}
	}()

	csvfile, err := os.Create("file/comment.csv")
	if err != nil {
		log.Panicln("Error create data :", err)
	}
	for i := 0; i < totalWorker; i++ {
		wg.Add(1)
		// index := i
		go func() {		
			csvwriter := csv.NewWriter(csvfile)
			for userComment := range userCommentChannel {
				var temp = []string{userComment.name, userComment.comment}
				m.Lock()
				if err := csvwriter.Write(temp); err != nil {
					log.Fatalln("Error writing data :", err)
				}
				m.Unlock()
				// fmt.Printf("worker-%d - %v\n", index+1, userComment)
			}
			defer csvwriter.Flush()
			wg.Done()
		}()
		wg.Wait()
	}

	defer func() {
		fmt.Println("Duration", time.Since(start).Seconds())
		if err := csvfile.Close(); err != nil {
			log.Panicln("Error closing file :", err)
		}
	}()

	log.Print("Start read")
	csvfile2, err := os.Open("file/comment.csv")
	if err != nil {
		log.Panicln("Error open data", err)
	}
	csvreader := csv.NewReader(csvfile2)
	ReadAllData(csvreader)
}

func randomString(length int) string {
	// randomizer := rand.New(rand.NewSource(time.Now().Unix()))
	letters := []rune("abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ")

	b := make([]rune, length)
	for i := range b {
		b[i] = letters[rand.Intn(len(letters))]
	}

	return string(b)
}

func ReadAllData(csvreader *csv.Reader) {
	if data, err := csvreader.ReadAll(); err != nil {
		log.Fatalln("Error cant read data from csv :", err)
	} else{
		for i:=0; i<100; i++ {
			fmt.Println("Name :", data[i][0])
			fmt.Println("Comment :", data[i][1])
			fmt.Println()
		}
	}
}

```
