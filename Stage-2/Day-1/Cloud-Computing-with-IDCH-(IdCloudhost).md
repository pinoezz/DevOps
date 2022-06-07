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

![image](https://user-images.githubusercontent.com/106061407/172426475-b302a180-bd07-4cbb-a11c-f62556015b8d.png)

Kalian copy ip public lalu ketikan ssh "username"@"ip" lalu masukan password

![image](https://user-images.githubusercontent.com/106061407/172426363-907dc855-dbff-46fc-86d9-7b9cce7ed836.png)

Apabila berhasil masuk ke server tampilan akan menjadi seperti ini

![image](https://user-images.githubusercontent.com/106061407/172427488-e422b7f9-1a12-418c-bf83-85b0bf9efc5f.png)

# Melakukan konfigurasi reverse proxy pada Server Gateway

Saya akan login terlebih dahulu pada server gateway

![image](https://user-images.githubusercontent.com/106061407/172411736-a114dcff-9807-44f1-b9d7-d91c94200727.png)

Pertama tama saya akan melakukan update dan upgrade pada server Gateway menggunakan perintah

```
sudo apt update ; sudo apt upgrade
```
![image](https://user-images.githubusercontent.com/106061407/172413097-e9f3b975-30c7-464a-bf7d-f76caceb3281.png)

Kemudian check versi nginx dengan menggunakan perintah 

```
nginx -v
```

Seharusnya pada server Gateway ini otomatis terinstall nginx

![image](https://user-images.githubusercontent.com/106061407/172416655-068e16f5-8a80-4295-a8a3-dd0a3c1e190b.png)

Selanjutnya buat direktori baru pada /etc/nginx , saya akan membuat direktori baru bernama dumbways dengan perintah

```
sudo mkdir dumbways
```

![image](https://user-images.githubusercontent.com/106061407/172417114-c0c9b398-3bdb-4c1b-b668-bfb8f5756cb3.png)

Selanjutnya saya akan membuat file untuk menyimpan konfigurasi dari reverse proxy 

```
sudo nano proxy.conf
```

![image](https://user-images.githubusercontent.com/106061407/172419867-47339153-f52d-4acf-baa8-cdf344bb48b9.png)

```
server {
        server_name wayshub.xyz;

        location / {
                proxy_pass http://10.71.15.131:3000;
        }
}
```

Keterangan : server_name adalah nama server , proxy_pass isi dengan ip dari aplikasi 

Kemudian save 

![image](https://user-images.githubusercontent.com/106061407/172418453-7a74ef01-49f2-4b68-8c1d-1a9dffc91e59.png)

Kemudian masuk ke file nginx.conf untuk menambahkan konfigurasi proxypass

![image](https://user-images.githubusercontent.com/106061407/172418936-2ad280ca-3f74-40cf-9e84-7320b19b8bde.png)

Setelah menambahkan konfigurasi reverse proxy pada nginx.conf kalian bisa save lalu exit

![image](https://user-images.githubusercontent.com/106061407/172420887-cbed699f-3779-446b-ad1f-d5b68326738d.png)


Untuk mengecek konfigurasi file reverse proxy kalian bisa menggunakan perintah 

```
sudo nginx -t
```

# Menginstall Aplikasi Frontend 

Pertama tama switch atau login terlebih dahulu pada server aplikasi atau server frontend terlebih dahulu

![image](https://user-images.githubusercontent.com/106061407/172430835-8783286a-0a18-466d-bb37-b264eaf9dad5.png)

saya juga akan membuat user baru terlebih dahulu 

![image](https://user-images.githubusercontent.com/106061407/172431548-a72adb98-c3a4-4ef1-80d2-411c32b758f6.png)

Setelah itu buat juga password untuk user aplikasi

![image](https://user-images.githubusercontent.com/106061407/172421715-c551ff7d-15f9-475b-8398-564024451c29.png)

Untuk menghapus user kalian bisa gunakan perintah userdel

![image](https://user-images.githubusercontent.com/106061407/172432690-df6049f4-9edb-47c7-aaf3-b68159d1a186.png)

Kemudian saya akan membuat user dengan direktori 

![image](https://user-images.githubusercontent.com/106061407/172433364-85a2c8a1-510a-4bd0-b509-d7d9764695e0.png)

Menggunakan perintah useradd -m untuk membuat user baru sekaligus beserta direktori

Berikut tadi adalah cara menggunakan useradd saya akan melanjutkan lagi pada instalasi npm , nvm dan cloning fork

Disini saya sudah login pada server frontend/aplikasi

![image](https://user-images.githubusercontent.com/106061407/172421978-79f003cd-0493-4f88-a6a2-515cfe17957e.png)

Selanjutnya cloning fork https://github.com/dumbwaysdev/wayshub-frontend menggunakan perintah

```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```
Karena disini saya akan mendeploy aplikasi frontend dengan konfigurasi node js jadi terlebih dahulu saya akan menginstall NPM (Node Package Manager)
dan NVM  (Node Version Manager) terlebih dahulu 

![image](https://user-images.githubusercontent.com/106061407/172423325-f0527f60-4672-48d5-abaf-72beeee70e37.png)

```
sudo apt install npm
```

![image](https://user-images.githubusercontent.com/106061407/172436747-27c08234-f845-4ed1-99ae-31a9f343c2fb.png)


Selanjutnya saya akan Install NVM (Node Version Manager) menggunakan link di bawah ini

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
![image](https://user-images.githubusercontent.com/106061407/172436878-72c2c2c0-5cfa-44dc-a28c-b0c39712f2b4.png)

![image](https://user-images.githubusercontent.com/106061407/172437204-c25fbcc8-97c5-451e-ae5b-d14128099522.png)

![image](https://user-images.githubusercontent.com/106061407/172437471-6f67210e-09e5-4a74-bd44-73d4eab51675.png)

Setelah semua sudah saya akan menginstall PM2 yang tujuannya yaitu supaya aplikasi dapat berjalan pada background

```
npm install pm2 -g
```
![image](https://user-images.githubusercontent.com/106061407/172438334-150c24ff-4f02-4d0b-980b-b34f9c075c51.png)

![image](https://user-images.githubusercontent.com/106061407/172438395-8691fc8b-9ae7-4645-ae2d-e296a37ad434.png)

![image](https://user-images.githubusercontent.com/106061407/172438414-55f97f9b-dce8-4b30-b4cd-cb25435ec08d.png)

![image](https://user-images.githubusercontent.com/106061407/172438524-cf4fb8fa-e587-421b-bbe6-9f4ada1243aa.png)

Dikarenakan pada direktori diatas tidak ada file index.js untuk menjalankannya kita harus terlebih dahulu membuat file ecosystem untuk menjalankan aplikasinya

![image](https://user-images.githubusercontent.com/106061407/172439023-d186e13c-3381-4744-9f3a-6df50b38bf3b.png)

```
pm2 ecosystem
```
![image](https://user-images.githubusercontent.com/106061407/172439727-a99aca65-2635-48ce-8841-8bf0bec9c342.png)

