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

