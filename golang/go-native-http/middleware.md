# Middleware

Untuk membuat middleware dengan golang native bisa dengan menggunakan http.Handler seperti _code_ di bawah ini.

```go
package main

import (
	"fmt"
	"log"
	"net/http"
)

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintln(w, "Test middleware")
	})

	middleware := &Middleware{}
	middleware.Handler = mux
	middleware.Use(Middleware1, Middleware2, Middleware3)

	server := http.Server{
		Addr:    "localhost:5000",
		Handler: middleware,
	}

	fmt.Println("Server running")
	err := server.ListenAndServe()
	if err != nil {
		panic(err)
	}
}

type MiddlewareFunc func(http.ResponseWriter, *http.Request, http.Handler) http.Handler

type Middleware struct {
	Handler     http.Handler
	Middlewares []MiddlewareFunc
}

func (m *Middleware) Use(middlewares ...MiddlewareFunc) {
	m.Middlewares = append(m.Middlewares, middlewares...)
}

func (m *Middleware) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	handler := m.Handler

	// handler = Middleware3(w, r, Middleware2(w, r, Middleware1(w, r, mux)))
	for _, middleware := range m.Middlewares {
		handler = middleware(w, r, handler)
	}

	handler.ServeHTTP(w, r)
}

// Middleware 1
func Middleware1(w http.ResponseWriter, r *http.Request, next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		log.Println("Middleware 1: Before request")
		next.ServeHTTP(w, r)
		log.Println("Middleware 1: After request")
	})
}

// Middleware 2
func Middleware2(w http.ResponseWriter, r *http.Request, next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		log.Println("Middleware 2: Before request")
		next.ServeHTTP(w, r)
		log.Println("Middleware 2: After request")
	})
}

// Middleware 3
func Middleware3(w http.ResponseWriter, r *http.Request, next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		log.Println("Middleware 3: Before request")
		next.ServeHTTP(w, r)
		log.Println("Middleware 3: After request")
		log.Println("")
	})
}

```

<figure><img src="../../.gitbook/assets/1 (2).png" alt=""><figcaption></figcaption></figure>

```
PS D:\bootcamp-go\go-middleware> go run main.go
Server running
2023/05/20 22:13:12 Middleware 3: Before request
2023/05/20 22:13:12 Middleware 2: Before request
2023/05/20 22:13:12 Middleware 1: Before request
2023/05/20 22:13:12 Middleware 1: After request 
2023/05/20 22:13:12 Middleware 2: After request 
2023/05/20 22:13:12 Middleware 3: After request 
```
