# Request JSON

Untuk memperoleh request JSON bisa memanfaatkan JSON Decoder dan Marshal seperti _code_ berikut.

## Contoh _code_ request JSON dengan map sebagai penampung data

```go
package main

import (
	"encoding/json"
	"fmt"
	"net/http"
)

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/welcome", func(w http.ResponseWriter, r *http.Request) {
		if r.Method == "POST" {
			var req map[string]interface{}
			err := json.NewDecoder(r.Body).Decode(&req)
			if err != nil {
				w.WriteHeader(http.StatusBadRequest)
			}
			jsonByte, err := json.Marshal(req)
			if err != nil {
				w.WriteHeader(http.StatusInternalServerError)
			}
			w.Write(jsonByte)
		}
	})

	server := http.Server{
		Addr: 	"localhost:5000",
		Handler: mux,
	}

	fmt.Println("Server running on", server.Addr)
	err := server.ListenAndServe()
	if err != nil {
		panic(err)
	}
}
```

<figure><img src="../../.gitbook/assets/1 (6).png" alt=""><figcaption></figcaption></figure>

## Contoh request JSON dengan struct sebagai penampung data

```go
package main

import (
	"encoding/json"
	"fmt"
	"net/http"
)

type User struct {
	Username string
	Password string
}

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/welcome", func(w http.ResponseWriter, r *http.Request) {
		if r.Method == "POST" {
			var req User
			err := json.NewDecoder(r.Body).Decode(&req)
			if err != nil {
				w.WriteHeader(http.StatusBadRequest)
			}
			jsonByte, err := json.Marshal(req)
			if err != nil {
				w.WriteHeader(http.StatusInternalServerError)
			}
			w.Write(jsonByte)
		}
	})

	server := http.Server{
		Addr: 	"localhost:5000",
		Handler: mux,
	}

	fmt.Println("Server running on", server.Addr)
	err := server.ListenAndServe()
	if err != nil {
		panic(err)
	}
}
```

<figure><img src="../../.gitbook/assets/Request JSON Struct.png" alt=""><figcaption></figcaption></figure>
