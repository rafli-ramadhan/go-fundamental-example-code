---
coverY: 0
---

# Command di Golang

## Inisiasi Go Module

Inisiasi go module :

```
go mod init nama_project
```

Buat file main.go dengan package main seperti contoh di bawah ini, kemudian lakukan running dengan command running go module. Sebagai catatan function main harus selalu berada di package main.

```go
package main

import (
	"fmt"
)

func main() {
	fmt.Println("Hello World")
}

```

## Running Go Module

```
go run main.go
```

atau

```
go run .
```

Perbedaan go run . akan mencari function main di package main di folder tempat command di atas dijalankan.

## Build Go Module

```
go build main.go
```

Untuk Windows OS, go build akan menghasilkan file ber-ekstensi .exe yang bisa dijalankan dengan command berikut.

```
start nama_file_exe
```

## Download Module

```
go mod tidy
```

Kegunaan `go mod tidy` :

* Untuk memastikan modul yang ada di go.mod sesuai dengan yang dibutuhkan di semua file dalam modul.
* Untuk menambahkan modul yang dibutuhkan tapi belum ada di go.mod.

## Go Get vs Go Install

Go get dan go install sama-sama digunakan untuk mengunduh suatu module dari github. Informasi detail dapat diakses di link berikut [https://go.dev/ref/mod#go-install](https://go.dev/ref/mod#go-install).

Reference:

{% embed url="https://stackoverflow.com/questions/66356034/what-is-the-difference-between-go-get-command-and-go-mod-download-command" %}
