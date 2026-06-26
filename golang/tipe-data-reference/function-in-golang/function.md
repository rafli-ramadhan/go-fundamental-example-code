# Function

## Istilah penting dalam function :

* Parameter -> Data yang di input saat mengeksekusi sebuah function
* Function -> Barisan suatu kode yang dapat mengeksekusi suatu perintah dan bisa digunakan **secara berulang-ulang**.
* Acception
* Conversion

## Contoh function #1

```go
package main

import (
	"fmt"
)
	
func main() {
	result := sayHi("Dawam")
	fmt.Println(result)		
}

func sayHi(name string) string {
	return "Hi " + name + " nice to meet you"
}

```

## Contoh function #2 dengan return fmt.Sprintf

```go
package main

import (
	"fmt"
)
	
func main() {
	result := sayHi("Dawam")
	fmt.Println(result)		
}

func sayHi(name string) string {
	return fmt.Sprintf("Hi %s nice to meet you", name)
}

```



