# Relational Operator

Relational operator merupakan operasi untuk membadingkan dua buah data untuk menentukan true atau false. Operator ini menggunakan tanda ->  >, <, >=, <=, ==, &&, !=.

## Contoh code operator relational untuk membandingkan string,  integer dan float

```go
package main

import (
	"fmt"
)

func main() {
	var name1 = "Test1"
	var name2 = "Test2"

	var compareName1 bool = name1 == name2
	fmt.Println(compareName1)

	var name3 = "Test1"
	var name4 = "test1"

	var compareName2 bool = name3 == name4
	fmt.Println(compareName2)

	var value1 = 123
	var value2 = 121

	var compareDigit1 bool = value1 != value2
	fmt.Println(compareDigit1)

	// var value3 = 2
	// var value4 = 2.0

	// var compareDigit2 bool = value3 == value4 // -> cannot compare value3 == value4 (mismatched types int and float64)
	// fmt.Println(compareDigit2)

	var float1 = 123
	var float2 = 121

	var compareFloat1 bool = float1 == float2
	fmt.Println(compareFloat1)

	var float3 = 123.0
	var float4 = 123.00

	var compareFloat2 bool = float3 == float4
	fmt.Println(compareFloat2)
}
```

```
false
false
true
false
true
```

## Contoh code operator relational untuk membandingkan tipe data string

```go
package main

import (
	"fmt"
)

func main() {
	var str1 string = "Test1"
	var str2 string = "Testb"
	var str3 string = "test1"

	fmt.Println(str1 == str2) // false
	fmt.Println(str1 == str3) // false
	fmt.Println(str1 != str3) // true

	fmt.Println(str1 < str2)  // true
	fmt.Println(str1 < str3)  // true
	fmt.Println(str1 <= str2) // true
	fmt.Println(str1 <= str3) // true
}
```

```
false
false
true
true
true
true
true
```

## Contoh code operator relational untuk membandingkan tipe data boolean

```go
package main

import (
	"fmt"
)

func main() {
	var bool1 bool = true
	var bool2 bool = false
	fmt.Println(bool1 == bool2)    // true
	fmt.Println(bool1 && bool2)	   // true
	fmt.Println(bool1 != bool2)    // false

	// fmt.Println(bool1 < bool2)
	// fmt.Println(bool1 <= bool2)
}
```

```
false
false
true
```

## Contoh code operator relational untuk membandingkan data array, map, slice dan function

```go
package main

import (
	"fmt"
)

func main() {
	// array
	var a1 = [3]int{1, 2, 3}
	var a2 = [3]int{1, 2, 3}
	fmt.Println(a1 == a2) // true
	// map can only be compared to nil
	var m1 = map[string]int{
		"member1": 123,
	}
	fmt.Println(m1 == nil) // false
	// slice can only be compared to nil
	var s1 = []int{1, 2, 3}
	fmt.Println(s1 == nil) // false
	// func can only be compared to nil
	var f1 = func() {
		fmt.Println("test1")
	}
	fmt.Println(f1 == nil) // false
	// channel
	var ch chan string
	fmt.Println(ch == nil) // true
}

```

```
true
false
false
false
true
```
