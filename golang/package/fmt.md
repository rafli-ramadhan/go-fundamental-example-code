---
description: Package "fmt"
---

# Fmt

Beberapa jenis fungsi di package Fmt diantaranya:

1. **fmt.Print** digunakan untuk menampilkan tipe data apapun di terminal.
2. **fmt.Println** digunakan untuk menampilkan tipe data apapun di terminal dengan akhiran new line.
3. **fmt.Printf** digunakan untuk menggabungkan beberapa tipe data apapun ke string utama dan menampilkannya di terminal.
4. **fmt.Sprint** digunakan untuk membuat variabel string dengan cara mirip dengan fmt.Print
5. **fmt.Sprintln** digunakan untuk membuat variabel string dengan cara mirip dengan fmt.Println, namun diakhiri dengan spasi dan new line.
6. **fmt.Sprintf** digunakan untuk membuat variabel string dengan cara mirip dengan fmt.Printf
7. **fmt.FPrintf** atau fmt.Fprintln digunakan untuk menampilkan tipe data apapun yang telah dikonversi menjadi slice byte ke sisi client (semisal web browser).
8. **fmt.Scanln** digunakan untuk memperoleh input dari terminal, tapi input tidak boleh dipisahkan oleh spasi.

## Contoh code penggunaan Print

```go
package main

import "fmt"

func main() {
	fmt.Print("Hello")
	fmt.Print("for integer        :", 123)
	fmt.Print("for scientific notation :", 3 + 5i)
	fmt.Print("for float          :", 1.234)
	fmt.Print("float rounding     :", 12.3456)
	fmt.Print("string example     :", "member 01")
	fmt.Print("boolean example    :", false)
	var someInterface interface{} = 123
	fmt.Print("for pointer    	:", &someInterface)
	fmt.Print("some interface     :", someInterface)
	fmt.Print("some array         :", [3]int{1,2,3})
	fmt.Print("some slice         :", []int{1,2,3})
	fmt.Print("some map           :", map[string]interface{}{
		"username": "member_01",
		"password": "Test123",
	})
	// struct
	type User struct {
		Username string
		Password string
	}
	user := User{"member_01", "Test123"}
	fmt.Print("some struct        :", user)
	// channel
	var ch = make(chan int)
	go func() {
		ch<-1
	}()
	fmt.Print("some channel       :", <-ch)
	// function
	someFunc := func (a, b int) int {
		return a + b
	}
	fmt.Print("some func          :", someFunc(2, 3))
}
```

```
Hellofor integer        :123for scientific notation :(3+5i)for float          :1.234float rounding     :12.3456string example     :member 01boolean example    :falsefor pointer  
        :0xc000040260some interface     :123some array         :[1 2 3]some slice         :[1 2 3]some map           :map[password:Test123 username:member_01]some struct        :{member_01 Test123}some channel       :1some func          :5
```

## Contoh code penggunaan Println

```go
package main

import "fmt"

func main() {					
	fmt.Println("Hello")
	fmt.Println("for integer        :", 123)
	fmt.Println("for scientific notation :", 3 + 5i)
	fmt.Println("for float          :", 1.234)
	fmt.Println("float rounding     :", 12.3456)
	fmt.Println("string example     :", "member 01")
	fmt.Println("boolean example    :", false)
	var someInterface interface{} = 123
	fmt.Println("for pointer    	:", &someInterface)
	fmt.Println("some interface     :", someInterface)
	fmt.Println("some array         :", [3]int{1,2,3})
	fmt.Println("some slice         :", []int{1,2,3})
	fmt.Println("some map           :", map[string]interface{}{
		"username": "member_01",
		"password": "Test123",
	})
	// struct
	type User struct {
		Username string
		Password string
	}
	user := User{"member_01", "Test123"}
	fmt.Println("some struct        :", user)
	// channel
	var ch = make(chan int)
	go func() {
		ch<-1
	}()
	fmt.Println("some channel       :", <-ch)
	// function
	someFunc := func (a, b int) int {
		return a + b
	}
	fmt.Println("some func          :", someFunc(2, 3))
}
```

```
Hello
for integer        : 123
for scientific notation : (3+5i)
for float          : 1.234
float rounding     : 12.3456
string example     : member 01
boolean example    : false
for pointer     : 0xc000040260
some interface     : 123
some array         : [1 2 3]
some slice         : [1 2 3]
some map           : map[password:Test123 username:member_01]
some struct        : {member_01 Test123}
some channel       :  1
some func          :  5
```

## Contoh code penggunaan Printf

```go
package main

import (
	"fmt"
)

func main() {
	fmt.Printf("for binary value   : %b \n", 10)
	fmt.Printf("for integer        : %d\n", 123)
	fmt.Printf("for scientific notation : %e \n", 3 + 5i)
	fmt.Printf("for float          : %f \n", 1.234)
	fmt.Printf("float rounding     : %.2f\n", 12.3456)
	fmt.Printf("string example     : %s\n", "member 01")
	var someInterface interface{} = 123
	fmt.Printf("type data of %s is : %T\n", "member_01", "member_01")
	fmt.Printf("type data of %d is : %T\n", someInterface, someInterface)
	fmt.Printf("for pointer    	   : %p\n", &someInterface)
	fmt.Printf("some interface     : %v\n", someInterface)
	fmt.Printf("some array         : %v\n", [3]int{1,2,3})
	fmt.Printf("some slice         : %v\n", []int{1,2,3})
	// struct
	type User struct {
		Username string
		Password string
	}
	user := User{"member_01", "Test123"}
	fmt.Printf("some struct        : %+v\n", user)
	// channel
	var ch = make(chan int)
	go func() {
		ch<-1
	}()
	fmt.Printf("some channel       : %v\n", <-ch)
	fmt.Printf("for boolean        : %t\n", false)
	// function
	someFunc := func(a, b int) int{
		return a + b
	}
	fmt.Printf("some func		   : %v\n", someFunc(2,3))
	// switch index
	fmt.Printf("switch index       : %[2]d %[1]d\n", 11, 22)
	fmt.Printf("switch index       : %[3]s %[2]d %[1]d\n", 11, 22, "some_string")
	fmt.Printf("switch index       : %[4]t %[3]s %[2]d %[1]d\n", 11, 22, "some_string", true)
}
```

