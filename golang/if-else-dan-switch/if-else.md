# If Else

If else  merupakan salah satu bentuk percabangan di golang.

## Contoh _code_

```go
package main

import "fmt"

func main() {
    name1 := "Umar"
    if name1 == "Umar" {
        fmt.Printf("Hello %v \n", name1)
 	} else if name1 == "Umar" {
		fmt.Println("Hello")
	} else {
		fmt.Println("Hi, Boleh kenalan?")
	}

	// if else with variable temporary
	if name2 := "Umar"; name2 == "Umar" {
        fmt.Printf("Hello %v", name2)
 	} else if name2 == "Umar" {
		fmt.Println("Hello")
	} else {
		fmt.Println("Hi, Boleh kenalan?")
	}

	if len := len(name1); len > 5 {
		fmt.Println("\nNama terlalu panjang")
	} else {
		fmt.Println("\nNama sudah benar")
	}	
}
```

```
Hello Umar 
Hello Umar
Nama sudah benar
```
