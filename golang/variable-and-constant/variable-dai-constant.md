# Variable daI Constant

Variabel dan constant di golang sama-sama dapat di inisiasi suatu value dengan tipe data tertentu. Perbedaannya nilai dari suatu constant tidak bisa diubah saat sudah di inisiasi suatu value.

## Contoh code

```go
package main

import "fmt"

func main() {
    var num1 int = 2
    fmt.Println(num1)

    // num1 di inisiasi dengan value berbeda
    num1 = 3
    fmt.Println(num1)
    
    var num2 = 2
    fmt.Println(num2)
    
    const num3 int = 2
    fmt.Println(num3)

    // num2 di inisiasi dengan velue berbeda akan memunculkan error :
    // cannot assign to num2 (constant 2 of type int)
}
```

```
2
3
2
2
```

## Contoh code deklarasi multi variabel dan constant

Contoh code untuk deklarasi multi variabel dan constant dapat dilihat di bawah ini.

```go
package main

import "fmt"

var (
	num1 = 1
	num2 = 2
	num3 = 3
)

func main() {
	var (
		num4 = 1
		num5 = 2
		num6 = 3
	)
	num7, num8, num9 := 1,2,3

    fmt.Println(num1)
    fmt.Println(num2)
    fmt.Println(num3)
    fmt.Println(num4)
    fmt.Println(num5)
    fmt.Println(num6)
    fmt.Println(num7)
    fmt.Println(num8)
    fmt.Println(num9)
}
```

```go
package main

import "fmt"

const (
	num1 = 1
	num2 = 2
	num3 = 3
)

func main() {
	const (
		num4 = 1
		num5 = 2
		num6 = 3
	)

    fmt.Println(num1)
    fmt.Println(num2)
    fmt.Println(num3)
    fmt.Println(num4)
    fmt.Println(num5)
    fmt.Println(num6)
}
```

```go
package main

import (
	"fmt"
)

var str1, str2, str3 string = "test1", "test2", "test3"

func main() {
	fmt.Println(str1)
	fmt.Println(str2)
	fmt.Println(str3)
}
```

## Format penamaan variabel di Golang

Penamaan variabel di golang tidak boleh diawali dengan simbol seperti @, #, angka serta syntax golang seperti for, type, string dan lainnya.

```go
package main

import (
	"fmt"
)

// not allowed
// var 1str string		 // syntax error*
// var @str string = "test"	 // invalid caracter
// var #str string = "test" 	 // invalid caracter
// var type string = "test"	 // syntax error*
// var for string = "test"	// syntax error*
// var some@str string = "test" // syntax error*
// var some#str string = "test" // syntax error*
// var some-string = "test"

// allowed but bad variable name
var int64 string = "test"

// allowed
var _str string = "test"
const _num = 1
var someString = "test"
var some_str = "test"
var SomeStr = "test"

func main() {
	fmt.Println(SomeStr)
}
```
