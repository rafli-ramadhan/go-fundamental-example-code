# Assignment Operator

Assignment operator merupakan operasi untuk memberikkan nilai baru ke suatu variabel dengan tanda = atau dengan tanda +=, -=, \*=, /= and %= yang fungsi-nya mirip operator arithmetic.

## Contoh code assignment operator pada integer, float, complex dan string

Seluruh assignment operator dapat digunakan untuk integer. Untuk float tidak bisa menggunakan operator %=. Untuk complex juga tidak bisa menggunakan operator %=. Untuk string hanya bisa menggunakan operator =+ saja. Sementara untuk boolean tidak bisa digunakan semuanya.

```go
package main

import (
	"fmt"
)

func main() {
	var a int = 2
	a += 4
	fmt.Println(a)

	a -= 3
	fmt.Println(a)

	a *= 2
	fmt.Println(a)

	a /= 3
	fmt.Println(a)

	a %= 2
	fmt.Println(a)

	var b float64 = 2.2
	b += 5
	fmt.Println(b)

	b -= 4
	fmt.Println(b)

	b *= 3
	fmt.Println(b)

	b /= 2
	fmt.Println(b)

	// b %= 2.0 // -> invalid operation: operator % not defined for b (variable of type float64)

	var c string = "test1"
	c += "test2"
	fmt.Println(c)

	// c -= "test3" // -> invalid operation: operator - not defined for c (variable of type string)

	// c *= "test3" // -> invalid operation: operator * not defined for c (variable of type string)

	// c /= "test3" // -> invalid operation: operator / not defined for c (variable of type string)

	var d bool = true
	fmt.Println(d)
	// d += false // -> invalid operation: operator + not defined for d (variable of type bool)

	// d /= false // -> invalid operation: operator / not defined for d (variable of type bool)
}
```

```
6
3
6
2
0
7.2
3.2
9.600000000000001
4.800000000000001
test1test2
true

```
