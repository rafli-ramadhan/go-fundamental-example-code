---
coverY: 0
---

# Interface Kosong atau Any

Interface kosong dapat di inisiasi menggunakan `any` untuk Go version di atas 1.18. Untuk memperoleh nilai dari interface kosong dapat menggunakan _type assertion_ seperti contoh _code_ berikut.

## Contoh code interface kosong untuk menampung string, integer dan slice

```go
package main

import (
	"fmt"
)

func main() {
    var name any = "member_01"
    // type assertion
    stringName := name.(string)
    fmt.Println(stringName)

    var number1 any = 2
    var number2 any = 3
    // type assertion
    hasil := number1.(int64) + number2.(int64)
    fmt.Println(hasil)

    var user any = []string{"member_01", "member_02", "member_03"}
    // type assertion
    arrayUser := user.([]string)
    for _, v := range arrayUser {
        fmt.Println(v)
    }
}
```

```
member_01
5
member_01
member_02
member_03
```

## Contoh code interface kosong untuk menampung output function

```go
package main
import "fmt"

func main() {
	var test any = func(a, b int) int {
		return a+b
	} 
	// type assertion
	someFunc, ok := test.(func(a, b int) int)
	fmt.Println(ok)
	fmt.Println(someFunc(2,3))
}
```

```
true
5
```

## Contoh code interface kosong untuk menampung value dari channel

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	ch := make(chan int)
	go func() {
		var result interface{} =<- ch
		fmt.Println(result)
	}()
	ch<-1
	time.Sleep(1 * time.Second)
}
```

```
1
```

## Contoh code type assertion interface kosong jika berisi nil

Jika interface kosong bernilai nil, maka tidak bisa dilakukan type assertion untuk memperoleh nilai sesuai tipe data dalam interface kosong.

```go
package main

import (
	"fmt"
)

func main() {
	var errors any = fmt.Errorf("some error")
	res := errors.(error)
	fmt.Println(res)

	// this code will give an panic
	var errors2 any = nil
	res2 := errors2.(error)
	fmt.Println(res2)
}
```

```
panic: interface conversion: interface is nil, not error

goroutine 1 [running]:
main.main()
	/tmp/sandbox3945396184/prog.go:13 +0x99
Program exited.
```
