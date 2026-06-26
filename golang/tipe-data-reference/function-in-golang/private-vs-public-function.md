# Private vs Public Function

Public function ditandai dengan huruf besar di awal nama function, sementara private dengan huruf kecil. Public function memungkinkan function tersebut untuk digunakan di package lain, sementara private function tidak bisa digunakan di package lain.

## Contoh _code_

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
	hitung1 := pythagoras(3, 4)
	hitung2 := pertambahan(2, 3)
	var penampungFunction func(int, int) float64 = pythagoras
	fmt.Println(hitung1)
	fmt.Println(hitung2)
	fmt.Println(penampungFunction(3,4))

}
```

```
5
5
5
```
