# Once

Once dapat digunakan untuk memastikan sebuah function di eksekusi hanya sekali.

## Contoh _code_

```go
package main

import (
	"fmt"
	"sync"
)

var wg sync.WaitGroup
var once sync.Once

func print() {
	fmt.Printf("test")
}

func main() {
	for i := 0; i < 1000; i++ {
		wg.Add(1)
		go func() {
			once.Do(print)
		}()
		go func() {
			once.Do(print)
		}()
		wg.Done()
	}

	wg.Wait()
}

```

```
test
```
