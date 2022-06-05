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
mkdir dumbways
```
![image](https://user-images.githubusercontent.com/106061407/172043798-55e02abd-3e45-47de-9727-f4e9516030de.png)


```
sudo nano proxy.conf
```

```
server { 
    server_name mydomain.xyz; 
  
    location / { 
             proxy_pass http://127.0.0.1:3000;
    }
}
```

![image](https://user-images.githubusercontent.com/106061407/172043952-95e9147a-c8d6-4a61-b6ae-f9c0dab7fe18.png)

Keterangan : ip pada proxypass kalian isi dengan ip aplikasi1 dan port nodejs

Selanjutnya keluar dari directory dumbways, setelah itu masuk ke dalam file nginx.conf.


![image](https://user-images.githubusercontent.com/106061407/172044113-41d21b60-b9e3-4087-af23-5ea6586eb3a3.png)

Selanjutnya pergi ke-bagian include, setelah itu masukan lokasi dari directory yang bersi konfigutasi yang sudah kalian buat tadi.

![image](https://user-images.githubusercontent.com/106061407/172044126-735ff194-3307-498e-a563-701c8b5aa117.png)

Jika sudah sekarang kita tinggal melakukan restart/reload Nginx kita.

```
sudo systemctl restart nginx
```
![image](https://user-images.githubusercontent.com/106061407/172044257-df3de8cc-a633-4588-9f20-1309151841e9.png)


Sekarang kita akan membuat sebuah virtual host. Untuk membuat virtual host kita harus masuk ke local server kita setelah itu masuk ke dalam file /etc/hosts.

```
sudo nano /etc/hosts
```

![image](https://user-images.githubusercontent.com/106061407/172044267-62a35f46-8cc6-4cb7-96c1-812372ab3efe.png)


# Instal aplikasi nodejs pada server aplikasi1


```
git clone https://github.com/dumbwaysdev/dumbflix-frontend.git
```

![image](https://user-images.githubusercontent.com/106061407/172042248-ea651142-78eb-42dd-9e3e-d57c93f35685.png)

```
cd dumbflix-frontend
```

![image](https://user-images.githubusercontent.com/106061407/172042289-3f80e5dd-babd-4df7-9c30-f49c64ea4bef.png)

```
sudo apt update
sudo apt install nodejs npm
```
```
npm i
```
```
npm start
```

![image](https://user-images.githubusercontent.com/106061407/172043361-a27ec07e-5234-4ec0-b6e8-83fdfc71863c.png)

![image](https://user-images.githubusercontent.com/106061407/172043435-87fd14a8-4c09-4578-aefd-2495ea835641.png)

Kemudian cek di web browser 

```
dumbways.xyz
```

![image](https://user-images.githubusercontent.com/106061407/172043483-a625926d-283b-4d8f-ab5c-39dbab2c9b64.png)


# Konfigurasi load balancing pada server gateway yang mengarah ke server aplikasi2 


# Pengertian Load Balancing


Load balancing adalah proses pendistribusian traffic jaringan ke beberapa server. Ini untuk memastikan salah satu server tidak menanggung terlalu banyak beban permintaan. 
Server website yang kelebihan beban membuat proses muat halaman menjadi lambat, atau bahkan tidak terhubung sama sekali.

Secara sederhana, berikut prinsip kerja load balancing:

Mendistribusikan permintaan klien atau beban jaringan secara efisien di beberapa server. Dengan pemerataan distribusi, website atau aplikasi menjadi lebih tanggap dan stabil ketika diakses oleh pengguna.

Memastikan ketersediaan dengan mengirimkan permintaan hanya ke server yang sedang online

Memberikan fleksibilitas untuk menambah atau mengurangi server sesuai permintaan

# Cara Kerja Load Balancing

Apapun bentuknya, perangkat load balancing mendistribusikan traffic ke beberapa server untuk memastikan tidak ada satu server pun yang menanggung beban berlebih. Secara efektif, load balancing meminimalkan waktu respon server. 

# Konfigurasi Load Balancing

Saat ini saya sudah mempunyai 3 server (gateway , aplikasi 1 dan aplikasi2)

![image](https://user-images.githubusercontent.com/106061407/172044546-34b4bd2d-c4d8-42f9-9c95-ff7eb14951e9.png)

Kemudian install dan jalankan npm pada aplikasi2 / server 2

```
sudo apt update
sudo apt install nodejs npm
```
```
npm i
```
```
npm start
```
![image](https://user-images.githubusercontent.com/106061407/172044650-23e7fe92-1a08-4320-9b7a-543123ab3318.png)

Kemudian masuk ke dalam konfigurasi reverse proxy yang sudah kita buat sebelumnya di server gateaway

![image](https://user-images.githubusercontent.com/106061407/172044676-621b8f85-75dc-45b0-926d-3bb9a21f38cf.png)

```
cd /etc/nginx/dumbways
```

```
sudo nano proxy.conf
```

Selanjutnya kita akan tambahkan konfigurasi ke dalam file proxy.conf. Sekarang kita akan coba tambahkan beberapa konfigurasi, kalian dapat menggunakan konfigurasi di bawah ini.

upstream wayshub {
    server 10.68.49.174:3000;
    server 10.68.49.101:3000;
}
server {
    server_name loadbalance.dumbways.xyz;

    location / {
             proxy_pass http://wayshub;
    }
} 
    
keterangan :

Pada bagian upstream kalian dapat mengganti nama domain dengan nama yang kalian inginkan.

Pada bagian server masukan IP dari server kalian, setelah itu diikuti dengan port aplikasi.

Selanjutnya pada bagian proxy_pass ubah dari yang sebelumnya adalah alamat IP dari aplikasi kalian, sekarang kalian samakan dengan nama upstream yang ada di konfigurasi kalian.

Jika sudah sekarang kita coba cek apakah konfigurasi yang sudah kita buat tadi itu error atau tidak.sudo

```
sudo nginx -t
```

![image](https://user-images.githubusercontent.com/106061407/172044878-935c5f13-df65-43fc-b56e-6c3b1fe5892a.png)

Jika tidak ada error jalankan perintah restart nginx untuk merestart nginx kita, karena kita sudah menambahkan 
suatu konfigurasi baru di dalam file reverse proxy kita.
 
 ```
sudo systemctl restart nginx
```

![image](https://user-images.githubusercontent.com/106061407/172044901-8d2c666e-27b7-4200-b4e0-acf8fc08c633.png)
