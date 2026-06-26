# Defer

Defer digunakan untuk mengakhiri eksekusi suatu statement tepat sebelum blok fungsi selesai, akan selalu dieksekusi di akhir.

## Contoh _code_ defer

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    Defer0()
    defer fmt.Println("Defer 1")
    defer fmt.Println("Defer 2")
    defer func() {
        defer fmt.Println("Defer 3")
        defer fmt.Println("Defer 4")
    }()
    Defer5()
    time.Sleep(3 * time.Second)
    fmt.Println("End")
}

func Defer0() {
    defer fmt.Println("Defer 0")
}

func Defer5() {
    defer fmt.Println("Defer 5")
}
```

```
Defer 0
Defer 5
End
Defer 4
Defer 3
Defer 2
Defer 1
```
