# Get Query Parameter

Query parameter merupakan data yang disimpan dalam URL yang sifatnya case sensitif (huruf besar kecil berpengaruh). Contohnya seperti URL [http://localhost:5000/?name=andi\&age=21](http://localhost:5000/?name=andi\&age=21\&name=nuh\&age=22) yang terdapat query parameter name dan age yang memiliki value andi dan 21. Untuk memperoleh query parameter di Golang dapat menggunakan method URL.Query().Get() seperti contoh _code_ di bawah ini.

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	mux := http.NewServeMux()

	var handlerMain http.HandlerFunc = func(write http.ResponseWriter, request *http.Request) {
		name := request.URL.Query().Get("name")
		fmt.Fprintf(write, "Name : %s\n", name)

		age := request.URL.Query().Get("age")
		fmt.Fprintf(write, "Age : %s\n", age)
	}
	mux.HandleFunc("/", handlerMain)

	server := http.Server{
		Addr:   "localhost:5000",
		Handler: mux,
	}

	err := server.ListenAndServe()
	if err != nil{
		panic(err.Error())
	}
}
```

Output di web browser saat akses URL [http://localhost:5000/?name=andi\&age=21\&name=nuh\&age=22](http://localhost:5000/?name=andi\&age=21\&name=nuh\&age=22):

```
Name : andi
Age : 21
```

## Query Parameter lebih dari 1 Data untuk Query yang sama

Contoh URL yang digunakan adalah [http://localhost:5000/?name=andi\&age=21\&name=nuh\&age=22](http://localhost:5000/?name=andi\&age=21\&name=nuh\&age=22). Dimana terdapat 2 data untuk query yang sama.

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	mux := http.NewServeMux()

	var handlerMain http.HandlerFunc = func(write http.ResponseWriter, request *http.Request) {
		urlValues := request.URL.Query()
		fmt.Fprintf(write, "Data 1 : %s\n", urlValues["name"])
		fmt.Fprintf(write, "Data 2 : %s\n", urlValues["age"])
	}
	mux.HandleFunc("/", handlerMain)

	server := http.Server{
		Addr:   "localhost:5000",
		Handler: mux,
	}

	err := server.ListenAndServe()
	if err != nil{
		panic(err.Error())
	}
}
```

Output in web browser :

```
Data 1 : [andi nuh]
Data 2 : [21 22]
```
