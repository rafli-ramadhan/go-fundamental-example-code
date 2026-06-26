# Slice

Slice merupakan tipe data reference di Golang yang hampir mirip dengan array. Perbedaanya tidak perlu ada length declaration seperti array. Kelebihan dari slice yaitu tidak perlu mendefinisikan berapa banyak value yang akan ditampung dalam data. Sementara kekurangan dari slice yaitu saat di inputkan value yang melebihi capasitas slice, maka capasitas slice akan menjadi 2 kali lipat.

## Membuat Slice dari Array

Slice dapat dibuat dengan mengambil value dari suatu array seperti contoh di bawah ini.

```go
package main

import "fmt"

func main() {
	arr := [5]int{1, 2, 3, 4, 5}
	slice := arr[1:4]
	fmt.Println(slice)
	fmt.Println(len(slice))
	fmt.Println(cap(slice))

	slice = append(slice, 5, 6)
	fmt.Println(slice)
	fmt.Println(len(slice))
	fmt.Println(cap(slice))
}
```

```
[2 3 4]
3
4
[2 3 4 5 6]
5
8
```

## Membuat Slice dengan Fungsi Make

Make digunakan untuk membuat suatu slice. Fungsi make memiliki 3 input parameter yaitu tipe data, length dan capacity. Capacity harus lebih dari length (capacity > length). Capacity ibaratkan beberapa kotak untuk menyimpan suatu nilai, sementara length dapat diartikan berapa kotak yang sudah diisi suatu nilai. Make akan mengisi capacity dari suatu slice dengan default value dari tipe data yang digunakan.

### Contoh Code Deklarasi Slice dengan Capacity > Length

```go
package main

import (
	"fmt"
)

func main() {
	// slice int
        slice1 := make([]int, 5, 5)
	fmt.Println(slice1)
	// slice string
	slice2 := make([]string, 5, 5)
	fmt.Println(slice2)
	// slice float64
	slice3 := make([]float64, 5, 5)
	fmt.Println(slice3)
	// slice bool
	slice4 := make([]bool, 5, 5)
	fmt.Println(slice4)
}
```

```
[0 0 0 0 0]
[    ]
[0 0 0 0 0]
[false false false false false]
```

### Contoh Code Deklarasi Slice dengan Capacity < Length

<pre class="language-go"><code class="lang-go"><strong>package main
</strong>import "fmt"

func main() {
    a := make([]int, 5, 2)
    fmt.Println(a)
}
</code></pre>

```
invalid argument: length and capacity swapped
```

## Input Value lebih dari Length Slice

```go
package main
import "fmt"

func main() {
    a := make([]int, 5, 6)
    a[0], a[1], a[2], a[3], a[4], a[5] = 1, 2, 3, 4, 5, 6
    fmt.Println(a)
}
```

```
panic: runtime error: index out of range [5] with length 5
```

## Kekurangan Slice

Saat kita menginputkan suatu value ke dalam slice yang melebihi length dari slice, capacity dari slice tersebut akan menjadi 2 kali lipatnya. Cotohnya seperti code dibawah ini. Slice s yang awalnya tidak mempunyai value, kemudian di isi value secara bertahap menggunakan looping. Lalu di tampilkan kapasitas dan length dari slice tersebut.

```go
package main
import "fmt"

func main() {
    s := make([]int, 0, 3)
    fmt.Println(s)
    for i := 0; i < 20; i++ {
        s = append(s, i)
        fmt.Printf("cap %v, len %v, %p\n", cap(s), len(s), s)
    }
}
```

```
[]
cap 3, len 1, 0xc000018018
cap 3, len 2, 0xc000018018
cap 3, len 3, 0xc000018018
cap 6, len 4, 0xc000014270
cap 6, len 5, 0xc000014270
cap 6, len 6, 0xc000014270p
cap 12, len 7, 0xc00005e060
cap 12, len 8, 0xc00005e060
cap 12, len 9, 0xc00005e060
cap 12, len 10, 0xc00005e060
cap 12, len 11, 0xc00005e060
cap 12, len 12, 0xc00005e060
cap 24, len 13, 0xc00007a000
cap 24, len 14, 0xc00007a000
cap 24, len 15, 0xc00007a000
cap 24, len 16, 0xc00007a000
cap 24, len 17, 0xc00007a000
cap 24, len 18, 0xc00007a000
cap 24, len 19, 0xc00007a000
cap 24, len 20, 0xc00007a000
```

## Add Value

Untuk menambahkan value dalam suatu slice dapat menggunakan fungsi append.

```go
package main
import "fmt"

func main() {
    a := []int{1,2,3,4,5}
    a = append(a, 6)
    fmt.Println(a)
}
```

```
[1 2 3 4 5 6]
```

## Update Value

Untuk memperbaruhi value dengan index tertentu dari suatu slice, dapat langsung diubah seperti contoh di bawah ini.

```go
package main
import "fmt"

func main() {
    a := [5]int{1,2,3,4,5}
    a[2] = 10
    fmt.Println(a)
}
```

```
[1 2 10 4 5]
```

## Delete Value

Untuk menghapus suatu value dengan index tertentu di slice dapat menggunakan fungsi append. Dimana append memiliki format append(slice, ...value). Parameter kedua dalam fungsi append merupakan variadic function, yang berarti append dapat menerima lebih dari 2 input.

```go
package main
import "fmt"

func main() {
    a := []int{1,2,3,4,5}
    a = append(a[:2], a[2+1:]...)
    fmt.Println(a)
}
```

```
[1 2 4 5]
```

Kodingan di atas sama memiliki algoritma yang sama dengan kodingan di bawah ini :

```go
package main
import "fmt"

func main() {
    a := []int{1,2,3,4,5}
    a = append(a[:2], []int{4,5}...)
    fmt.Println(a)
}
```

```go
package main
import "fmt"

func main() {
    a := []int{1,2,3,4,5}
    a = append(a[:2], 4, 5)
    fmt.Println(a)
}
```

## Informasi tambahan

Suatu slice misalkan s akan disimpan dengan _memory address_ yang berbeda dengan value-value di dalam slice tersebut.

```go
package main
import "fmt"

func main() {
    s := make([]int, 0, 3)
    for i := 0; i < 5; i++ {
        s = append(s, i)
        fmt.Printf("cap %v, len %v, %p\n", cap(s), len(s), s)
        for i := range s {
            val := &i
            fmt.Println(val)
        }
    }
}
```

```
cap 3, len 1, 0xc000018018
0xc00001a050
cap 3, len 2, 0xc000018018
0xc00001a058
0xc00001a058
cap 3, len 3, 0xc000018018
0xc00001a060
0xc00001a060
0xc00001a060
cap 6, len 4, 0xc000014270
0xc00001a068
0xc00001a068
0xc00001a068
0xc00001a068
cap 6, len 5, 0xc000014270
0xc00001a070
0xc00001a070
0xc00001a070
0xc00001a070
0xc00001a070
```

