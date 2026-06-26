# Logic Operator

Logical merupakan operator untuk membandingkan 2 tipe data boolean. Operator ini memiliki operasi AND, OR, NOT/negasi yang masing-masing menggunakan tanda &&, || dan tanda !.

## Contoh code operator logic pada string

```go
package main

import (
	"fmt"
)
func main() {
	var str1 string = "Test1"
	var str2 string = "Testb"
	var str3 string = "test1"
	fmt.Println(str1 == str2 && str1 != str3) 	// (0*1) : false
	fmt.Println(str1 == str2 || str1 != str3)   // (0+1) : true
	fmt.Println(!(str1 == str2))				// true
}
```

```
false
true
true
```

## Contoh code operator logic pada boolean

```go
package main

import (
	"fmt"
)

func main() {
   var bool1 bool = false
   var bool2 bool = true

   fmt.Println(bool1 && bool2)
   fmt.Println(bool1 || bool2)
   fmt.Println(!bool1)
   fmt.Println(!bool2)
}
```

```
false
true
true
false
```
