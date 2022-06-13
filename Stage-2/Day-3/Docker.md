# DOCKER

![image](https://user-images.githubusercontent.com/106061407/173285812-c8a322b7-dcc0-4a9a-9598-b1de0a45f5c2.png)

Docker adalah sistem operasi (atau waktu proses) untuk kontainer. Mesin Docker diinstal pada setiap server tempat Anda ingin menjalankan kontainer dan menyediakan sekumpulan perintah sederhana yang dapat digunakan untuk membuat, memulai, atau menghentikan kontainer.

![image](https://user-images.githubusercontent.com/106061407/173286484-9059456f-56f8-4594-bc7a-e6f77d11e173.png)

Hal pertama yang perlu dipersiapkan yaitu dengan membuat akun pada [Docker Hub](https://hub.docker.com/)

![image](https://user-images.githubusercontent.com/106061407/173314705-b7376e98-e86d-4726-8ef8-72e0c51f2b42.png)

# TASK

# Docker Installation

[Tutorial install docker](https://docs.docker.com/engine/install/ubuntu/)

Bagian pertama dalam pembuatan Docker saya akan mempersiapkan 2 buah server yang nantinya akan saya install Docker untuk gateway dan Docker untuk menjalankan (Frontend, Backend, dan Database)

Saya akan gunakan VPS yang di sediakan oleh [IDCloudHost](https://idcloudhost.com/) 

![image](https://user-images.githubusercontent.com/106061407/173315738-66b4b918-4000-4411-b17d-5faf521100ba.png)

Kemudian saya akan build 

![image](https://user-images.githubusercontent.com/106061407/173319377-2421003b-5eca-4b34-a5eb-187479cc378a.png)

![image](https://user-images.githubusercontent.com/106061407/173319876-00e09adc-f248-4f7f-b7fc-67b31ff58961.png)

Kemudian saya akan mengoneksikan VPS menggunakan terminal menggunakan perintah

ssh "username"@"ip host"

```
ssh pino@103.174.115.37
```
![image](https://user-images.githubusercontent.com/106061407/173320411-c045e34e-f2ea-484b-a97d-749227c21895.png)

Akan secara otomatis terinstall docker  


![image](https://user-images.githubusercontent.com/106061407/173321455-aa3f93db-98b8-42e1-a08e-fa44e72f354e.png)

Saya akan melakukan update dan upgrade terlebih dahulu

```
sudo apt update ; sudo apt upgrade
```

Kemudian saya akan memerikan hak akses root kepada docker supaya nantinya tidak perlu menggunakan sudo


```
sudo usermod -aG docker pino
```
Lakukan kepada 2 server


# Create Docker Images

# DOCKER IMAGES IN GATEWAY

Pada gateway saya akan menginstall [Nginx](https://hub.docker.com/_/nginx) 

![image](https://user-images.githubusercontent.com/106061407/173324606-7592acd2-2743-464b-bf38-307d1f8cfe38.png)

Lakukan login terlebih dahulu

```
docker login
```

![image](https://user-images.githubusercontent.com/106061407/173325255-1ab16e2a-c35f-4fb9-b9ee-922e656c1ec1.png)

Kemudian saya akan menginstall image [Nginx](https://hub.docker.com/_/nginx) untuk versinya saya akan install versi terbaru (latest)

```
docker pull nginx:latest
```

![image](https://user-images.githubusercontent.com/106061407/173326278-f49b570e-bbae-42ff-9daf-85d7df29a7d0.png)

Untuk mengetahui image apa saja yang sudah terinstall bisa gunakan perintah 

```
docker images
```

```
docker image ls
```

Selanjutnya saya akan membuat container nginx 

![image](https://user-images.githubusercontent.com/106061407/173334127-abffddf1-616e-49fc-829a-f3594624fe3a.png)

```
docker container create --name nginx1 -p 8080:80 nginx:latest
```

Untuk menjalankan container diatas gunakan perintah

![image](https://user-images.githubusercontent.com/106061407/173334556-8b2348ae-8b18-45ae-a3cb-6f9ca837ca1c.png)

```
docker container start nginx1
```
Masuk ke container nginx menggunakan perintah

![image](https://user-images.githubusercontent.com/106061407/173335034-8ad87605-882e-4720-9d90-ff580e0168bb.png)

```
docker exec -it nginx1 bash
```

![image](https://user-images.githubusercontent.com/106061407/173335204-1d1cfdfa-4937-4d9a-b23f-621d0be1e40a.png)

Selanjutnya saya akan cek menggunakan web browser dengan mencari ip dari host dan port nginx (8080)

![image](https://user-images.githubusercontent.com/106061407/173335468-c2f4b002-53a8-4278-a119-b2035039c000.png)


# DOCKER IMAGES IN APP

Pada App saya akan menginstall [Mysql](https://hub.docker.com/_/mysql) sebagai database

![image](https://user-images.githubusercontent.com/106061407/173327020-806d5501-6cd1-4cfd-9047-713f358f8b3b.png)

![image](https://user-images.githubusercontent.com/106061407/173329145-062d6474-07df-4d25-bab1-6e323213d381.png)

```
docker pull mysql:latest
```

# Docker Setup Frontend , Backend and databases

FORK FRONTEND :
```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

FORK BACKEND  : 

```
git clone https://github.com/dumbwaysdev/wayshub-backend
```

Saya akan cloning kedua fork FE(frontend) dan BE(Backend)

![image](https://user-images.githubusercontent.com/106061407/173351746-ea70f73b-f973-4bc3-8f67-393fad02c2af.png)

Kemudian saya akan membuat volume dengan direktori mysql-database

![image](https://user-images.githubusercontent.com/106061407/173354063-d81f27e6-73da-4b95-bff5-41840b0b17a3.png)

```
docker run -d --name database -p 3306:3306 -v ~/mysql-database:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=P4ssw0rd -e MYSQL_DATABASE=wayshub mysql:latest
```

![image](https://user-images.githubusercontent.com/106061407/173354451-c187999c-8cf4-44c4-b17f-5c4d13405e4e.png)

Untuk memasuki container mysql gunakan perintah 

```
docker container exec -it database bash
```

Kemudian saya akan melihat daftar databases

![image](https://user-images.githubusercontent.com/106061407/173354657-d659538a-cc58-4696-83f3-78dfafd7309e.png)

Selanjutnya saya akan konfigurasi backend menggunakan docker compose

Install terlebih dahulu docker compose

![image](https://user-images.githubusercontent.com/106061407/173354994-dbdb371c-e7bb-4af3-8f6c-e468d558509a.png)


```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

```
sudo chmod +x /usr/local/bin/docker-compose
```

Untuk cek versi docker compose gunakan perintah

```
docker compose --version
```

Selanjutnya saya akan masuk ke direktori backend dan melakukan konfigurasi mengoneksikan backend ke database dan melakukan migrasi sequelize 

![image](https://user-images.githubusercontent.com/106061407/173355873-894acb96-c973-4951-a9fa-16b504bbf3fa.png)

app@App-alfino:~/wayshub-backend/config$ 

```
nano config.json
```

![image](https://user-images.githubusercontent.com/106061407/173356362-2d9f847a-3328-4afe-8e05-2adec95630fa.png)

Setelah mengubah kemudian save 

Kemudian kembali  ke direktori wayshub-backend dan saya akan membuat dockerfile

NOTE : SAYA GUNAKAN node:dubnium-alpine3.11 (karena sizenya kecil)

![image](https://user-images.githubusercontent.com/106061407/173359394-d07bbb21-47a9-4364-9cd5-9841523d18a7.png)


![image](https://user-images.githubusercontent.com/106061407/173356581-124db5ef-e764-4c54-a725-9f84613e1e23.png)

```
nano dockerfile
```

Untuk membuat file dockerfile

![image](https://user-images.githubusercontent.com/106061407/173359925-bc03474e-9e86-4155-be6f-4dd885a49394.png)

build dockerfile 

![image](https://user-images.githubusercontent.com/106061407/173362217-9021c7e6-a5b6-4ed9-a841-306f99dd03d9.png)

![image](https://user-images.githubusercontent.com/106061407/173362329-963f6af5-3a73-44d3-b424-62b2f1ee7b5a.png)


```
docker build -t pino/wayshub-be:1.0 .
```

Kemudian selanjutnya saya akan membuat docker-compose.yml 

![image](https://user-images.githubusercontent.com/106061407/173364307-5936f9a2-c536-4578-b26f-10eed65fc74a.png)


```
version: '3.8'
services:
 backend:  
   build: .    
   container_name: be
   image: pino/wayshub-be:stable
   stdin_open: true
   ports:
    - 5050:5000
```    

![image](https://user-images.githubusercontent.com/106061407/173364381-99fcb952-d5ee-4500-93c2-9911d5dfa432.png)

![image](https://user-images.githubusercontent.com/106061407/173364431-92ca9249-aa52-46bb-b1a6-980e1808e487.png)

![image](https://user-images.githubusercontent.com/106061407/173364671-5f54ace7-c893-4ec8-a5f0-3d5064cff400.png)

Untuk jalankan docker-compose gunakan perintah

```
docker-compose up -d
```

![image](https://user-images.githubusercontent.com/106061407/173365201-1a4d2d5a-4c32-4627-9822-75eef0a6bcfa.png)

Bisa di cek container app backend sudah berjalan dan selanjutnya saya akan cek menggunakan web browser

![image](https://user-images.githubusercontent.com/106061407/173365329-53848ca2-ed4d-47ae-8f2f-c699a92d3777.png)

Jika hasilnya seperti ini artinya berhasil 

Kemudian saya akan cek juga migrasi datanya pada mysql

![image](https://user-images.githubusercontent.com/106061407/173366333-b1b5be9c-9c08-4c30-84d8-1baf6b5e8aa1.png)

Migrasi data berhasil :D

Selanjutnya saya ingin push repo menuju docker hub

Dikarenakan nama repository saya berbeda tidak sesuai username docker hub jadi saya akan membuat tag baru

![image](https://user-images.githubusercontent.com/106061407/173370570-d49d2cb5-4e74-477f-9055-6d663e410f79.png)

```
docker tag 98afd9e2ba69 pinoezz/wayshub-be
```

![image](https://user-images.githubusercontent.com/106061407/173371272-7a3e098e-50c4-493d-88cd-312c5c54fe79.png)

```
docker push pinoezz/wayshub-be
```

KETERANGAN : Apabila nama repository tidak sesuai dengan akun docker hub maka akan muncul pesan "denied: requested access to the resource is denied"

Selanjutnya cek di web browser 

![image](https://user-images.githubusercontent.com/106061407/173371987-869383c7-914c-4eeb-9525-76d33a2312aa.png)


