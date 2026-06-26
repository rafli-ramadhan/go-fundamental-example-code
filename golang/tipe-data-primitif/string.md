# String

Tipe data string digunakan untuk menyimpan value berupa karakter. Default value dari tipe data string adalah karakter kosong atau "".

## Contoh code

```go
package main

import "fmt"

var str string

func main() {
    if str == "" {
        fmt.Println("it is an empty string")
    }
    str = "test"
    fmt.Println(str)
}
```

```
it is an empty string
test
```

## String dan Byte

Di golang string disimpan dalam bentul slice dengan tipe data byte. Untuk menampilkan setiap nilai byte pada 1 karakter di dalam string dapat menggunakan _code_ berikut.

```go
package main

import "fmt"

var sample string = "please"

func main() {
    for i := 0; i < len(sample); i++ {
        fmt.Printf("%x ", sample[i])
    }
}
```

```
70 6c 65 61 73 65 
```
