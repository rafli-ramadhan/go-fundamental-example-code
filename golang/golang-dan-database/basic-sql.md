---
description: Create Table, Alter Table, Select, Insert, Update, Delete dan SQL Injection
---

# Basic SQL

## Create Table

Contoh SQL untuk membuat tabel baru bernama pelanggan dan comments di MySQL:

```sql
create table pelanggan (
	id int not null auto_increment,
	name varchar(100) not null,
	no_telp varchar(100) not null,
	created_at datetime,
	updated_at datetime,
	deleted_at datetime,
	primary key (id)
)
```

Sementara itu PostgreSQL memiliki SQL yang sedikit berbeda seperti di bawah ini :

```sql
create table pelanggan (
	id serial not null,
	name varchar(100) not null,
	pelanggan varchar(100) not null,
	created_at timestamp,
	updated_at timestamp,
	deleted_at timestamp,
	primary key (id)
)
```

## Alter

Contoh alter untuk menambah kolom :

```sql
alter table pelanggan 
add no_telp varchar(100) not null
```

Contoh alter untuk modifikasi kolom :

```sql
alter table pelanggan 
modify column id int not null auto_increment;
```

Contoh alter untuk menambahkan kolom foreign key bernama id\_2 di tabel\_A yang nilainya dari kolom id di tabel\_B :

```sql
alter table table_A
add constaint table_B
foregn key id_2 references table_B(id)
```

## Select

Asumsikan tabel pelanggan telah memiliki data sebagai berikut :

<figure><img src="../../.gitbook/assets/table.png" alt=""><figcaption></figcaption></figure>

Untuk mendapatkan data kolom id, name dan no\_telp dari tabel pelanggan dapat menggunakan query berikut :

```sql
select id, name, no_telp from pelanggan
```

## Select Distinct

Untuk mendapatkan data-data yang tidak duplikat dari kolom name tabel pelanggan dapat menggunakan query berikut :

```sql
select distinct name from pelanggan;
```

Untuk mendapatkan data-data yang tidak duplikat dari kolom name dan no\_telp tabel pelanggan dapat menggunakan query berikut :

```sql
select distinct name, no_telp from pelanggan;
```

Perlu di ingat, jika misal di kolom name terdapat 20 data distinct (data tidak duplikat) dan kolom no\_telp terdapat 30 data distinct. Maka jumlah data yang terpilih akan menjadi 30, menyesuaikan kolom dengan jumlah data distinct terbanyak.&#x20;

## Insert

Untuk insert data baru ke tabel pelanggan dapat menggunakan query berikut :

```sql
insert into pelanggan (name, no_telp) values ("andi", "088227867533")
```

## Update

Untuk update data dari tabel pelanggan dapat menggunakan query berikut :

```sql
update pelanggan SET name = "umar" , no_telp = "089932943287" where id = 1
```

## Delete

Untuk menghapus data 1 baris dari tabel pelanggan dapat menggunakan query berikut :

```sql
delete FROM contact where id = 1
```

Reference :

{% embed url="https://www.w3schools.com/SQL" %}

{% embed url="https://www.w3schools.com/Sql/trysql.asp?filename=trysql_select_no_distinct" %}
