---
description: Package "os"
---

# Os

## Fungsi Create

Fungsi Create dalam package os digunakan untuk membuat file kosong berekstensi tertentu.

### Contoh code

```go
package main

import(
	"log"
	"os"
)

func main() {
	csvfile, err := os.Create("file/bookstore.csv")
	if err != nil {
		log.Panicln("Error create data", err)
	}

	defer func() {
		if err := csvfile.Close(); err != nil {
			log.Panicln("Error closing file", err)
		}
	}()
}
```

## Fungsi Args

Contoh code penggunaan fungsi os Args.

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    args1 := os.Args
    fmt.Println(args1)

    args2 := os.Args
    fmt.Println(args2)

}
```

```
[C:\Users\Lenovo\AppData\Local\Temp\go-build883185711\b001\exe\main.exe]
[C:\Users\Lenovo\AppData\Local\Temp\go-build883185711\b001\exe\main.exe]
```
