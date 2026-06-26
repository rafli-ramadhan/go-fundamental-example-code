# Split

```go
package main

import (
	"fmt"
	"strings"
)

func main() {		
	idStr := "1,2,3,4,5"
	id := strings.Split(idStr, ",")	
	fmt.Println(id)
}
```

```
[1 2 3 4 5]
```
