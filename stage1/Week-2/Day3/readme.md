Setelah mempelajari terkait web server, reverse proxy dan load balancing maka buatlah konfigurasi dengan ketentuan sebagai berikut:

![image](https://user-images.githubusercontent.com/106061407/171826913-7119827e-e4b5-49b8-8494-9824ea5e012a.png)

# Project Management​
Tambahkan deskripsi berikut ke dalam kanban pada project management Anda

Konfigurasi web server dengan reverse proxy dan load balancing hingga dapat di akses melalui browser.

- [ ] Definisikan apa itu Web Server menurut pemahamanmu
- [ ] Buatlah 3 buah server (server gateway, server aplikasi1, server aplikasi2)
- [ ] Instal web server nginx pada server gateway
- [ ] Instal aplikasi nodejs pada server aplikasi1 dan server aplikasi2
- [ ] Buatlah sebuah konfigurasi reverse proxy pada server gateway yang mengarah ke server aplikasi1 dengan domain dumbways.xyz
- [ ] Buatlah sebuah konfigurasi load balancing pada server gateway yang mengarah ke server aplikasi2 dengan domain loadbalance.dumbways.xyz


# Ketentuan​

Jalankan 1 aplikasi yang sama pada 2 buah server

Buatlah sebuah konfigurasi reverse proxy pada server gateway (nginx)

Buatlah sebuah konfigurasi load balancing pada server gateway (nginx)

Aplikasi dapat di akses menggunakan domain virtual dan otomatis load balance ke 2 aplikasi tersebut
