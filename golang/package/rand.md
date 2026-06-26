---
description: Package "math/rand"
---

# Rand

## Fungsi Seed

Contoh code penggunaan fungsi Seed

```go
package main

import (
    "fmt"
    "math/rand"
    "time"
)

func main() {
    rand.Seed(time.Now().UnixNano())
    fmt.Printf("random integer 1: %d\n", rand.Int())
    fmt.Printf("random integer 2: %d\n", rand.Int())
    fmt.Printf("random integer 3: %d\n", rand.Int())
}
```

```
random integer 1: 741697430560038344
random integer 2: 4577369961301591295
random integer 3: 2371873606202891420
```
