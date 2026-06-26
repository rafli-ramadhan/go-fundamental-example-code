# Atoi

Digunakan untuk mengkonversi string ke integer.

```go
func Atoi(str string) (int, error)
```

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	str := "1234"
	fmt.Printf("%v \n", str)
	fmt.Printf("%T \n", str)
	if s, err := strconv.Atoi(str); err == nil {
		fmt.Printf("%v \n", s)
		fmt.Printf("%T \n", s)
	}
}
```
