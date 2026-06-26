# Context WithDeadline dan Context WithTimeout

Jika ditelusuri pada code context WithTimeout terdapat code Context WithDeadline. Keduanya sama, namun berbeda secara pengertian.

* WithDeadline digunakan untuk mengakhiri context dengan deadline waktu sekarang + beberapa waktu kedepan.
* WithTimeout digunakan untuk menjalankan suatu code sampai waktu tertentu.

## Contoh code context WithDeadline

```go
package main

import (
	"context"
	"fmt"
	"time"
)

func main() {
	deadline := time.Now().Add(1 * time.Millisecond)

	ctx, cancel := context.WithDeadline(context.Background(), deadline)
	defer cancel()

	select {
	case <-time.After(1 * time.Second):
		fmt.Println("overslept")
	case <-ctx.Done():
		fmt.Println(ctx.Err())
	}
}
```

```
context deadline exceeded
```

## Contoh code context WithTimeout

```go
package main

import (
	"context"
	"fmt"
	"time"
)

func main() {
	ctx, cancel := context.WithTimeout(context.Background(), 1 * time.Millisecond)
	defer cancel()

	select {
	case <-time.After(1 * time.Second):
		fmt.Println("overslept")
	case <-ctx.Done():
		fmt.Println(ctx.Err())
	}
}

```

```
context deadline exceeded
```
