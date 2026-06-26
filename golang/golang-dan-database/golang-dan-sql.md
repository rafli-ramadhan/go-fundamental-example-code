# Golang dan SQL

## SQL Query di Golang dengan Query Parameter

Tujuan adanya query parameter adalah untuk menghindari SQL injection. Jika menggunakan MySQL, query parameter dapat disisipkan di query dengan tanda ?. Lalu value di query dapat di input melalui fungsi ExecContext() untuk query Insert, Update dan Delete atau fungsi QueryContext() untuk query Get seperti code di bawah ini.

```sql
insert into comments (email, comment) value (?,?)
```

```sql
update contact SET name = ?, no_telp = ? where id = ?
```

```sql
delete FROM contact where id = ?
```

Jika menggunakan pgx (driver golang PostgreSQL), query parameter disisipkan di query dengan tanda $1, $2 dan seterusnya sesuai urutan  parameter.

```sql
insert into comments (email, comment) value ($1,$2)
```

```sql
update contact SET name = $1, no_telp = $2 where id = $3
```

```sql
delete FROM contact where id = $1
```

## Prepare Statement

Prepare statement digunakan untuk memastikan query yang di eksekusi berada dalam 1 koneksi database yang sama.

## Database Transaction

Database transaction digunakan supaya SQL yang dikirim tidak langsung di commit ke database. Implementasi database transaction semisal jika kita ingin melakukan insert beberapa database, lalu ada 1 data yang gagal di create. Maka kita bisa menggunakan database transaction untuk me-rollback atau membatalkan create seluruh data yang telah di insert ke database. Database transaction di awali dengan inisiasi berikut.

```go
trx, err := db.BeginTx(ctx, nil)
if err != nil {
	panic(err) // bisa diganti dengan fmt atau log
}
```

Query dapat di commit dengan _code_ berikut.

```go
trx.Commit()
```

Namun, ada kalanya ingin dilakukan pengecekan untuk menghindari error. Jika error terjadi dapat di atasi dengan _code_ berikut.

```go
if err != nil {
    trx.Rollbacck()
}
```

## Implementasi Query Parameter, Prepare Statement dan Database Transaction pada Insert Data ke Database

Catatan : untuk query get seluruh data, update dan delete 1 data tidak memerlukan prepare statement ataupun database transaction.

{% code title=" main.go" %}
```go
package main

import (
	"context"
	"fmt"
	"log"
	"time"

	"database/sql"
	_ "github.com/go-sql-driver/mysql"
	_ "github.com/jackc/pgx/v5/stdlib"
)

var listItem = map[string]float64{
	"item1": 40000,
	"item2": 30000,
	"item3": 50000,
}

func main() {
	db := GetDBConnection("pgx")
	InsertPostgreSQL(db)
}

func GetDBConnection(driver string) (db *sql.DB) {
	var connString string
	if driver == "mysql" {
		// "username:password@tcp(host:port)/database_name"
		connString = fmt.Sprintf("%s:%s@tcp(%s:%d)/%v",
			"root", "@Ugm428660", "localhost", 3306, "bootcamp")
	} else if driver == "pgx" {
		// "postgres://username:password@localhost:5432/database_name"
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

func InsertPostgreSQL(db *sql.DB) {
	ctx, cancel := context.WithTimeout(context.Background(), 3*time.Second)
	defer cancel()

	// query parameter -> to prevent SQL Injection
	query := `insert into product (name, price) values ($1, $2)`
	// database transaction
	trx, err := db.Begin()
	if err != nil {
		panic(err)
	}
	
	// prepare statement 
	preparestmt, err := trx.PrepareContext(ctx, query)
	if err != nil {
		panic(err)
	}

	for i, v := range listItem {
		res, err := preparestmt.ExecContext(ctx, i, v)
		if err != nil {
			trx.Rollback()
			panic(err)
		}

		// LastInsertId is not supported by this driver
		lastInsertedID, err := res.LastInsertId()
		rowAffected, _ := res.RowsAffected()
		fmt.Printf("(%d, %d)", lastInsertedID, rowAffected)
	}
	trx.Commit()

	defer db.Close()
}
```
{% endcode %}

## Link Code

Berikut contoh code penerapan query parameter, prepare statement dan database transaction di Golang.

{% embed url="https://github.com/rafli-ramadhan/contact-go/blob/master/repository/contact_http_db_impl.go" %}

{% embed url="https://github.com/rafli-ramadhan/sales-go/tree/master/repository" %}
