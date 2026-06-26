# HTTP Test

HTTP Test digunakan untuk tes response dari suatu URL tanpa harus membuat server atau untuk memperoleh response dari suatu service endpoint.

```go
package main

import (
	"fmt"
	"io"
	"net/http"
	"net/http/httptest"
)

func Test(write http.ResponseWriter, request *http.Request) {
	fmt.Println("Server running")
	fmt.Fprintln(write, "Success")
}

func main() {
	// server
	mux := http.NewServeMux()
	mux.HandleFunc("/test", Test)

	// httptest
	request := httptest.NewRequest("GET", "http://localhost:5000/test", nil)
	recorder := httptest.NewRecorder()

	Test(recorder, request)

	response := recorder.Result()
	body, _ := io.ReadAll(response.Body)

	fmt.Println(response)
	fmt.Println(response.StatusCode)
	fmt.Println(response.Status)
	fmt.Println(string(body))
}
```

```
Server running
&{200 OK 200 HTTP/1.1 1 1 map[Content-Type:[text/plain; charset=utf-8]] {0xc000071080} -1 [] false false map[] <nil> <nil>}
200
200 OK
Success
```

## HTTP Test for > 1 URL

```go
package main

import (
	"fmt"
	"io"
	"net/http"
	"net/http/httptest"
)

func Test(write http.ResponseWriter, request *http.Request) {
	fmt.Println("Server running")
	fmt.Fprintln(write, "Success")
}

func Test2(write http.ResponseWriter, request *http.Request) {
	fmt.Fprintln(write, "Success 2")
}

func main() {
	// server
	mux := http.NewServeMux()
	mux.HandleFunc("/test", Test)
	mux.HandleFunc("/test2", Test2)

	// request & response
	request := httptest.NewRequest("GET", "http://localhost:5000/test", nil)
	recorder := httptest.NewRecorder()

	request2 := httptest.NewRequest("GET", "http://localhost:5000/test2", nil)
	recorder2 := httptest.NewRecorder()

	Test(recorder, request)
	Test2(recorder2, request2)

	// recorder 1
	response := recorder.Result()
	body, _ := io.ReadAll(response.Body)

	fmt.Println(response)
	fmt.Println(response.StatusCode)
	fmt.Println(response.Status)
	fmt.Println(string(body))

	// recorder 2
	response2 := recorder2.Result()
	body2, _ := io.ReadAll(response2.Body)

	fmt.Println(response2)
	fmt.Println(response2.StatusCode)
	fmt.Println(response2.Status)
	fmt.Println(string(body2))
}
```

```
Server running
&{200 OK 200 HTTP/1.1 1 1 map[Content-Type:[text/plain; charset=utf-8]] {0xc0000c1110} -1 [] false false map[] <nil> <nil>}
200
200 OK
Success

&{200 OK 200 HTTP/1.1 1 1 map[Content-Type:[text/plain; charset=utf-8]] {0xc0000c11a0} -1 [] false false map[] <nil> <nil>}
200
200 OK
Success 2
```
