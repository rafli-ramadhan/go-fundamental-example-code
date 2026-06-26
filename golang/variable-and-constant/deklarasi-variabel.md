# Deklarasi Variabel

## **Var (Manifest Typing)**

Keunggulan deklarasi variabel dengan var adalah bisa di inisiasi di luar function dan bisa digunakan di level package. Kekurangannya tidak bisa untuk handle function yang return multi variabel. Contoh code manifest typing seperti code dibawah ini.

```go
package main

import (
	"fmt"
)

func main() {
	var res1, res2 int = calculate(2, 3)
	fmt.Println("Result", res1, res2)
}

func calculate(a, b int) (int, int) {
	return a + b, a * b
}
```

## Operator := (Type Interference)

Keunggulan deklarasi variabel dengan operator := adalah bisa untuk menampung value yang belum diketahui tipe datanya. Kekurangannya tidak bisa dideklarasikan di luar function.

## Contoh code manifest typing dan type interference

```go
package main

import "fmt"

var num1 int = 2
// num2 := 2 -> error non-declaration statement outside function body

func main() {
    num2 := 2
    fmt.Println(num1)
    fmt.Println(num2)
}
```

```
2
2
```
