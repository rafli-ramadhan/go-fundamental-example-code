# Table Test

Kita juga dapat menggunakan tabel test untuk membuat unit testing di Golang. Perbedaannya dengan code test sebelumnya adalah, di tabel test kita akan memanfaatkan looping. Setiap data untuk input fungsi / method, hasil yang diharapkan dan sebagainya ditampung dalam sebuah struct. Kemudian looping digunakan untuk menjalankan setiap unit test seperti contoh code berikut.

## Contoh code

{% code title="main.go" %}
```go
package main

import (
	"fmt"
)

func main() {
	result := SayHi("Utsman")
	fmt.Println(result)
}

func SayHi(name string) string {
	return name
}

```
{% endcode %}

{% code title="main_test.go" %}
```go
package main

import (
	"testing"
)

type TestTable struct {
	input		 string
	expected 	 bool
	subtestName  string
	errorMessage string
}

func TestSayHi2(t *testing.T) {
	var tableTest []TestTable = []TestTable{
		{
			input: "Andi",
			expected: true,
			subtestName: "Test-1",
			errorMessage: "Is Andi",
		},
		{
			input: "Umar",
			expected: false,
			subtestName: "Test-2",
			errorMessage: "Is Not Andi",
		},
		{
			input: "Utsman",
			expected: false,
			subtestName: "Test-3",
			errorMessage: "Is Not Andi",
		},
	}

	for _, v := range tableTest {
		t.Run(v.subtestName, func(t *testing.T) {
			if result := SayHi(v.input); result != "Andi" {
				t.Error("Not Andi")
			}
		})
	}
}
```
{% endcode %}

```
PS D:\bootcamp-go\go-unit-test> go test -v -run TestSayHi2
=== RUN   TestSayHi2
=== RUN   TestSayHi2/Test-1
=== RUN   TestSayHi2/Test-2
    main_test.go:40: Not Andi
=== RUN   TestSayHi2/Test-3
    main_test.go:40: Not Andi
--- FAIL: TestSayHi2 (0.00s)
    --- PASS: TestSayHi2/Test-1 (0.00s)
    --- FAIL: TestSayHi2/Test-2 (0.00s)
    --- FAIL: TestSayHi2/Test-3 (0.00s)
FAIL
exit status 1
FAIL    unit-testing    0.384s
```
