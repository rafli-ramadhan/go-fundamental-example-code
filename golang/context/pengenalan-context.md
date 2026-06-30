# Pengenalan Context

Context merupakan sebuah data yang membawa value, sinyal cancel, sinyal timeout dan sinyal deadline. Context biasanya dibuat per request (misal setiap ada request masuk ke server web melalui http request). Context digunakan untuk mempermudah kita meneruskan value, dan sinyal antar proses. Dengan menggunakan context, ketika kita ingin membatalkan semua proses, kita cukup mengirim sinyal ke context, maka secara otomatis semua proses akan dibatalkan. Context dapat digunakan untuk koneksi database, http server, http client, dan lain-lain.
