---
coverY: 0
---

# Nil

Nil merupakan default value dari beberapa tipe data seperti slice, map, pointer dan interface.&#x20;

```go
package main

import "fmt"

func main() {
    var someSlice []string
    if someSlice == nil {
        fmt.Println(someSlice)
        fmt.Println("yes nil")
    }
    
    var someMap map[string]string
    if someMap == nil {
        fmt.Println(someMap)
        fmt.Println("yes nil")
    }
    
    var someInterface any
    if someInterface == nil {
        fmt.Println(someInterface)
        fmt.Println("yes nil")
    }
    
    var somePointer *string
    if somePointer == nil {
        fmt.Println(somePointer)
        fmt.Println("yes nil")
    }
}
```

```
[]
yes nil
map[]
yes nil
<nil>
yes nil
<nil>
yes nil
```

Nil juga dapat digunakan sebagai return value dari suatu function seperti contoh code di bawah ini.

```go
package main

import (
	"fmt"
)

func Logging(text string) map[string]string {
    if text == "" {
        return nil
    } else {
        return map[string]string{
            "Text": text,
        }
    }
}

func main() {
    if check:= Logging(""); check == nil {
        fmt.Println("Data is empty")
    } else {
        fmt.Println(check)
    }
}
```

```
Data is empty
```

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
    result, err := Pembagian(12,0)
    if err != nil {
        fmt.Println(err)         // return interface
        fmt.Println(err.Error()) // return string
    } else {
        fmt.Println(result)
    }
}
```

```
b should not 0
b should not 0
```
