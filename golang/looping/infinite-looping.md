# Infinite Looping

Infinite looping digunakan untuk mengulangi suatu baris program sampai kondisi break terpenuhi.

## Contoh code infinite looping

```go
package main
 
import "fmt"
 
func main() {
	i := 3
	for {
		fmt.Print("Test-", i, " ")
		if i == 10 {
			break
		}
		i++
	}
}
```

```
Test-3 Test-4 Test-5 Test-6 Test-7 Test-8 Test-9 Test-10 
```

## Contoh code break nested looping dengan 1 kali break

Untuk kasus nested looping, break dapat di tulis sekali seperti contoh berikut.

```go
package main

func main() {
    out:
    for i := 0; i < 10; i++ {
        for j := 0; j < 10; j++ {
            if i + j == 20 {
                break out
            }
        }
    }
}
```

Reference:

{% embed url="https://stackoverflow.com/questions/51996175/how-to-break-out-of-nested-loops-in-go" %}
