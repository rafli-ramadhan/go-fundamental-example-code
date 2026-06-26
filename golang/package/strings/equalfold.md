# EqualFold

EqualFold digunakan untuk membandingkan 2 string. EqualFold sifatnya case insensitive.

```go
package main

import(
    "fmt"
    "strings"
)

func main() {
    fmt.Println(strings.EqualFold("Test", "test"))
    fmt.Println(strings.EqualFold("Test", "Test"))
}
```

```
true
true
```
