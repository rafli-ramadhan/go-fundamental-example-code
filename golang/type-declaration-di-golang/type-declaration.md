# Type Declaration

Type declaration digunakan untuk membuat tipe data baru menggunakan tipe data yang sudah ada (string, int, float, bool, array, slice, map, struct, interface atau function).

## Contoh code

```go
package main

import (
	"fmt"
)

func main() {
	type NoKTP string
	var KTPNumber NoKTP = "43284234928347293"
	fmt.Println(KTPNumber)

	type IsValid bool
	var isValid IsValid = true
	fmt.Println(isValid)

	type exp complex128
	var num exp = 2 + 5i
	fmt.Println(num)
}
```

```
43284234928347293
true
(2+5i)
```

## Type Alias dan Type Definition

Type alias digunakan untuk memberikan alias pada tipe data yang sudah ada, sementara type definition digunakan untuk membuat tipe data baru dari tipe data yang sudah ada. Contohnya seperti code dibawah ini.

```go
package main

import (
    "fmt"
)

// type alias or alias declaration
type str1 = string
// type definition
// bisa untuk menampung method
type str2 string

func main() {
    var username1 str1 = "member_01"
    var username2 str2 = "member_02"
    fmt.Printf("type of username1 is %T\n", username1)
    fmt.Printf("type of username2 is %T\n", username2)
	// passing variable
	var user1 string = username1
	var user2 string = username1
	fmt.Println(user1)
	fmt.Println(user2)
}
```

```
type of username1 is string
type of username2 is main.str2
```

Reference:

{% embed url="https://stackoverflow.com/questions/61247864/what-is-the-difference-between-type-alias-and-type-definition-in-go" %}
