# Variadic Function

Variadic memungkinkan fungsi dengan input parameter lebih dari 1 data (varargs) dengan tipe data yang sama. Namun hanya untuk input parameter terakhir dari sebuah function. Contohnya sebagai berikut :

```
func Example(a, b, c, ....d) {}
```

Keunggulannya variadic yaitu tidak perlu membuat slice terlebih dahulu untuk input lebih dari 1 data dengan tipe data yang sama, sehingga bisa langsung mengirim keseluruhan data yang dipisahkan dengan tanda koma.

## Contoh _code_

```go
package main

import (
	"fmt"
)

func main() {
	total := sumAll(10, 20, 30, 40, 50, 60, 70)
	fmt.Println(total)

	numbers := []int{10, 20, 30, 40, 50, 60, 70}
	fmt.Println(sumAll(numbers...))

	// numbers := [7]int{10, 20, 30, 40, 50, 60, 70} -> can not use array
	// fmt.Println(sumAll(numbers...))
}

// input harus berupa slice
func sumAll(numbers ...int) int {
	total := 0
	for _, value := range numbers {
		total += value
	}
	return total
}
```

```
280
280
```
