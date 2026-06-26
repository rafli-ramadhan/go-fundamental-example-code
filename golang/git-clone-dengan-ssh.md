# Git Clone dengan SSH

Buka terminal lalu ketik `ssh-keygen -t rsa`, selanjutnya tekan enter sampai key fingerprint berhasil di generate.

<figure><img src="../.gitbook/assets/ssh.png" alt=""><figcaption></figcaption></figure>

Kemudian masuk ke menu Settings di menu bagian kanan bawah.

<figure><img src="../.gitbook/assets/ssh setting.png" alt=""><figcaption></figcaption></figure>

Selanjutnya buka tab SSH and GPG keys, lalu klik New SSH key.

<figure><img src="../.gitbook/assets/ssh new.png" alt=""><figcaption></figcaption></figure>

Tambahkan SSH dengan judul sesuai keinginan dan key finger print dari hasil generate command `ssh-keygen -t rsa`.

<figure><img src="../.gitbook/assets/ssh setting add new key.png" alt=""><figcaption></figcaption></figure>

Kemudian copy command clone dari tab SSH dan paste ke terminal seperti berikut.

<figure><img src="../.gitbook/assets/ssh clone.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/ssh git clone.png" alt=""><figcaption></figcaption></figure>