```
for binary value   : 1010 
for integer        : 123
for scientific notation : (3.000000e+00+5.000000e+00i)
for float          : 1.234000
float rounding     : 12.35
string example     : member 01
type data of member_01 is : string
type data of 123 is : int
for pointer        : 0xc000040260
some interface     : 123
some array         : [1 2 3]
some slice         : [1 2 3]
some struct        : {Username:member_01 Password:Test123}
some channel       : 1
for boolean        : false
some func                  : 5
switch index       : 22 11
switch index       : some_string 22 11
switch index       : true some_string 22 11
```

## Contoh code penggunaan Sprintln

```go
package main

import "fmt"

func main() {					
	fmt.Println(fmt.Sprintln("Hello"))
	fmt.Println(fmt.Sprintln("for integer        :", 123))
	fmt.Println(fmt.Sprintln("for scientific notation :", 3 + 5i))
	fmt.Println(fmt.Sprintln("for float          :", 1.234))
	fmt.Println(fmt.Sprintln("float rounding     :", 12.3456))
	fmt.Println(fmt.Sprintln("string example     :", "member 01"))
	fmt.Println(fmt.Sprintln("boolean example    :", false))
	var someInterface interface{} = 123
	fmt.Println(fmt.Sprintln("for pointer    	:", &someInterface))
	fmt.Println(fmt.Sprintln("some interface     :", someInterface))
	fmt.Println(fmt.Sprintln("some array         :", [3]int{1,2,3}))
	fmt.Println(fmt.Sprintln("some slice         :", []int{1,2,3}))
	fmt.Println(fmt.Sprintln("some map           :", map[string]interface{}{
		"username": "member_01",
		"password": "Test123",
	}))
	// struct
	type User struct {
		Username string
		Password string
	}
	user := User{"member_01", "Test123"}
	fmt.Println(fmt.Sprintln("some struct        :", user))
	// channel
	var ch = make(chan int)
	go func() {
		ch<-1
	}()
	fmt.Println(fmt.Sprintln("some channel       :", <-ch))
	// function
	someFunc := func (a, b int) int {
		return a + b
	}
	fmt.Println(fmt.Sprintln("some func          :", someFunc(2, 3)))
}
```

```
Hello

for integer        : 123

for scientific notation : (3+5i)

for float          : 1.234

float rounding     : 12.3456

string example     : member 01

boolean example    : false

for pointer     : 0xc000088040

some interface     : 123

some array         : [1 2 3]

some slice         : [1 2 3]

some map           : map[password:Test123 username:member_01]

some struct        : {member_01 Test123}

some channel       : 1

some func          : 5

```

## Contoh code penggunaan Sprintf

```go
package main

import (
	"fmt"
)

func main() {
	fmt.Println(fmt.Sprintf("for binary value   : %b ", 10))
	fmt.Println(fmt.Sprintf("for integer        : %d", 123))
	fmt.Println(fmt.Sprintf("for scientific notation : %e ", 3 + 5i))
	fmt.Println(fmt.Sprintf("for float          : %f ", 1.234))
	fmt.Println(fmt.Sprintf("float rounding     : %.2f", 12.3456))
	fmt.Println(fmt.Sprintf("string example     : %s", "member 01"))
	var someInterface interface{} = 123
	fmt.Println(fmt.Sprintf("type data of %s is : %T", "member_01", "member_01"))
	fmt.Println(fmt.Sprintf("type data of %d is : %T", someInterface, someInterface))
	fmt.Println(fmt.Sprintf("for pointer    	   : %p", &someInterface))
	fmt.Println(fmt.Sprintf("some interface     : %v", someInterface))
	fmt.Println(fmt.Sprintf("some array         : %v", [3]int{1,2,3}))
	fmt.Println(fmt.Sprintf("some slice         : %v", []int{1,2,3}))
	// struct
	type User struct {
		Username string
		Password string
	}
	user := User{"member_01", "Test123"}
	fmt.Println(fmt.Sprintf("some struct        : %+v", user))
	// channel
	var ch = make(chan int)
	go func() {
		ch<-1
	}()
	fmt.Println(fmt.Sprintf("some channel       : %v", <-ch))
	fmt.Println(fmt.Sprintf("for boolean        : %t", false))
	// function
	someFunc := func(a, b int) int{
		return a + b
	}
	fmt.Println(fmt.Sprintf("some func		   : %v", someFunc(2,3)))
}
```

```
for binary value   : 1010 
for integer        : 123
for scientific notation : (3.000000e+00+5.000000e+00i)
for float          : 1.234000
float rounding     : 12.35
string example     : member 01
type data of member_01 is : string
type data of 123 is : int
for pointer        : 0xc000088290
some interface     : 123
some array         : [1 2 3]
some slice         : [1 2 3]
some struct        : {Username:member_01 Password:Test123}
some channel       : 1
for boolean        : false
some func                  : 5
```
