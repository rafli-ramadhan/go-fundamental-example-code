# Time Since

Time since merupakan fungsi untuk memperoleh durasi waktu dari sejak fungsi time.Now() di inisiasi ke suatu variabel.

## Contoh _code_ time since dengan time sleep detik

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	start := time.Now()
	// fmt.Println(start)
	time.Sleep(1 * time.Second)
	fmt.Println(time.Since(start))
	fmt.Println(time.Since(start).Nanoseconds())
	fmt.Println(time.Since(start).Microseconds())
	fmt.Println(time.Since(start).Milliseconds())
	fmt.Println(time.Since(start).Seconds())
	fmt.Println(time.Since(start).Minutes())
	fmt.Println(time.Since(start).Hours())
}

```

```
5.0137703s
5015350700
5016250
5017
5.0179141
0.08365447166666666
0.0013947766666666667
```

## Contoh _code_ time since dengan time sleep menit

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	start := time.Now()
	time.Sleep(1 * time.Minute)
	fmt.Println(time.Since(start))
	fmt.Println(time.Since(start).Nanoseconds())
	fmt.Println(time.Since(start).Microseconds())
	fmt.Println(time.Since(start).Milliseconds())
	fmt.Println(time.Since(start).Seconds())
	fmt.Println(time.Since(start).Minutes())
	fmt.Println(time.Since(start).Hours())
}

```

```
1m0.0130677s
60013966400
60014645
60015
60.0157221
1.0002705466666666
0.016671274333333333
```
