# Pointer pada Parameter di Function

Tipe data berbasis pointer dapat digunakan sebagai parameter di sebuah function.

## Contoh code

```go
package main

import (
    "fmt"
)

func main() {
    name1 := "member_1"
    name2 := &name1
    ChangeName(name2)
    fmt.Println(name1)
}

func ChangeName(name *string) {
    *name = "member_2"
}
```

```
member_2
```

