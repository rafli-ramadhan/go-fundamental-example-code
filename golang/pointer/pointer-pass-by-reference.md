# Pointer (Pass By Reference)

Kelebihan pointer yaitu memungkinkan penggunaan memory address seminimal mungkin. Suatu variabel bisa di inisiasi dengan value variabel lain, tanpa membuat memory address baru. Disebut reference karena variabel 1 dan variabel 2 punya value yang sama dan memory address yang sama.

Kekurangan dari pointer yaitu jika value variabel yang me-reference variabel lain diubah, value dari variabel yang di reference juga akan berubah.

## Contoh code

```go
package main
import "fmt"

func main() {
  var num  int
  var ptr *int
    
  num = 22
  fmt.Println("Address of num:",&num)
  fmt.Println("Value of num:",num)

  // assign the memory address of variable to the pointer
  ptr = &num
  fmt.Println("\nAddress of pointer:",ptr)
  fmt.Println("Value of pointer:",*ptr)
    
  num = 11
  fmt.Println("\nAddress of pointer:",ptr)
  fmt.Println("Value of pointer:",*ptr)
    
  *ptr = 2
  fmt.Println("\nAddress of num:",&num)
  fmt.Println("Value of num:",num)
}
```

```
Address of num: 0xc0000ba000
Value of num: 22

Address of pointer: 0xc0000ba000
Value of pointer: 22

Address of pointer: 0xc0000ba000
Value of pointer: 11

Address of num: 0xc0000ba000
Value of num: 2
```
