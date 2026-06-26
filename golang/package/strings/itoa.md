# Itoa

Digunakan untuk konversi integer ke string.

<pre class="language-go"><code class="lang-go"><strong>func Itoa(x int) string
</strong></code></pre>

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
    var val int = 1234
    str := strconv.Itoa(val)
    fmt.Printf("Result 1: %v", str)
    fmt.Printf("\nType 1: %T", str)
}

```
