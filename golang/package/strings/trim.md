# Trim

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
    str1 := "!! Test !!"
    str2 := "@@Test$$"
    fmt.Println(strings.Trim(str1, "!"))
    fmt.Println(strings.Trim(str2, "@$"))
}
```

```
Test
Test
```
