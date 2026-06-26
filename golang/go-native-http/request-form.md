# Request Form

Saat kita belajar HTML, kita tahu bahwa saat kita membuat form, kita bisa submit datanya dengan method GET atau POST. Jika menggunakan method GET, semua data di form dapat menjadi query parameter. Sedangkan jika menggunakan POST, semua data di form akan dikirim via body HTTP request. Di Golang, submit data form dapat dilakukan dengan ParseForm yang mengambil (parses) query mentah dari URL seperti request dari CURL.

```go
r.PostForm.Get()
```

## Contoh _code_ request form

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
			if err := r.ParseForm(); err != nil {
				panic(err)
			}

			username := r.PostForm.Get("username")
			password := r.PostForm.Get("password")
			
			res := map[string]interface{}{
				"username": username,
				"password": password,
			}
			jsonByte, err := json.Marshal(res)
			if err != nil {
				w.WriteHeader(http.StatusInternalServerError)
			}
			w.Write(jsonByte)
		}
	})

	server := http.Server{
		Addr:    "localhost:5000",
		Handler: mux,
	}

	fmt.Println("Server running on", server.Addr)
	err := server.ListenAndServe()
	if err != nil {
		panic(err)
	}
}
```

<figure><img src="../../.gitbook/assets/Request JSON Struct (2).png" alt=""><figcaption></figcaption></figure>

## Contoh _code_ request form dengan http test

```go
package main

import (
	"fmt"
	"io"
	"net/http"
	"net/http/httptest"
	"strings"
)

func FormPost(write http.ResponseWriter, request *http.Request) {
	err := request.ParseForm()
	if err != nil {
		panic(err)
	}

	firstName := request.PostForm.Get("first_name")
	lastName := request.PostForm.Get("last_name")
	age := request.PostForm.Get("age")
	
	fmt.Fprintf(write, "Hello %s %s and I am %s years old", firstName, lastName, age)
}

func main() {
	requestBody := strings.NewReader("first_name=Utsman&last_name=Bey&age=23")
	request := httptest.NewRequest(http.MethodPost, "localhost:5000/", requestBody)
	request.Header.Add("Content-Type", "application/x-www-form-urlencoded")
	recorder := httptest.NewRecorder()
	
	FormPost(recorder, request)
	response := recorder.Result()
	body, _ := io.ReadAll(response.Body)
	fmt.Println(string(body))
}
```

```
Hello Utsman Bey and I am 23 years old
```
