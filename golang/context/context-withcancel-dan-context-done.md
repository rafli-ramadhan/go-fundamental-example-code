# Context WithCancel dan Context Done

## Context With Cancel

Context WithCancel digunakan untuk mengakhiri context.

```go
package main

import (
	"context"
	"fmt"
	"time"
)

func main() {
	ctx, cancel := context.WithCancel(context.Background())
	defer cancel()

	go func() {
		fmt.Println("before cancel")
		time.Sleep(2 * time.Second)
		cancel()
		fmt.Println("after cancel")
	}()

	select {
	case <-time.After(5 * time.Second):
		fmt.Println("more than 5 second")
	case <-ctx.Done():
		fmt.Println(ctx.Err())
	}
}
```

```
before cancel
after cancel
context canceled
```

## Context Done

Context Done digunakan untuk cek apakah context sudah selesai atau belum. Contoh code penerapan context done seperti code dibawah ini.

```go
package main

import (
	"context"
	"fmt"
	"time"
)

func main() {
	ctx, cancel := context.WithTimeout(context.Background(), 3*time.Second)
	defer cancel()

	select {
	case <-time.After(5 * time.Second):
		fmt.Println("more than 5 second")
	// jika program berjalan < 5 detik, maka case ini akan di pilih
	case <-ctx.Done():
		fmt.Println(ctx.Err())
	}
}
```

```
context deadline exceeded
```
