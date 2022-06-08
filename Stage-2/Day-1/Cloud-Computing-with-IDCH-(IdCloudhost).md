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

![image](https://user-images.githubusercontent.com/106061407/172511206-d191f2b0-f5b7-457e-bbb2-1968d114e23b.png)

Menggunakan perintah adduser untuk menambahkan user

```
sudo adduser aplikasi
```
![image](https://user-images.githubusercontent.com/106061407/172525608-f0a8578e-d83c-48a2-9523-50760d1844c8.png)

Untuk memberikan izin sudo pada user baru gunakan perintah 

```
sudo usermod -aG sudo aplikasi
```

Untuk membuat user aplikasi bisa gunakan perintah diatas

![image](https://user-images.githubusercontent.com/106061407/172525912-1323658f-03a8-4a54-b8c6-7fcad6643221.png)


Kemudian untuk login / pindah user bisa menggunakan perintah

```
sudo login aplikasi
```

![image](https://user-images.githubusercontent.com/106061407/172511462-cb78e6bb-90d7-4149-b944-fdff8e3f3b30.png)

Untuk login ssh bisa menggunakan cara seperti ini

```
ssh aplikasi@ip
```

![image](https://user-images.githubusercontent.com/106061407/172525963-2eb93783-a47a-46a5-924d-b786bf4ca841.png)

Kemudian saya update dan upgrade terlebih dahulu


Berikut tadi adalah cara menggunakan useradd saya akan melanjutkan lagi pada instalasi npm , nvm dan cloning fork

Disini saya sudah login pada user aplikasi

Karena disini saya akan mendeploy aplikasi frontend dengan konfigurasi node js jadi terlebih dahulu saya akan menginstall NPM (Node Package Manager)
dan NVM  (Node Version Manager) terlebih dahulu 

![image](https://user-images.githubusercontent.com/106061407/172526646-ad9e0f77-49c2-47a4-96fe-11be9406baa3.png)

```
sudo apt install npm
```

![image](https://user-images.githubusercontent.com/106061407/172526685-c8fbec26-4a22-4e64-bf4d-5beb584fc568.png)


Selanjutnya saya akan Install NVM (Node Version Manager) menggunakan link di bawah ini

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```

![image](https://user-images.githubusercontent.com/106061407/172527023-a33c0631-054e-4d63-8232-11d8436fce6e.png)

Kemudian saya install nvm nya terlebih dahulu

![image](https://user-images.githubusercontent.com/106061407/172528741-a7f6c250-6405-4206-953b-04dff12c46ac.png)


Selanjutnya cloning fork https://github.com/dumbwaysdev/wayshub-frontend menggunakan perintah

```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

![image](https://user-images.githubusercontent.com/106061407/172528775-be395b43-d001-4dcd-a94d-1227c041eb91.png)

![image](https://user-images.githubusercontent.com/106061407/172537060-40d38d75-06b9-4725-af82-2d3ea70b5815.png)

Setelah itu jalankan perintah
```
npm i
```

Setelah sudah saya akan menginstall PM2 yang tujuannya yaitu supaya aplikasi dapat berjalan pada background

![image](https://user-images.githubusercontent.com/106061407/172535692-a65dd638-476f-4934-9462-3bd36f428aed.png)


```
npm install pm2 -g
```
![image](https://user-images.githubusercontent.com/106061407/172535807-f1256e11-700b-4f31-a46b-ff505e9bd98b.png)

Dikarenakan pada direktori diatas tidak ada file index.js untuk menjalankannya kita harus terlebih dahulu membuat file ecosystem untuk menjalankan aplikasinya

![image](https://user-images.githubusercontent.com/106061407/172536070-74cdf52b-df81-4585-9c04-f2e90a694135.png)

```
pm2 ecosystem simple
```

![image](https://user-images.githubusercontent.com/106061407/172536115-a716f09c-6543-49d5-85fe-cb9e085282ac.png)

Kemudian masuk ke file ecosystem.config.js

![image](https://user-images.githubusercontent.com/106061407/172536229-5ddcbebc-e60e-4e5a-a5b2-62c3ab5d8a55.png)


```
module.exports = {
  apps : [{
    name   : "frontend-wayshub",
    script : "npm start"
  }]
}
```
Save dan exit

![image](https://user-images.githubusercontent.com/106061407/172536288-faae329f-1f9f-4a6c-aff9-cf027a41d868.png)

```
pm2 start ecosystem.config.js
```

Kemudian cek di web browser

![image](https://user-images.githubusercontent.com/106061407/172509584-f57a2b19-9cb2-484e-95de-359684d33659.png)

Apabila berhasil akan muncul aplikasi frontend pada web browser


# Membuat DNS (Domain Name Server)


Singkatnya, DNS adalah sebuah sistem yang mengubah URL website ke dalam bentuk IP Address. Tanpa DNS, Anda harus mengetikkan IP Address secara lengkap ketika ingin mengunjungi sebuah website

Disini saya akan membuat DNS pada aplikasi frontend wayshub menggunakan cloudflare

Daftar atau login terlebih dahulu di website [CloudFlare](https://dash.cloudflare.com/)

![image](https://user-images.githubusercontent.com/106061407/172538401-566cff8a-72cd-4610-8c43-ea57b5cf0cd9.png)

![image](https://user-images.githubusercontent.com/106061407/172538469-545cf22d-982e-4714-9cbb-c8e903dad6eb.png)

Kemudian pilih DNS

![image](https://user-images.githubusercontent.com/106061407/172538916-32532372-81b8-41a4-9e9e-2149a5c4d785.png)

Isi nama dan ipv4(ip gateway) kemudian save

Domain yang saya buat : alfino.studentdumbways.my.id

Kemudian Masuk ke terminal lagi server gateway dan melakukan konfigurasi baru pada /etc/nginx/dumbways 

![image](https://user-images.githubusercontent.com/106061407/172539602-e15eb184-3c3c-4842-ad00-daddc527a52f.png)


```
server { 
        server_name alfino.studentdumbways.my.id; 

        location /{
        proxy_pass http://103.31.38.84:3000;
        }
}
```

![image](https://user-images.githubusercontent.com/106061407/172539630-f74900b5-5df9-431b-bcdb-2935539d4a07.png)

Kemudian saya akan cek menggunakan domain http://alfino.studentdumbways.my.id/ pada web browser

![image](https://user-images.githubusercontent.com/106061407/172539753-7cfde937-633f-437c-b105-fd0ce388da07.png)

Apabila berhasil akan tampil aplikasi frontend menggunakan domain http://alfino.studentdumbways.my.id/

# Menggunakan SSL [CertBot](https://certbot.eff.org/) untuk memperaman website

# Apa itu SSL ?

SSL adalah singkatan dari Secure Socket Layer, salah satu komponen penting yang harus dimiliki website. Dengan SSL, transfer data di dalam website menjadi lebih aman dan terenkripsi. Bahkan saking pentingnya, Google Chrome melabeli website tanpa sertifikat SSL sebagai Not Secure.

Apabila sistem keamanan ini ditambahkan pada website Anda, maka URL website akan berubah menjadi HTTPS. Tujuan utama pemasangan SSL adalah sebagai pengaman pertukaran data yang terjadi melalui jaringan internet.

![image](https://user-images.githubusercontent.com/106061407/172540720-a93c852f-c5eb-48be-b185-c795c0a0767e.png)

Langkah pertama instalasi certbot

```
sudo snap install core; sudo snap refresh core
```

![image](https://user-images.githubusercontent.com/106061407/172540860-fbdcf3bc-1ff0-49b0-baf8-8f13f4db08fd.png)

sudo snap install --classic certbot

![image](https://user-images.githubusercontent.com/106061407/172541652-e5e3920a-ccfd-4879-89dc-3104212b0399.png)

Jalankan certbot menggunakan perintah 

```
sudo certbot
```
![image](https://user-images.githubusercontent.com/106061407/172541707-2841c641-bc6b-473b-837f-3acd8917c34c.png)

Apabila berhasil akan muncul kalimat seperti gambar diatas

![image](https://user-images.githubusercontent.com/106061407/172541847-706ea872-5429-4c22-a782-af64c9e108d9.png)

Konfigurasi SSL Certbot otomatis akan ada pada proxy alfino.studentdumbways.my.id

Kemudian saya akan mengecek juga menggunakan web browser dengan menggunakan alamat https://alfino.studentdumbways.my.id/login

![image](https://user-images.githubusercontent.com/106061407/172542049-f56ab5d3-5e8b-473d-890a-9c2c1f578e39.png)

Dan berhasil SSL certbot sudah ada dalam website kalian



