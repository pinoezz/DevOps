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

![image](https://user-images.githubusercontent.com/106061407/171848779-b0d5a45e-6513-4e30-bfdf-37a482c6d8d7.png)

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
