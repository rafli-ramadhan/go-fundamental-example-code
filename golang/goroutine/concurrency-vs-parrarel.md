# Concurrency vs Parrarel

**Go routine** -> mini thread ringan yang dikelola oleh go runtime & implementasi golang pada concurrency -> untuk menjalakan concurrency (secara bergantian) di golang -> sifatnya asynchronous (tidak berurutan) -> tidak saling tunggu -> dan secara random.

**Thread** -> sebuah segmen dari process.

**Process** -> sebuah eksekusi dari program

Go routine dijalankan oleh Go Scheduler dalam thread -> jumlah thread nya sebanyak GOMAXPROCS (biasanya sejumlah core CPU).

**Kelebihan** -> Go routine sangat ringan -> ukurannya hanya 2 kB.

**Concurrency** -> eksekusi fungsi yang dijalankan secara pararel, namun saat ada fungsi yang selesai terlebih dahulu, akan membantu mengerjakan fungsi lain.

**Parallel programming** -> eksekusi fungsi yang dijalankan bersamaan, berakhirnya bisa berbeda-beda.

<figure><img src="https://www.baeldung.com/wp-content/uploads/sites/4/2022/01/vs-1024x462-1.png" alt=""><figcaption><p><a href="https://www.baeldung.com/wp-content/uploads/sites/4/2022/01/vs-1024x462-1.png">https://www.baeldung.com/wp-content/uploads/sites/4/2022/01/vs-1024x462-1.png</a></p></figcaption></figure>

<figure><img src="https://miro.medium.com/max/1200/1*V5syja2casc0gCuu9zKV5g.png" alt=""><figcaption><p><a href="https://miro.medium.com/max/1200/1*V5syja2casc0gCuu9zKV5g.png">https://miro.medium.com/max/1200/1*V5syja2casc0gCuu9zKV5g.png</a></p></figcaption></figure>

```go
package main

import (  
    "fmt"
    "time"
)

func text(num int, message string) {
    for i := 0; i < num; i++ {
        fmt.Printf("%s ", message)
    }
}

func main() {
    textSlice := []string{"test 1", "test 2", "test 3", "test 4", "test 5", "test 6", "test 7", "test 8", "test 9", "test 10"}
    for _, val := range textSlice {
        go text(5, val)
    }
    time.Sleep(3000*time.Millisecond)
    fmt.Println("end")
}
```

```
a 1 2 3 4 5 1 2 3 4 5 a b c d e 1 2 3 4 5 1 2 3 4 5 a b c d e a b c d e 1 2 3 4 5 a b c d e 1 2 3 4 5 a b c d e a b c d e a b c d e 1 2 3 4 5 1 2 3 4 5 a b c d e 1 2 3 4 5 b c d e a 
b c d e a b c d e 1 2 3 4 5 1 2 3 4 5 end
```
