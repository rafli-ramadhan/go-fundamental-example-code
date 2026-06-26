# Time Sleep

Time sleep digunakan untuk menunda eksekusi suatu program sampai waktu tertentu.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
	fmt.Println("start")
	time.Sleep(3*time.Second)
	fmt.Println("end")
}
```

```
start
end
```
