# Blank Identifier (Variable Underscore)

Variabel underscore (\_) digunakan untuk menampung suatu value yang tidak ingin digunakan.

## Contoh code 1

Variabel underscore bisa digunakan untuk menampung value dari return output suatu function yang tidak digunakan seperti contoh di bawah ini.

```go
package main

import (
    "errors"
    "fmt"
)

func Pembagian(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("b should not 0")
    } else {
        return a/b, nil
    }
}

func main() {
    result, _:= Pembagian(12,0)
    fmt.Println(result)
}
```

```
0
```

## Contoh code 2

```go
package main

import (
	"fmt"
)

func main() {
	_ = "example string"
	name, _, id, _ := "member_01", "Test123", 123, map[string]interface{}{
		"username": "member_01",
		"password": "Test123",
	}

	fmt.Println(name)
	fmt.Println(id)

	someFunc := func(a, b int) (int, int) {
		return a + b, a * b
	}
	sum, _ := someFunc(2,3)
	fmt.Println(sum)
}
```

```
member_01
123
5
```

Reference:

{% embed url="https://github.com/godlixe/modul-go/blob/main/dasar-dasar-golang.md#slice" %}
