# HTTP Response Writer

Response Writer digunakan untuk mengeluarkan response saat suatu endpoint di hit.

## Contoh _code_ penggunaan response dengan pakcage http

```go
package main

import (
	"fmt"
	"net/http"
)

var Hello http.HandlerFunc = func(w http.ResponseWriter, r *http.Request) {
	w.WriteHeader(http.StatusOK)
	w.Write([]byte("Hello \n"))
	// fmt
	name := "member_01"
	fmt.Fprint(w, "Hello! \n", name)
	fmt.Fprintln(w, "Hello!", name)
	fmt.Fprintf(w, "Hello! %s", name)
}
	
func main() {
	server := http.Server{
		Addr:   "localhost:5000",
		Handler: Hello,
	}

	fmt.Printf("Server running on %s", server.Addr)
	err := server.ListenAndServe()
	if err != nil{
		panic(err.Error())
	}
}
```

<figure><img src="../../.gitbook/assets/Res (3).png" alt=""><figcaption></figcaption></figure>

## Contoh response JSON dengan map

Ada kalanya response yang dibutuhkan dalam bentuk JSON. Berikut contoh _code_ untuk membuat response dalam bentuk JSON.

```go
package main

import (
	"encoding/json"
	"fmt"
	"net/http"
)

var Hello http.HandlerFunc = func(w http.ResponseWriter, r *http.Request) {
	w.WriteHeader(http.StatusOK)
	res := map[string]interface{}{
		"Status": http.StatusOK,
		"Message": http.StatusText(http.StatusOK),
	}
	jsonByte, err := json.Marshal(res)
	if err != nil {
		panic(err)
	}
	w.Write([]byte(jsonByte))
}
	
func main() {
	server := http.Server{
		Addr:   "localhost:5000",
		Handler: Hello,
	}

	fmt.Printf("Server running on %s", server.Addr)
	err := server.ListenAndServe()
	if err != nil{
		panic(err.Error())
	}
}
```

![](<../../.gitbook/assets/image (8).png>)

## Contoh response JSON dengan struct

```go
package main

import (
	"encoding/json"
	"fmt"
	"net/http"
)

type Res struct {
	Status int
	Message string
}
var Hello http.HandlerFunc = func(w http.ResponseWriter, r *http.Request) {
	w.WriteHeader(http.StatusOK)
	res := Res{
		Status: http.StatusOK, 
		Message: http.StatusText(http.StatusOK),
	}

	jsonByte, err := json.Marshal(res)
	if err != nil {
		panic(err)
	}
	w.Write([]byte(jsonByte))
}
	
func main() {
	server := http.Server{
		Addr:   "localhost:5000",
		Handler: Hello,
	}

	fmt.Printf("Server running on %s", server.Addr)
	err := server.ListenAndServe()
	if err != nil{
		panic(err.Error())
	}
}
```

<figure><img src="../../.gitbook/assets/Struct Map (1).png" alt=""><figcaption></figcaption></figure>
