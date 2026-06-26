# Hit Endpoint dengan Curl di Terminal

## HTTP Get Method:

```bash
curl -X GET http://localhost:5000
```

## HTTP Post Method:

<pre class="language-bash"><code class="lang-bash"><strong>curl -X POST -d "first_name=Umar&#x26;last_name=Bawazir&#x26;age=20" http://localhost:5000/post
</strong>Hello Umar Bawazir. Iam 20 years old.
</code></pre>

## Contoh _code_

```go
package main

import (
	"fmt"
	"net/http"
)

func HandlerGet(write http.ResponseWriter, request *http.Request) {
	fmt.Println("Success", http.StatusOK)
	fmt.Println("Success")
	fmt.Fprintf(write, "Success")
}

func HandlerFormPost(write http.ResponseWriter, request *http.Request) {
	err := request.ParseForm()
	if err != nil {
		panic(err)
	}

	firstName := request.PostForm.Get("first_name")
	lastName := request.PostForm.Get("last_name")
	age := request.PostForm.Get("age")
	fmt.Println("Success", http.StatusOK)
	fmt.Printf("Hello %s %s and I am %s years old", firstName, lastName, age)
	fmt.Fprintf(write, "Hello %s %s and I am %s years old", firstName, lastName, age)
}

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/", HandlerGet)
	mux.HandleFunc("/t", HandlerFormPost)

	server := http.Server{
		Addr:   "localhost:5000",
		Handler: mux,
	}

	err := server.ListenAndServe()
	if err != nil{
		panic(err.Error())
	}

	fmt.Println("Server running")
}
```

Jalankan dengan go run main.go, kemudian buka terminal (CMD/bash/powershell) dan coba _copy command_ berikut.

## HTTP Get Method

CMD 1 (Request)

```bash
D:\go-server>curl -X GET http://localhost:5000
Success
```

CMD 2 (Response)

```bash
D:\go-server>go run main.go
Success
```

## HTTP Post Method

CMD 1 (Request)

```bash
D:\go-server>curl -X POST -d "first_name=Utsman,last_name=Bey,age=20" http://localhost:5000/t
Hello Utsman,last_name=Bey,age=20  and I am  years old
```

CMD 1 (Response)

```
D:\go-server>go run main.go
Hello Utsman,last_name=Bey,age=20  and I am  years old
```

## Reference

{% embed url="https://superuser.com/questions/149329/how-do-i-make-a-post-request-using-curl" %}
