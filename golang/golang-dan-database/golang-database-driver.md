# Golang Database Driver

Golang memiliki beberapa driver untuk koneksi database, diantarnya :

### 1. MySQL

Untuk instalasi dan set up bisa klik link berikut.

{% embed url="https://github.com/go-sql-driver/mysql" %}

### 2. PostgreSQL

Untuk instalasi dan set up bisa klik link berikut.

{% embed url="https://github.com/jackc/pgx" %}

## Link code&#x20;

Berikut link code lengkap contoh koneksi database MySQL dan PostgreSQL di Golang.

{% embed url="https://github.com/rafli-ramadhan/contact-go/blob/master/db/client.go" %}

{% embed url="https://github.com/rafli-ramadhan/sales-go/blob/master/db/client.go" %}

## Golang Database Pool

Database pool digunakan untuk management access database di Golang. Di package "database/sql", golang menyediakan 4 parameter management access seperti berikut.

```go
db.SetMaxIdleConns(10)                  // setMaxIdelConns -> pengaturan jumlah koneksi minimal yang dibuat saat aplikasi connect ke database
db.SetMaxOpenConns(50)                  // setMaxOpenConns -> pengaturan jumlah koneksi maksimal dibuat
db.SetConnMaxIdleTime(5 * time.Minute)  // setConnMaxIdleTime -> contoh ada 10 koneksi tidak digunakan selamat durasi waktu tertentu, maka akan di close
db.SetConnMaxLifetime(60 * time.Minute) // setConnMaxLifeTime -> contoh koneksi sudah mencapai waktu tertentu, maka akan di close atau memperbaruhi koneksi yang lama
```

Code lengkap-nya dapat dilihat dibawah ini

{% code title="client.go" %}
```go
package client

import (
	"fmt"
	"log"
	"time"

	"database/sql"
	_ "github.com/go-sql-driver/mysql"
	_ "github.com/jackc/pgx/v5/stdlib"
)

func GetDBConnection(driver string) (db *sql.DB) {
	var connString string
	if driver == "mysql" {
		// "username:password@tcp(host:port)/database_name"
		connString = fmt.Sprintf("%s:%s@tcp(%s:%d)/%v",
			"root", "@Ugm428660", "localhost", 3306, "bootcamp")
	} else if driver == "pgx" {
		// urlExample := "postgres://username:password@localhost:5432/database_name"
		connString = fmt.Sprintf("postgres://%s:%s@%s:%d/%s",
			"postgres", "@Ugm428660", "localhost", 5432, "postgres")
	}

	db, err := sql.Open(driver, connString)
	if err != nil {
		panic(err)
	}
	log.Printf("Running database")

	db.SetMaxIdleConns(2)
	db.SetMaxOpenConns(5)
	db.SetConnMaxIdleTime(10 * time.Minute)
	db.SetConnMaxLifetime(60 * time.Minute)

	return
}
```
{% endcode %}

## Close koneksi database

Jika SetMaxIdleConns dan SetMaxOpenCons diinisiasi value-nya, koneksi perlu segera mungkin di close agar bisa digunakan untuk menjalankan query di function lain.

```go
defer db.Close()
```

Penerapan `db.Close()` dapat dilihat di materi selanjutnya.

Reference:

{% embed url="https://stackoverflow.com/questions/4111594/why-always-close-database-connection" %}
