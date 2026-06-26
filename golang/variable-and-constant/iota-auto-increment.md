---
description: by Mochamad Rafli Ramadhan
---

# Iota (Auto Increment)

Iota digunakan untuk menginisiasi beberapa constant dengan tipe data integer, float atau complex yang membutuhkan value auto increment.

## Contoh code deklarasi iota dengan integer

```go
package main

import (
	"fmt"
)

func main() {
	const (
		num1 = 2 + iota*2
		num2
		num3
	)
	fmt.Println(num1, num2, num3)
	
	
	const (
		num4 = 2.2 + iota*3
		num5
		num6
	)
	fmt.Println(num4, num5, num6)

	// Contoh untuk deklarasi variabel hari menjadi integer dari 1 sampai 7
	const (
		Monday = 1 + iota
		Tuesday
		Wednesday
		Thursday
		Friday
		Saturday
		Sunday
	)
	fmt.Println(Monday)

	// Contoh untuk deklarasi variabel bulan menjadi integer dari Januari sampai Desember
	const (
		January = 1 + iota
		February
		March
		April
		May
		June
		July
		August
		September
		October
		November
		December
	)
	fmt.Println(January)
}
```

```
2 4 6
2.2 5.2 8.2
1
1
```

## Contoh code deklarasi constant iota dengan complex

```go
package main

import (
	"fmt"
)

func main() {
	const (
		num1 = 2+5i + iota*2
		num2
		num3
	)
	fmt.Println(num1, num2, num3)
	
	
	const (
		num4 = 2+3i + iota*3
		num5
		num6
	)
	fmt.Println(num4, num5, num6)
}
```

```
(2+5i) (4+5i) (6+5i)
(2+3i) (5+3i) (8+3i)
```
