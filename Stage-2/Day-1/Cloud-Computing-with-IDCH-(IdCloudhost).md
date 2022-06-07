# Cloud Computing

![image](https://user-images.githubusercontent.com/106061407/172401166-8b7f9408-f57b-4348-8b6c-fa472156cfb8.png)

Cloud Computing merupakan sebuah teknologi yang menjadikan internet sebagai pusat server untuk mengelola data dan juga aplikasi pengguna. Cloud Computing memudahkan penggunanya untuk menjalankan program tanpa harus menginstall aplikasi terlebih dahulu dan memudahkan pengguna untuk mengakses data dan informasi melalui internet

# Cara Kerja Cloud Computing

Teknologi Cloud Computing ini menjadikan internet sebagai pusat server dalam mengelelola data. Sistem ini memudahkan pengguna untuk login ke internet agar mendapatkan akses untuk menjalankan program atau aplikasi tanpa harus menginstall aplikasi tersebut.

# Membuat Server Gateway dan Aplikasi menggunakan IdCloudhost

![image](https://user-images.githubusercontent.com/106061407/172402771-cd9fbf3b-6ac8-4cc1-855a-854136475b32.png)


PT Cloud Hosting Indonesia (IDCloudHost) Merupakan Salah Satu Web Hosting Provider yang Ada di Indonesia dengan Menawarkan Layanan Seperti Pendaftaran Domain, Cloud Hosting, Server (VPS & Dedicated Server), Reseller Domain & Hosting, dan Beberapa Layanan Lainnya.


Langkah pertama dalam pembuatan server kalian terlebih dahulu harus membuat akun IdCloudhost menggunakan link di bawah ini

[IdCloudhost](https://idcloudhost.com/)

![image](https://user-images.githubusercontent.com/106061407/172403542-cc02edb9-6e32-4277-8dbb-551be5d0d5da.png)

Kemudian kalian bisa login / membuat akun baru IdCloudhost terlebih dahulu

![image](https://user-images.githubusercontent.com/106061407/172403918-4445daa4-6ea8-494b-826f-d95c3d608344.png)

Setelah login kalian akan masuk pada menu dashboard

![image](https://user-images.githubusercontent.com/106061407/172404481-4b3bc569-c20b-49f6-bb20-647f43cd2fb2.png)

Kemudian pilih menu Compute di kiri pojok dan pilih create new resource

![image](https://user-images.githubusercontent.com/106061407/172404669-5c184564-178e-4f3e-b91f-4bdcbe227fa8.png)

Saya akan gunakan Ubuntu versi 20.04 LTS , Server Indonesia

![image](https://user-images.githubusercontent.com/106061407/172405248-b95a2b46-5256-4abe-8ae7-70c6e1e9c80a.png)

Kemudian kalian isi username dan password , untuk ssh ini opsional kemudian pilih create di kanan bawah

![image](https://user-images.githubusercontent.com/106061407/172405791-60d81b3f-05ad-4aa1-9240-5d7643279a3a.png)

Tunggu proses building server aplikasi hingga selesai

Apabila proses sudah selesai selanjutnya saya akan membuat Server Gateway

![image](https://user-images.githubusercontent.com/106061407/172406372-6947691d-644f-4764-9fda-4a88d6c7eb29.png)

Untuk type pilih app catalog dan Os nya Nginx

![image](https://user-images.githubusercontent.com/106061407/172407417-a2fc6cdc-429f-4118-8791-bdc4a750fa53.png)

Kemudian isi username password dan resource name , untuk ssh ini opsional kemudian pilih create

![image](https://user-images.githubusercontent.com/106061407/172407693-37dba27e-86a0-4fe3-9f15-0f78a8a2089d.png)

Tunggu hingga proses building Gateway selesai

Selanjutnya saya akan login pada kedua server yang sudah saya buat 

Untuk ip kalian bisa cek dengan mengklik resource 

![image](https://user-images.githubusercontent.com/106061407/172408986-845d539b-410a-4d06-acd5-5491c2657d0f.png)

Kalian copy ip public lalu ketikan ssh "username"@"ip" lalu masukan password

![image](https://user-images.githubusercontent.com/106061407/172409319-2037cc3a-d8ab-4963-9e36-f77c1ca53491.png)

Apabila berhasil masuk ke server tampilan akan menjadi seperti ini

![image](https://user-images.githubusercontent.com/106061407/172409542-c97a5886-e1c9-4032-b039-f830e6e71d62.png)

# Melakukan konfigurasi reverse proxy pada Server Gateway

Saya akan login terlebih dahulu pada server gateway

![image](https://user-images.githubusercontent.com/106061407/172411736-a114dcff-9807-44f1-b9d7-d91c94200727.png)

Pertama tama saya akan melakukan update dan upgrade pada server Gateway menggunakan perintah

```
sudo apt update ; sudo apt upgrade
```


