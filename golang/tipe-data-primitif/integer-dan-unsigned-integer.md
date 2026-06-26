# Integer dan Unsigned Integer

Tipe data integer digunakan untuk menampung bilangan bulat, sementara tipe data unsigned integer digunakan untuk menampung bilangan cacah. Default value dari tipe data integer dan unsigned integer adalah 0. Untuk Int8, Int16, Int32, Int64 perbedaannya terletak pada jumlah nilai minimal dan maksimal value yang bisa ditampung. Selain itu, angka 8, 16, 32 dan 64 bisa disesuaikan dengan jumlah bit pada komputer yang digunakan. Tipe data int atau uint tanpa akhiran angka akan menyesuaikan jumlah bit pada komputer yang digunakan. Untuk nilai minimum dan maksimum dari tipe data int atau uint tertera pada tabel dibawah ini.

<figure><img src="../../.gitbook/assets/int.png" alt=""><figcaption><p>Sumber gambar : dokumen bootcamp PT Phincon</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/uint.png" alt=""><figcaption><p>Sumber gambar : dokumen bootcamp PT Phincon</p></figcaption></figure>

```go
package main

import "fmt"

var num int

func main() {
    if num == 0 {
        fmt.Println("zero value")
    }
    num = -5
    fmt.Println(num)
    
    num2 := uint(num)
    fmt.Println(num2)
}
```

```
zero value
-5
18446744073709551611
```

## Int, Int32 dan Int64

Int dan Int32 atau Int64 bukan tipe data yang sama. Tipe data int bergantung pada memori dari komputer yang digunakan. Tipe data int64 dapat dipilih jika memori bukan masalah utama dalam pengembangan aplikasi. Untuk nilai biner maksimal dari int64 adalah 2 pangkat 63 - 1.

```
0111111111111111111111111111111111111111111111111111111111111111
```

Reference:

{% embed url="https://yourbasic.org/golang/int-vs-int64/" %}

{% embed url="https://stackoverflow.com/questions/6003492/how-big-can-a-64bit-signed-integer-be" %}
