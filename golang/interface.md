---
coverY: 0
---

# Interface

Interface merupakan suatu tipe data yang berisi kumpulan definisi method (hanya definisi saja) dengan nama tertentu. Untuk default value dari interface adalah nil. Interface syaratnya harus method dan method syaratnya harus ada kepemilikan. Contoh untuk 2 method Greeting _code_ di bawah ini merupakan method milik struct Account dan Customer. Method tersebut dapat ditampung dalam sebuah interface bernama CustomerInterface.

## Contoh code 1

```go
package main

import "fmt"

type CustomerInterface interface {
	Greeting() string
}

type Account struct {
	Name     string
	Password string
}

type Customer struct {
	Name      string
	AccountID int
}

func (a Account) Greeting() string {
	return "Hi " + a.Name
}

func (c Customer) Greeting() string {
	return "Welcome " + c.Name
}

// function untuk menggunakan interface dari method beberapa struct.
func NewUser(customerInterface CustomerInterface) string {
	return customerInterface.Greeting()
}

func main() {
	// variabel yang memiliki method yang sama dengan CustomerInterface
	account1 := Account{
		Name:     "Dana",
		Password: "Test123",
	}
	customer1 := Customer{
		Name:      "Firman",
		AccountID: 1,
	}

	fmt.Println(NewUser(customer1))
	fmt.Println(NewUser(account1))
}

```

```
Welcome Firman
Hi Dana
```

## Contoh code 2

```go
package main

import(
	"fmt"
)

// type declaration
type Value string

func (v Value) Hello() {
	fmt.Println("Hello", v)
}

type Example interface {
	Hello()
}

func main() {
	var string1 Value = "Andi"
	string1.Hello()
	var interface1 Example = string1
	interface1.Hello()

	var string2 Value = "Utsman"
	string2.Hello()
	var interface2 Example = string2
	interface2.Hello()
}
```

```
Hello Andi
Hello Andi
Hello Utsman
Hello Utsman
```

## Kegunaan Interface untuk membuat Mocking

Jika suatu fungsi dari suatu package membutuhkan input bertipe interface, kita dapat membuat mockingan dari method yang ada didalam fungsi tersebut.

Semisal ada go module bernama "go-rest-api" yang di dalamnya terdapat 2 file yaitu repository.go dan handler.go.

{% code title="repository.go" %}
```go
package repository

type repo struct {}

func NewRepository() *repo {
	return &repo{}
}

type Repositorier interface {
	CheckUserByName(username string) (isExist bool, err error) {}
	Create(username string, password string) (err error) {}
}

func (r *random) CheckUserByName(username string) (isExist bool, err error) {}

func (r *random) Create(username string, password string) (err error) {}
```
{% endcode %}

Di package lain semisal handler.go membutuhkan method CheckUserByName dan Create dari package repository. Package tersebut diinputkan melalui fungsi NewHandler dengan parameter repo bertipe interface.

{% code title="handler.go" %}
```go
package handler

import (
	"go-rest-api/repository"
)

type handler struct {
	repo repository.Repositorier
}

func NewHandler(repo repository.Repositorier) *handler {
	return &handler{
		repo: repo,
	}
}

func (h *handler) Example(username, password string) (err error) {
	exist := r.repo.CheckUserByName(id)
	// lanjutan code
	err := r.repo.Create(username, password)
	// lanjutan code
}
```
{% endcode %}

Semisal ingin membuat unit test dari method Example di package handler yang memanggil method CheckUserByName dan Create. Kita perlu membuat mocking repository yang memiliki method mirip package repository menggunakan package testify/mock seperti dibawah ini.

{% code title="repositorymock.go" %}
```go
package repositorymock

import (
	"github.com/stretchr/testify/mock"
)

type RepoMock struct {
	mock.Mock
}

func NewRepoMock() *RepoMock {
	return &RepoMock {}
}


func (r *random) CheckUserByName(username string) (isExist bool, err error) {
	// sebagai indikator parameter input diperoleh
	ret := m.Called(username)
	// get return isExist dari mock dengan type assertion
	isExist= ret.Get(0).(bool)
	if ret.Get(1) != nil {
		// get return error dari mock dengan type assertion
		err = ret.Get(1).(error)
	}
	return
}
func (r *random) Create(username string, password string) (err error) {
	// sebagai indikator parameter input diperoleh
	ret := m.Called(username, password)
	if ret.Get(0) != nil {
		// get return error dari mock dengan type assertion
		err = ret.Get(0).(error)
	}
	return
}
```
{% endcode %}

Mocking-an di atas dapat dijadikan sebagai input di fungsi NewHandler di unit testing seperti code di bawah ini karena fungsi NewHandler menerima input repo dengan tipe interface Repositorier. Interface Repositorier memiliki 2 method yaitu CheckUserByName dan Create. Baik package repository atau repositorymock mempunyai fungsi NewRepository dan NewRepoMock yang mengembalikkan struct yang memiliki 2 method tersebut.

```go
package product

import (
	"testing"
	"go-rest-api/repositorymock"
	"github.com/stretchr/testify/require"
)

func TestExample(t *testing.T) {
	// inputkan repoMock ke NewHandler
	repoMock := repository.NewRepoMock()
	handler := NewHandler(repoMock)
	// panggil fungsi Example dari Handler
	err := handler.Example("member_01", "Test123")
	// jika tidak ada error, maka unit testing PASS
	require.NoError(t, err)
}
```

Referensi:

{% embed url="https://stackoverflow.com/questions/39092925/why-are-interfaces-needed-in-golang" %}
