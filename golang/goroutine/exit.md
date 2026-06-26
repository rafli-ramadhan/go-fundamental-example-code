# Exit

Exit digunakan untuk menghentikan blok fungsi secara paksa.

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    defer fmt.Println("halo")
    os.Exit(1)
    fmt.Println("selamat datang")
}
```

```
exit status 1
```
