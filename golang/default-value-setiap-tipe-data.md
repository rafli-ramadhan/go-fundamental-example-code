---
coverY: 0
---

# Default Value setiap Tipe Data

Default value untuk setiap tipe data dirinci sebagai berikut:

1. Integer dan Unsigned Integer -> 0
2. Float dan Complex -> 0
3. String -> ""
4. Boolean -> false
5. Array -> menyesuaikan tipe data yang digunakan
6. Struct -> menyesuaikan tipe data dari setiap property di dalam struct &#x20;
7. Map -> nil
8. Slice -> nil
9. Function -> nil
10. Channel -> nil
11. Interface Kosong -> nil

Berikut merupakan code untuk mengetahui default value dari setiap tipe data seperti array, struct, slice, interface dan map.&#x20;

```go
package main

import(
	"fmt"
)

func main() {
	var arr [3]int
	fmt.Println(arr)

	type User struct {
		Name  string
		Age   int
	}
	var user User
	fmt.Println(user == User{})

	var exampleSlice []int
	fmt.Println(exampleSlice == nil)

	type error interface {
		Error() string
	}

	var err error
	fmt.Println(err == nil)

	var exampleMap map[string]int					
	fmt.Println(exampleMap == nil)

	var exampleMap2 map[string]int = map[string]int{}
	fmt.Println(exampleMap2 == nil)
}
```

```
[0 0 0]
{ 0}
true
[]
true
true
true
false
```
