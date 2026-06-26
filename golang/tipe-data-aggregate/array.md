# Array

Array merupakan jenis tipe data aggregate di Golang yang mampu menampung beberapa value dengan tipe data yang sama dengan jumlah (length) tertentu. Kekurangan dari array adalah hanya bisa di isi value sesuai dengan length yang telah di deklarasikan. Untuk default value dari suatu array akan bergantung pada tipe data yang digunakan.

## Contoh code array dengan tipe data string

```go
package main

import (
	"fmt"
)

func main() {
	var names [3]string
	fmt.Println(names)

	names[0] = "Test1"
	names[1] = "Test2"
	names[2] = "Test3"
	// names[3] = "Test4" -> error karena melebihi length dari array
	fmt.Printf("%s %s %s \n", names[0], names[1], names[2])

	var values = [3]int{12, 13, 14}
	fmt.Println(values)
}
```

```
[  ]
Test1 Test2 Test3 
[12 13 14]
```

## Contoh code array dengan tipe data interface kosong

```go
package main

import "fmt"

var i1 any = 2
var i2 any = 2
var i3 any = 2
var i4 any = 2
var i5 any = 2

var a [10]interface{} = [10]interface{}{i1, i2, i3, i4, i5}

func main() {
    fmt.Println(a)
}

```

```
[2 2 2 2 2 <nil> <nil> <nil> <nil> <nil>]
```

## Contoh code array dengan tipe data pointer

```go
package main

import "fmt"

var num1 int = 2
var num2 *int = &num1
var num3 *int = &num1
var num4 *int = &num1

var a [10]*int = [10]*int{num2, num3, num4}

func main() {
    fmt.Println(a)
}

```

```
[0xbbb340 0xbbb340 0xbbb340 <nil> <nil> <nil> <nil> <nil> <nil> <nil>]
```

## Jumlah value dan Kapasitas dari Array

Kapasitas merupakan tempat untuk menampung value, sementara length adalah berapa banyak kapasitas yang sudah diisi nilai. Kapasitas dari array akan selalu sama dengan jumlah value yang ada di dalam array.

```go
package main

import "fmt"

func main() {
	arr := [5]int{1, 2, 3, 4, 5}
	fmt.Println(len(arr))
	fmt.Println(cap(arr))
}
```

```
5
5
```

## Informasi tambahan

Suatu array misalkan arr1 akan disimpan dengan memory address yang berbeda dari value-value di dalam array tersebut. Sebagai contoh code di bawah ini, array arr1 disimpan pada memory address 0xc000014280, sementara value dalam array arr1 yaitu 1, 2, 3, dst disimpan dalam memory address 0xc00000e088.

```go
package main
import "fmt"

func main() {
    arr1 := [10]int{1,2,3,4,5,6,7,8,9,10}
	arr2 := &arr1
    fmt.Printf("%p\n", arr2)
    for i := range a {
        val := &i
        fmt.Println(val)
    }
}
```

```
0xc000014280
0xc00000e088
0xc00000e088
0xc00000e088
0xc00000e088
0xc00000e088
0xc00000e088
0xc00000e088
0xc00000e088
0xc00000e088
0xc00000e088
```

## Add, Update dan Delete Value di Array

Untuk delete value tidak bisa dilakukan di array dan hanya bisa mengganti value dari index yang ingin di delete dengan default value dari tipe data yang digunakan

```go
package main

import (
	"fmt"
)

func main() {
	var arr = [5]int{1, 2, 3, 4}
	// add
	arr[4] = 5
	// update
	arr[4] = -5
	fmt.Println(arr)
	// detele (default value integer = 0)
	arr[4] = 0
	fmt.Println(arr)
}
```

```
[1 2 3 4 -5]
[1 2 3 4 0]
```
