# HTTP Server

Berikut _code_ untuk membuat HTTP server dengan native golang (tanpa framework).

## Server dengan http.Handler

```go
package main

import (
	"fmt"
	"net/http"
)

type HelloHandler struct{}

func (h *HelloHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello!")
}

func main() {
	handler := &HelloHandler
	server := http.Server{
		Addr:   "localhost:5000",
		Handler: handler,
	}

	fmt.Printf("Server running on %s", server.Addr)
	err := server.ListenAndServe()
	if err != nil{
		panic(err.Error())
	}
}
```

## Server dengan http.HandlerFunc

```go
package main

import (
	"fmt"
	"net/http"
)

var HelloHandler http.HandlerFunc = func(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello!")
}
	
func main() {
    	handler := &HelloHandler
	server := http.Server{
		Addr:   "localhost:5000",
		Handler: handler,
	}

	fmt.Printf("Server running on %s", server.Addr)
	err := server.ListenAndServe()
	if err != nil{
		panic(err.Error())
	}
}
```

Open localhost:5000

{% embed url="https://pkg.go.dev/net/http#Server.Handler" %}
