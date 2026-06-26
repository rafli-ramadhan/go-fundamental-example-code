# Operator Address (& dan \*)

Pada pointer, operator & digunakan untuk me-reference alamat memori dari suatu variabel ke variabel lain. Sementara operator \* digunakan menampilkan value dari variabel yang di reference.

## Contoh code pointer pada string

```go
package main

import (
    "fmt"
)

func main() {
    name1 := "member_1"
    name2 := &name1          // reference from memory address name
    fmt.Println(name1)
    fmt.Println(*name2)      // menampilkan variabel name1 yang me-reference variabel name harus dengan operator *
    fmt.Println(&name1)      // check memory address variabel name1
    fmt.Println(name2)       // check memory address variabel name2

    *name2 = "member_2"      // assign variabel name1 dengan nilai baru yang me-reference variabel name dengan tipe string
    fmt.Println(name1)
    fmt.Println(*name2)
    fmt.Println(&name1)      // check memory address
    fmt.Println(name2)       // check memory address
}
```

```
member_1
member_1
0xc00003e230
0xc00003e230
member_2
member_2
0xc00003e230
0xc00003e230
```

## Contoh code pointer pada struct

```go
package main

import "fmt"

func main() {
	type User struct {
		Name string
		Age  int
	}
	var userA = User{
		Name: "member_01",
		Age:  21,
	}
	var data = &userA
	*data = User{"member_02", 22}
	fmt.Println(userA)
}
```

```
{member_02 22}
```

## Contoh code pointer pada map

```go
package main

import "fmt"

func main() {
	var someMap = map[string]int{
		"test1": 1,
		"test2": 2,
	}
	var data = &someMap
	fmt.Println(*data)
	*data = map[string]int{
		"test": 2,
	}
	fmt.Println(someMap)
}	
```

```
map[test1:1 test2:2]
map[test:2]
```
