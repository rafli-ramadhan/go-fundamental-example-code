# Input Function dari CLI

Untuk memperoleh input dari CLI (_Command Line Interface_) seperti dari CMD atau Bash di Golang dapat menggunakan fmt.Scanln.

## Contoh _code_

_Copy code_ dibawah ini, lalu jalankan di local dengan `go run main.go`.

```go
package main

import (
	"fmt"
	"math"
)

// private function
func pythagoras(a int, b int) float64 {
	return math.Sqrt(math.Pow(float64(a), 2) + math.Pow(float64(b), 2))
}

// private function
func pertambahan(a, b int) (hasil int) {
	hasil = a + b
	return
}

func main() {
    fmt.Println("Menghitung pythagoras dan penjumlahan 2 angka")

    var a int
    var b int

    fmt.Println("Masukkan input a")
    fmt.Scanln(&a)

    fmt.Println("Masukkan input b")
    fmt.Scanln(&b)

    fmt.Printf("Hasil dari perhitungan pythagoras adalah : %0.1f", pythagoras(a, b))
    fmt.Printf("\nHasil dari perjumlahan 2 angka di atas adalah : %d", pertambahan(a, b))
}
```
