# Function vs Procedure

Perbedaan function dan procedure adalah function mengembalikan suatu nilai, sementara procedure tidak. Prosedur hanya mengeksekusi bari kode saja.

## Contoh _code_ function

```go
package main

import "fmt"

func add(x int, y int) int {
    return x + y
}

func main() {
    fmt.Println(add(42, 13))
}

```

## Contoh _code_ prosedur

```go
package main

import (
	"fmt"
)

func main() {
	Introduction("Adi", "programmer", 1, 23)
}

func Introduction(name, job string, experience, age int) {
	fmt.Printf(`
	    Hello, Iam %s,
		I was an %s,
		I have %d experience
		and I am %d old.
	`, name, job, experience, age)
}
```

```
Hello, Iam Adi,
		I was an programmer,
		I have 1 experience
		and I am 23 old.
```

Reference:

{% embed url="https://www.golangprograms.com/go-language/functions.html" %}
