# Method di Package Testing

Package testing golang memiliki beberapa method bawaan untuk keperluan testing seperti t.Fail, t.FailNow, t.Error & t.Fatal, t.Skip. Penjelasan masing-masing method dirinci sebagai berikut:

* t.Fail() digunakan untuk menggagalkan unit test, namun tetap melanjutkan eksekusi unit test. Unit test tersebut dianggap gagal.

```go
func (c *common) Fail() {
	if c.parent != nil {
		c.parent.Fail()
	}
	c.mu.Lock()
	defer c.mu.Unlock()
	// c.done needs to be locked to synchronize checks to c.done in parent tests.
	if c.done {
		panic("Fail in goroutine after " + c.name + " has completed")
	}
	c.failed = true
}
```

* t.FailNow() digunakan untuk menggagalkan unit test saat ini juga, tanpa melanjutkan eksekusi unit test selanjutnya.

```go
func (c *common) FailNow() {
	c.checkFuzzFn("FailNow")
	c.Fail()

	// ...
	c.mu.Lock()
	c.finished = true
	c.mu.Unlock()
	runtime.Goexit()
}
```

* t.Error() digunakan untuk menampilkan error dengan log dan memanggil function Fail(), sehingga eksekusi unit test akan tetap berjalan sampai selesai meskipun unit test saat ini telah gagal.

```go
func (c *common) Error(args ...any) {
	c.checkFuzzFn("Error")
	c.log(fmt.Sprintln(args...))
	c.Fail()
}
```

* t.Fatal() mirip dengan Error() namun diakhiri dengan FailNow(), sehingga mengakibatkan eksekusi unit test berhenti.

```go
func (c *common) Fatal(args ...any) {
	c.checkFuzzFn("Fatal")
	c.log(fmt.Sprintln(args...))
	c.FailNow()
}
```

* t.Skip() digunakan untuk skip suatu unit test dan menampilkan suatu argument dengan log.

```go
func (c *common) Skip(args ...any) {
	c.checkFuzzFn("Skip")
	c.log(fmt.Sprintln(args...))
	c.SkipNow()
}
```

* t.SkipNow digunakan untuk skip suatu unit test dan exit.

```go
func (c *common) SkipNow() {
	c.checkFuzzFn("SkipNow")
	c.mu.Lock()
	c.skipped = true
	c.finished = true
	c.mu.Unlock()
	runtime.Goexit()
}
```

## Contoh code

Berikut adalah code function SayHi pada package main yang ingin dibuat unit test-nya.

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

## Implementasi method Error

Berikut contoh code unit testing yang menerapkan method error.

{% code title="main_test.go" %}
```go
package main

import (
	"fmt"
	"testing"
	// "github.com/stretchr/testify/assert"
)

func TestSayHi(t *testing.T) {
	t.Run("Test-1", func(t *testing.T) {
		result := SayHi("Amar")
		if result != "Andi" {
			t.Error("Not Andi")
		}
		fmt.Println("Next")
		result = SayHi("Andi")
		if result != "Andi" {
			t.Error("Andi")
		}
	})
}

```
{% endcode %}

```
PS D:\bootcamp-go\go-unit-test> go test -v -run TestSayHi
=== RUN   TestSayHi
=== RUN   TestSayHi/Test-1
    main_test.go:13: Not Andi
Next
    main_test.go:18: Andi
--- FAIL: TestSayHi (0.00s)
    --- FAIL: TestSayHi/Test-1 (0.00s)
FAIL
exit status 1
FAIL    unit-testing    0.374s
```

## Implementasi method Fatal

Berikut contoh code unit testing yang menerapkan method fatal.

{% code title="main_test.go" %}
```go
package main

import (
	"fmt"
	"testing"
)

func TestSayHi(t *testing.T) {
	t.Run("Test-1", func(t *testing.T) {
		result := SayHi("Amar")
		if result != "Andi" {
			t.Fatal("Not Andi")
		}
		fmt.Println("Next")
		result = SayHi("Andi")
		if result != "Andi" {
			t.Fatal("Andi")
		}
	})
}

```
{% endcode %}

```
PS D:\bootcamp-go\go-unit-test> go test -v -run TestSayHi
=== RUN   TestSayHi
=== RUN   TestSayHi/Test-1
    main_test.go:13: Not Andi
--- FAIL: TestSayHi (0.00s)
    --- FAIL: TestSayHi/Test-1 (0.00s)
FAIL
exit status 1
FAIL    unit-testing    0.316s
```

## Implementasi method Skip

Berikut contoh code unit testing yang menerapkan method skip.

{% code title="main_test.go" %}
```go
package main

import (
	"fmt"
	"testing"
	// "github.com/stretchr/testify/assert"
)

func TestSayHi(t *testing.T) {
	t.Run("Test-1", func(t *testing.T) {
		result := SayHi("Amar")
		if result != "Andi" {
			t.Skip("Not Available")
		}
		fmt.Println("Next")
		result = SayHi("Andi")
		if result != "Andi" {
			t.Error("Andi")
		}
	})
}

```
{% endcode %}

```
PS D:\bootcamp-go\go-unit-test> go test -v -run TestSayHi
=== RUN   TestSayHi
=== RUN   TestSayHi/Test-1
    main_test.go:13: Not Available
--- PASS: TestSayHi (0.00s)
    --- SKIP: TestSayHi/Test-1 (0.00s)
PASS
ok      unit-testing    0.270s
```
