# Looping For

Looping merupakan cara untuk mengulangi urutan data dari suatu string, array, map dan string.&#x20;

## Contoh code looping sederhana

```go
package main
 
import "fmt"
 
func main() {
	i := 1
	for ; i <= 10; i++ {
		fmt.Println(i)
	}
 
	i = 1
	for i <= 10 {
		fmt.Println(i)
		i++
	}
 
	for i := 1; ; i++ {
		fmt.Println(i)
		if i == 10 {
			break
		}
	}
}
```

```
1
2
3
4
5
6
7
8
9
10
1
2
3
4
5
6
7
8
9
10
1
2
3
4
5
6
7
8
9
10
```

## Contoh code looping for dengan operator assignment

Operator assignment seperti +=, -=, \*=, /= atau %= dapat digunakan untuk meng-update value dari integer yang diinisiasi di awal.

```go
package main

import "fmt"

func main() {
    i := 0
    for i < 10 {
        fmt.Println(i)
        i += 2
    }
}
```

```
0
2
4
6
8
```

Reference:

{% embed url="https://stackoverflow.com/questions/58635507/rune-vs-byte-ranging-over-string" %}

{% embed url="https://www.golangprograms.com/for-range-loops.html" %}
