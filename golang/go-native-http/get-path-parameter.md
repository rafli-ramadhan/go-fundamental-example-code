# Get Path Parameter

Path parameter merupakan data yang disisipkan dalam suatu URL. Path parameter sifatnya tidak bisa kosong seperti query parameter. Contoh URL berikut localhost:5000/test/Dana/21 memiliki path parameter yaitu dana dan 21. Untuk memperoleh path parameter dengan http native bisa menggunakan package strings seperti _code_ di bawah ini.

```go
package main

import (
	"fmt"
	"net/http"
	"strings"
)

func main() {
	mux := http.NewServeMux()

	var handlerMain http.HandlerFunc = func(w http.ResponseWriter, r *http.Request) {
		// string prefix untuk mengembalikan string tanpa prefix
		data := strings.TrimPrefix(r.URL.Path, "/test/")
		// split untuk memisahkan string dengan karakter tertentu
		strSlice := strings.Split(data, "/")
		fmt.Fprintf(w, "Name : %s\n", strSlice[0])
		fmt.Fprintf(w, "Id : %s\n", strSlice[1])
	}
	mux.HandleFunc("/test/", handlerMain)

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

<figure><img src="../../.gitbook/assets/1 (6) (1).png" alt=""><figcaption></figcaption></figure>
