---
coverY: 0
---

# Konversi Tipe Data

Konversi tipe data digunakan untuk mengubah value dengan tipe data tertentu ke tipe data yang lain.

## Contoh code konversi integer ke float

Value dengan tipe data integer bisa diubah menjadi float, karena di tipe data float terdapat integer.

```go
package main

import (
	"fmt"
)

func main() {
	var num1 int = 2
	var num2 float64 = float64(num1)
	fmt.Println(num2)
	fmt.Printf("%T\n", num2)
}
```

```
2
float64
```

## Contoh code konversi float ke integer

Value dengan tipe data float dapat dikonversi menjadi integer dan akan dibulatkan ke bawah.

```go
package main

import (
	"fmt"
)

func main() {
	var num1 float64 = 2.9
	var num2 int = int(num1)
	fmt.Println(num2)
	fmt.Printf("%T", num2)
}
```

```
2
int
```

## Contoh code konversi boolean ke string

Boolean tidak dapat dikonversi menjadi string

```go
package main

import (
	"fmt"
)

func main() {
	var isFalse bool = true
	fmt.Printf(string(isFalse))
}
```

```
cannot convert isFalse (variable of type bool) to type string
```

## Contoh code konversi string menjadi rune dan byte

Konversi string menjadi byte akan menghasilkan angka yang mewakili karakter ASCII, sementara konversi menjadi rune akan menghasilkan angka yang mewakili karakter Unicode.

```go
package main
 
import (
    "fmt"
)
 
func main() {
    s := "GÖLANG PROGRAMMING golang programming" // Ö is a non-ASCII character 
 
    s_rune := []rune(s)
    s_byte := []byte(s)
     
    fmt.Println(s_rune)
    fmt.Println(s_byte)
}
```

```
[71 214 76 65 78 71 32 80 82 79 71 82 65 77 77 73 78 71 32 103 111 108 97 110 103 32 112 114 111 103 114 97 109 109 105 110 103]
[71 195 150 76 65 78 71 32 80 82 79 71 82 65 77 77 73 78 71 32 103 111 108 97 110 103 32 112 114 111 103 114 97 109 109 105 110 103]
```

Reference :

{% embed url="https://golangdocs.com/rune-in-golang" %}
