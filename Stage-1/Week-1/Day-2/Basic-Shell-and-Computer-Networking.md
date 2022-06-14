## Basic Shell and Computer Networking

![Img 1](assets/1.png)

Jaringan Komputer adalah dua atau lebih perangkat komputer yang saling terhubung atau terkoneksi antara satu dengan yang lain

Kembali lagi bersama saya Alfino Dwi Nugroho pada kali ini saya akan memberikan tutorial atau cara dari task tentang “Basic Shell and Computer networking”.

Baca juga
[Tutorial Install Ubuntu Server 20.04 LTS Menggunakan VirtualBox](https://github.com/pinoezz/DevOps/blob/main/stage1/Week-1/Day1/Instalasi-Ubuntu-Server.md)

# Sebelum memulai task kali ini saya akan memberitahu secara singkat perintah perintah dasar pada CLI linux :

# sudo
sudo merupakan singkatan dari “SuperUser Do” dan berfungsi untuk menjalankan task yang memerlukan hak akses (permission) administrative atau root

Contoh penggunaanya adalah sudo apt update; sudo apt upgrade berfungsi untuk meng-update serta meng-upgrade sistem kita agar tetap up to date

```
sudo apt update; sudo apt upgrade
```

![Img 1](assets/2.png)

# mkdir​
mkdir adalah perintah untuk membuat suatu directory. Sebagai contoh coba kalian buat directory dengan nama pino.

```
mkdir
```

![Img 1](assets/3.png)

# ls
ls adalah perintah untuk melihat list apa saja yang ada di directory.

```
ls
```

![Img 1](assets/4.png)

# cd
cd adalah perintah untuk masuk ke dalam directory.

```
cd
```

![Img 1](assets/5.png)

# ls -la​

ls -la adalah perintah untuk melihat semua list file dan directory yang ada serta menampilkan semua file maupun directory yang tersembunyi.

```
ls -la
```

![Img 1](assets/6.png)

# cd ..​
cd .. adalah perintah untuk keluar dari directory.

```
cd ..
```

![Img 1](assets/7.png)

# touch​
touch adalah perintah untuk membuat suatu file. Sebagai contoh coba kalian buat suatu file dengan nama index.html.

```
touch index.html
```

![Img 1](assets/8.png)

# cp​

cp adalah perintah untuk meng-copy file serta mengubahnya dengan nama yang kalian inginkan. sebagai contoh coba kalian copy file index.html yang sudah kalian buat tadi lalu ubah dengan nama file index.

```
cp index.html index
```


![Img 1](assets/9.png)

# mv​
mv adalah sebuah perintah untuk me-rename nama file, tetapi juga dapat digunakan untuk memindahkan suatu file ke directory tertentu. Sebagai contoh coba kalian ubah nama file index tadi dengan nama index.js lalu buat sebuah directory baru lalu pindahkan file index.js tadi ke directory yang sudah kalian buat.

```
mv index index.js
```

![Img 1](assets/10.png)

![Img 1](assets/11.png)

Berikut adalah beberapa command pada linux, untuk lengkapnya kalian bisa cek di sini : 
[Basic Linux](https://bit.ly/3wTzrlL)

# Mengubah IP Server

![Img 1](assets/12.png)

Ip yang saya gunakan sebelumnya adalah 192.168.100.10 , saya akan mengubahnya menjadi 192.168.100.20

```
sudo nano /etc/netplan/00-installer-config.yaml
```

![Img 1](assets/13.png)

Kemudian silahkan kalian masukan password root

![Img 1](assets/14.png)

Selanjutnya tampilan akan berubah menjadi text editor pada addresses enp0s3 saya akan ubah menjadi 192.168.100.20/24

![Img 1](assets/15.png)

Kemudian untuk save dan exit kalian tekan ctrl+o (write out)lalu enter kemudian ctrl + x untuk exit

Selanjutnya untuk mengkonfirmasi customisasi IP yang sudah kalian buat tadi kalian bisa menggunakan perintah dibawah

```
sudo netplan apply
```

![Img 1](assets/16.png)

Selanjutnya untuk mengecek apakah ip kalian sudah berubah dengan mengetikan cat /etc/netplan/00-installer-config.yaml


```
cat /etc/netplan/00-installer-config.yaml
```

![Img 1](assets/17.png)

Untuk memastikan lagi kalian bisa cek ip dengan megetikan ip a

```
ip a
```

![Img 1](assets/18.png)

# Install Web Server Apache2 secara manual

# Apa itu Localtunnel?​

Localtunnel adalah sebuah tools yang memungkinkan kita untuk berbagi layanan website dari lokal komputer ke publik dengan url akses yang disediakan oleh localtunnel.

berikut adalah langkah langkah instalasi Apache2 secara manual

Sebelum di mulai saya akan meremote server yang baru di ubah ipnya terlebih dahulu

```
ssh pino@192.168.100.20
```

![Img 1](assets/19.png)

Apabila tampilan sudah seperti ini artinya kalian sudah berhail remote server

Selanjutnya untuk menginstall Apache2 kalian bisa gunakan command di bawah ini

```
sudo apt install apache2
```

![Img 1](assets/20.png)

Ketikan “y” lalu “enter

![Img 1](assets/21.png)

Prosess penginstallan Apache2

Apabila proses penginstalan sudah selesai kalian bisa mengcek status Apache2 dengan command di bawah ini

```
sudo systemctl status apache2
```

![Img 1](assets/22.png)

Langkah selanjutnya kita coba cek melalui browser dengan mengetikan ip server

![Img 1](assets/23.png)

Jika tampilan seperti di atas artinya Instalasi Apache2 berhasil

# Membuat localtunnel pada web server apache2

Kita akan mencoba untuk menjalankan localtunnel agar server local kita dapat di akses secara publik. Berikut adalah step by step cara menggunakannya:

Pertama-tama yang kita lakukan adalah instalalsi node.js menggunakan nvm untuk melakukan instalasi kalian dapat mengikuti langkah-langkah dibawah ini.

```
sudo apt install curl
```

![Img 1](assets/24.png)

Selanjutnya ketik "y" lalu "Enter"

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

![Img 1](assets/25.png)

```
exec bash
```

```
nvm install 14
```

```
node -v
```

![Img 1](assets/27.png)

Selanjutnya kita akan melakukan instalasi localtunnel menggunakan npm yang sudah kita install.

```
npm install -g localtunnel
```

![Img 1](assets/28.png)


Sekarang kita coba untuk menggunakan localtunel untuk aplikasi Apache2 yang sudah kita install.

Untuk menjalankan localtunel kalian dapat mengikuti perintah di bawah ini.

```
lt — port 80
```

![Img 1](assets/29.png)

Kemudian salin URL lalu paste kan pada browser kalian

![Img 1](assets/30.png)

Klik tombol “Click to Continue”

Selanjutnya kalian akan di arahkan ke aplikasi kalian. Dan aplikasi kalian sekarang sudah dapat di akses oleh public.

![Img 1](assets/31.png)

Apabila tampilan seperti ini artinya local host kalian berhasil di install

Saya akan melakukan testing untuk mengakses Local Host Apache2 menggunakan smartphone.

![Img 1](assets/32.png)

Tampilan di smartphone
