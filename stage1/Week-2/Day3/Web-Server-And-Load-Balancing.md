# Web Server And Load Balancing

![image](https://user-images.githubusercontent.com/106061407/171828915-d6f1fd78-1d07-4a2a-83fb-383e80637779.png)

# Pengertian Web Server

Pengertian Web Server menurut pemahaman saya yaitu sebuah peragkat lunak yang memberikan layanan berupa data yang berfungsi untuk menerima permintaan client berupa HTTP/HTTPS atau yang biasa kita pakai contohnya seperti halaman halaman web pada browser (chrome,mozila,dll)

 # Membuat 3 buah server (server gateway, server aplikasi1, server aplikasi2)
 
 Untuk task kali ini saya akan menggunakan multipass yang berfungsi untuk server nantinya
 
 Link Download [Multipass](https://multipass.run/)
 
 Perintah Linux
 
# Install multipass
```
sudo snap install multipass
```
 
![image](https://user-images.githubusercontent.com/106061407/171831308-41620679-8f21-475f-bb29-e87eb5c19c60.png)

![image](https://user-images.githubusercontent.com/106061407/171831951-bf677b21-fb13-4b25-8e97-132afa4c2a5a.png)

Kemudian saya akan membuat server baru menggunakan multipass

```
multipass launch --name server1
```
Untuk melihat list server gunakan

```
multipass list
```
![image](https://user-images.githubusercontent.com/106061407/171845728-231d1513-9224-476a-907c-36ca692e4bcf.png)

HINT : Apabila kalian mengalami error seperti gambar di bawah ini saat membuat server multipass kalian dapat ikuti langkah langkah berikut

![image](https://user-images.githubusercontent.com/106061407/171845801-c1c4487b-9340-4f21-8fe0-8d8c3907ba8a.png)

```
export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libgtk3-nocsd.so.0
```
```
exec bash
```

```
sudo apt install gtk3-nocsd
```

Kemudian kalian bisa langsung lanjut membuat servernya

Saya akan membuat 2 server lagi bernama server gateway dan server 2

![image](https://user-images.githubusercontent.com/106061407/171866764-855db866-1180-4073-9c29-de9fbbdd9eda.png)

![image](https://user-images.githubusercontent.com/106061407/171866828-60672328-f64a-41f1-95aa-054ff93c4802.png)


# Instal web server nginx pada server gateway

(https://user-images.githubusercontent.com/106061407/171848779-b0d5a45e-6513-4e30-bfdf-37a482c6d8d7.png)

Langkah awal saya akan masuk pada server gateway dengan menggunakan perintah

```
multipass shell server-gateway
```

![image](https://user-images.githubusercontent.com/106061407/171851068-3572c711-3b80-4799-b2ec-1f98e467ab05.png)


Pada step ini saya akan menginstall nginx terlebih dahulu

```
sudo apt update; sudo apt upgrade
```

```
sudo apt install nginx
```

![image](https://user-images.githubusercontent.com/106061407/171851391-6806db27-d52f-45a2-8547-5d84c18518c9.png)

Untuk cek status nginx gunakan perintah 

```
sudo systemctl status nginx
```
![image](https://user-images.githubusercontent.com/106061407/171852069-60ca1c1c-f8f7-4a2a-8d1d-1130aff3b5ad.png)


Mengecek versi nginx menggunakan

```
nginx -v
```

![image](https://user-images.githubusercontent.com/106061407/171851480-de861b1e-88a7-4193-9900-214fa4d0600e.png)

kemudian saya akan cek pada web browser

![image](https://user-images.githubusercontent.com/106061407/171852288-184d9142-4f6a-41ef-ad21-204982bb6495.png)

Keterangan  : Apabila muncul seperti gambar diatas artinya web server nginx sudah berhasil diinstall dan sudah berjalan

# Instal aplikasi nodejs pada server aplikasi1 dan server aplikasi2

Tutorial install node js [application in server](https://github.com/pinoezz/DevOps/blob/main/stage1/Week-1/Day3/Application-In-Server.md)

![image](https://user-images.githubusercontent.com/106061S407/171860328-5a30f940-4375-415e-9828-a5a0a7e40571.png)

Selanjutnya saya akan clone aplikasi 

```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

![image](https://user-images.githubusercontent.com/106061407/171862346-c96d5346-11da-4869-bbfb-2872e66a1671.png)


Selanjutnya menginstall module dari aplikasi.js

```
npm install
```
![image](https://user-images.githubusercontent.com/106061407/171862998-c170b69a-8c04-4e0e-873c-1ee90a88ccee.png)

Untuk menjalankan aplikasi gunakan

```
npm start
```

lakukan di kedua server aplikasi

# Membuat Konfigurasi Revese Proxy

Apa itu Reverse Proxy?​
Reverse proxy adalah konfigurasi standar yang digunakan untuk mengubah jalur traffic, misalkan aplikasi menggunakan port 3000 tetapi agar dapat di akses melalui port 80 maka harus menggunakan reverse proxy.

Pertama-tama masuk ke folder nginx setelah itu buat suatu directory baru telebih dahulu.

```
cd /etc/nginx
```

![image](https://user-images.githubusercontent.com/106061407/171870369-829fa723-fa42-4e46-b83b-049d961dbc64.png)

Setelah itu saya membuat direktori baru lalu masuk ke direktori baru

```
sudo nano my.reverse-proxy.conf
```

```
server { 
    server_name mydomain.xyz; 
  
    location / { 
             proxy_pass http://127.0.0.1:3000;
    }
}
```

![image](https://user-images.githubusercontent.com/106061407/171875444-1a62849e-3b8e-4e0e-8092-ad443b78ac91.png)

Selanjutnya pergi ke-bagian include, setelah itu masukan lokasi dari directory yang bersi konfigutasi yang sudah kalian buat tadi

![image](https://user-images.githubusercontent.com/106061407/171875955-00ef6164-fbd1-44e9-b599-b2903dba9a7e.png)

![image](https://user-images.githubusercontent.com/106061407/171876239-421a2f92-1dfa-4561-ada8-6bc48ec2cf2c.png)

Beberapa proses tadi adalah cara untuk membuat reverse proxy untuk aplikasi kita, kemudian pastikan untuk melakukan pengecekan konfigurasi dengan menjalankan perintah :

# Setting Aplikasi 1

![image](https://user-images.githubusercontent.com/106061407/172016087-3d413a22-9766-46c3-9be2-ec50bdb6c3d0.png)

![image](https://user-images.githubusercontent.com/106061407/172016776-7dd88366-64ab-4d61-b65b-9fc4976e87c8.png)


![image](https://user-images.githubusercontent.com/106061407/172016072-d260b5ae-e392-4d01-aa0f-7a9476aa7f2f.png)

![image](https://user-images.githubusercontent.com/106061407/172016176-821e3ef0-0f1a-47f5-b590-d276384d877d.png)

Selanjutnya pergi ke-bagian include, setelah itu masukan lokasi dari directory yang bersi konfigutasi yang sudah kalian buat tadi

![image](https://user-images.githubusercontent.com/106061407/172016248-8167f58f-497a-4337-b2f3-253c4bf1857e.png)


Beberapa proses tadi adalah cara untuk membuat reverse proxy untuk aplikasi kita, kemudian pastikan untuk melakukan pengecekan konfigurasi dengan menjalankan perintah :

```
sudo nginx -t
```

![image](https://user-images.githubusercontent.com/106061407/172016325-61856edd-1570-42b5-935f-4a5e4bc8f09e.png)

Sekarang kita akan membuat sebuah virtual host. Untuk membuat virtual host kita harus masuk ke local server kita setelah itu masuk ke dalam file /etc/hosts.

```
sudo nano /etc/hosts
```




