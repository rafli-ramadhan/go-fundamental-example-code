# Default Value Pointer

Saat suatu pointer di inisiasi tapi tidak di deklarasikan value-nya, maka value-nya adalah nil.

## Contoh code

```go
package main

import "fmt"

func main() {
  // declare a pointer variable
  var num *int
  var str *string
  var dec *float64
  var isTrue *bool
  type example struct {
      num *int
      str *string
  }
  e := example{}

  fmt.Println("Value of pointer:", num)
  fmt.Println("Value of pointer:", str)
  fmt.Println("Value of pointer:", dec)
  fmt.Println("Value of pointer:", isTrue)
  fmt.Println("Value of pointer:", e)
}
```

```
Value of pointer: <nil>
Value of pointer: <nil>
Value of pointer: <nil>
Value of pointer: <nil>
Value of pointer: {<nil> <nil>}
```
