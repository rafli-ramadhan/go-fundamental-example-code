# HTTP Server dengan Serve Mux

HTTP server juga bisa dibuat dengan menggunakan serve mux. Untuk menggunakan serve mux perlu keyword NewServeMux. New di awal keyword tersebut untuk mengembalikan struct serve mux yang sifatnya masih private (tidak bisa diakses di luar package) di dalam package net/http.

## Contoh _code_ HTTP server mux dengan handler

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

type WorldHandler struct{}

func (h *WorldHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "World!")
}

func main() {
	var hello http.Handler = &HelloHandler{}
	var world http.Handler = &WorldHandler{}

	mux := http.NewServeMux()
	mux.Handle("/hello", hello)
	mux.Handle("/world", world)

	server := http.Server{
		Addr:    "localhost:5000",
		Handler: mux,
	}
	fmt.Printf("Server running on %s", server.Addr)
	err := server.ListenAndServe()
	if err != nil {
		panic(err.Error())
	}
}
```

## Contoh _code_ HTTP server mux dengan handler func

```go
package main

import (
	"fmt"
	"net/http"
)

func Hello(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello!")
}

func World(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "World!")
}

func main() {
	var hello http.HandlerFunc = Hello
	var world http.HandlerFunc = World

	mux := http.NewServeMux()
	mux.HandleFunc("/hello", hello)
	mux.HandleFunc("/world", world)

	server := http.Server{
		Addr:    "localhost:5000",
		Handler: mux,
	}
	fmt.Printf("Server running on %s", server.Addr)
	err := server.ListenAndServe()
	if err != nil {
		panic(err.Error())
	}
}
```
