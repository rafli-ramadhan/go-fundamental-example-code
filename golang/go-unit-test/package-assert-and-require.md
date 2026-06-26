# Package Assert & Require

Package **assert** dan **require** merupakan package bawaan dari github.com/stretchr/testify yang memiliki beberapa fungsi yang dapat digunakan untuk pengecekan expected result dan real result dari suatu fungsi yang di test. Untuk instalasi package testify tertera pada link berikut [https://github.com/stretchr/testify](https://github.com/stretchr/testify) atau bisa menggunakan command berikut.

```
go get github.com/stretchr/testify
```

Pada setiap akhir fungsi di package assert akan memanggil method Fail() dari package testing, artinya eksekusi unit test akan tetap dilanjutkan meskipun suatu unit testing dianggap gagal.&#x20;

Pada setiap akhir fungsi di package require akan memanggil method FailNow() dari package testing, artinya eksekusi unit test tidak akan dilanjutkan saat suatu unit testing telah gagal.

## Contoh code penggunaan fungsi Equal() dari package assertion dan require di unit testing

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
	return "Hello " + name
}

```
{% endcode %}

{% code title="main_test.go" %}
```go
package main

import (
	"testing"
	"github.com/stretchr/testify/assert"
)

func TestSayHi(t *testing.T) {
	expectedResult := "Hello Andi"
	t.Run("Test-1", func(t *testing.T) {
		result := SayHi("Amar")
		assert.Equal(t, expectedResult, result)
	})
	t.Run("Test-2", func(t *testing.T) {
		result := SayHi("Andi")
		assert.Equal(t, expectedResult, result)
	})
	t.Run("Test-3", func(t *testing.T) {
		result := SayHi("Umar")
		assert.Equal(t, expectedResult, result)
	})
}
```
{% endcode %}

```
PS D:\bootcamp-go\go-unit-test> go test -v -run TestSayHi
=== RUN   TestSayHi
=== RUN   TestSayHi/Test-1
    main_test.go:11:
                Error Trace:    D:/bootcamp-go/go-unit-test/main_test.go:11
                Error:          Not equal:
                                expected: "Hello Andi"
                                actual  : "Hello Amar"

                                Diff:
                                --- Expected
                                +++ Actual
                                @@ -1 +1 @@
                                -Hello Andi
                                +Hello Amar
                Test:           TestSayHi/Test-1
=== RUN   TestSayHi/Test-2
=== RUN   TestSayHi/Test-3
    main_test.go:19:
                Error Trace:    D:/bootcamp-go/go-unit-test/main_test.go:19
                Error:          Not equal:
                                expected: "Hello Andi"
                                actual  : "Hello Umar"

                                Diff:
                                --- Expected
                                +++ Actual
                                @@ -1 +1 @@
                                -Hello Andi
                                +Hello Umar
                Test:           TestSayHi/Test-3
--- FAIL: TestSayHi (0.01s)
    --- FAIL: TestSayHi/Test-1 (0.00s)
    --- PASS: TestSayHi/Test-2 (0.00s)
    --- FAIL: TestSayHi/Test-3 (0.00s)
FAIL
exit status 1
FAIL    unit-testing    0.395s
```

{% code title="" %}
```go
package main

import (
	"testing"
	"github.com/stretchr/testify/require"
)

func TestSayHi(t *testing.T) {
	expectedResult := "Hello Andi"
	t.Run("Test-1", func(t *testing.T) {
		result := SayHi("Amar")
		require.Equal(t, expectedResult, result, "Input Not Andi")
	})
	t.Run("Test-2", func(t *testing.T) {
		result := SayHi("Andi")
		require.Equal(t, expectedResult, result, "Input Andi")
	})
	t.Run("Test-3", func(t *testing.T) {
		result := SayHi("Dawam")
		require.Equal(t, expectedResult, result, "Input Not Andi")
	})
}
```
{% endcode %}

```
PS D:\bootcamp-go\go-unit-test> go test -v -run TestSayHi
=== RUN   TestSayHi
=== RUN   TestSayHi/Test-1
    main_test.go:11:
                Error Trace:    D:/bootcamp-go/go-unit-test/main_test.go:11
                Error:          Not equal:
                                expected: "Hello Andi"
                                actual  : "Hello Amar"

                                Diff:
                                --- Expected
                                +++ Actual
                                @@ -1 +1 @@
                                -Hello Andi
                                +Hello Amar
                Test:           TestSayHi/Test-1
                Messages:       Input Not Andi
=== RUN   TestSayHi/Test-2
=== RUN   TestSayHi/Test-3
    main_test.go:19:
                Error Trace:    D:/bootcamp-go/go-unit-test/main_test.go:19
                Error:          Not equal:
                                expected: "Hello Andi"
                                actual  : "Hello Umar"

                                Diff:
                                --- Expected
                                +++ Actual
                                @@ -1 +1 @@
                                -Hello Andi
                                +Hello Umar
                Test:           TestSayHi/Test-3
                Messages:       Input Not Andi
--- FAIL: TestSayHi (0.01s)
    --- FAIL: TestSayHi/Test-1 (0.00s)
    --- PASS: TestSayHi/Test-2 (0.00s)
    --- FAIL: TestSayHi/Test-3 (0.01s)
FAIL
exit status 1
FAIL    unit-testing    0.499s
```
