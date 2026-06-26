# Arithmetic Operator

Arithmetic operator merupakan simbol operasi matematika yang bisa diterapkan di golang menggunakan tanda +, -, \*, /, %, ++ (+ 1) dan -- (- 1).

## Contoh code assignment operator pada integer, float, complex dan string

Seluruh arithmetic operator dapat digunakan untuk integer. Untuk float tidak bisa menggunakan operator %. Untuk complex juga tidak bisa menggunakan operator %. Untuk string hanya bisa menggunakan operator + saja.  Sementara untuk boolean tidak bisa digunakan semuanya.

```go
package main

import (
	"fmt"
)

func main() {
    // integer
    var num1, num2 int = 10, 12
	fmt.Println(num1 + num2*2/5%2)
	num1++
    fmt.Println(num1)
	num2--
    fmt.Println(num1)
    // float
    var f1, f2 float64 = 10.5, 10.5
	fmt.Println(f1 + f2*2/5)
	f1++
	fmt.Println(f1)
	f2--
	fmt.Println(f2)
    // complex
	var cmplx1, cmplx2 complex128 = 2 + 6i, 3 + 6i
	fmt.Println(cmplx1 + cmplx2*2/5)
	cmplx1++
	fmt.Println(cmplx1)
	cmplx2++
	fmt.Println(cmplx2)
    // string
    var str1, str2 = "10", "10"
	fmt.Println(str1 + str2)
}

```

```
10
11
11
14.7
(3.2+8.4i)
1010
PS D:\bootcamp-go\go-example> go run main.go
10
11
11
14.7
11.5
9.5
(3.2+8.4i)
(3+6i)
(4+6i)
1010
```
