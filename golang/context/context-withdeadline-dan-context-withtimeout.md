# Context WithDeadline dan Context WithTimeout

Jika ditelusuri pada code context WithTimeout terdapat code Context WithDeadline. Keduanya sama, namun berbeda secara pengertian.

* WithDeadline digunakan untuk mengakhiri context dengan deadline waktu sekarang + beberapa waktu kedepan. WithDeadline juga bisa digunakan untuk mengakhiri context pada waktu tertentu dalam tanggal dan jam. Jika tanggal dan jam sudah terlampaui, maka context deadline akan langsung di eksekusi.
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

## Contoh code contextWithDeadline dengan deadline tanggal dan jam di masa depan

```go
package main

import (
	"context"
	"errors"
	"fmt"
	"time"
)

func main() {
	// Set deadline ke waktu spesifik, misal jam 17:30:00 hari ini
	deadline := time.Date(2026, 6, 30, 18, 00, 0, 0, time.Local)

	ctx, cancel := context.WithDeadline(context.Background(), deadline)
	defer cancel() // selalu panggil cancel untuk release resource, meski deadline sudah lewat

	doWork(ctx)
}

func doWork(ctx context.Context) {
	select {
	case <-time.After(5 * time.Second): // simulasi kerjaan yang butuh waktu 5 detik
		fmt.Println("pekerjaan selesai sebelum deadline")

	case <-ctx.Done():
		err := ctx.Err()
		if errors.Is(err, context.DeadlineExceeded) {
			fmt.Println("dibatalkan karena deadline terlampaui:", err)
		} else if errors.Is(err, context.Canceled) {
			fmt.Println("dibatalkan manual:", err)
		}
	}
}
```

```
pekerjaan selesai sebelum deadline
```

## Contoh code contextWithDeadline dengan deadline tanggal dan jam di masa lalu

```go
package main

import (
	"context"
	"errors"
	"fmt"
	"time"
)

func main() {
	// Set deadline ke waktu lampau
	deadline := time.Date(2026, 6, 29, 17, 00, 0, 0, time.Local)

	ctx, cancel := context.WithDeadline(context.Background(), deadline)
	defer cancel() // selalu panggil cancel untuk release resource, meski deadline sudah lewat

	doWork(ctx)
}

func doWork(ctx context.Context) {
	select {
	case <-time.After(5 * time.Second): // simulasi kerjaan yang butuh waktu 5 detik
		fmt.Println("pekerjaan selesai sebelum deadline")

	case <-ctx.Done():
		err := ctx.Err()
		if errors.Is(err, context.DeadlineExceeded) {
			fmt.Println("dibatalkan karena deadline terlampaui:", err)
		} else if errors.Is(err, context.Canceled) {
			fmt.Println("dibatalkan manual:", err)
		}
	}
}
```

```
dibatalkan karena deadline terlampaui: context deadline exceeded
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
