# DOCKER

![image](https://user-images.githubusercontent.com/106061407/173285812-c8a322b7-dcc0-4a9a-9598-b1de0a45f5c2.png)

Docker adalah sistem operasi (atau waktu proses) untuk kontainer. Mesin Docker diinstal pada setiap server tempat Anda ingin menjalankan kontainer dan menyediakan sekumpulan perintah sederhana yang dapat digunakan untuk membuat, memulai, atau menghentikan kontainer.

![image](https://user-images.githubusercontent.com/106061407/173286484-9059456f-56f8-4594-bc7a-e6f77d11e173.png)

Hal pertama yang perlu dipersiapkan yaitu dengan membuat akun pada [Docker Hub](https://hub.docker.com/)

![image](https://user-images.githubusercontent.com/106061407/173314705-b7376e98-e86d-4726-8ef8-72e0c51f2b42.png)

# TASK

# Docker Installation

[Tutorial install docker](https://docs.docker.com/engine/install/ubuntu/)

Bagian pertama dalam pembuatan Docker saya akan mempersiapkan 2 buah server yang nantinya akan saya install Nginx untuk gateway dan Docker untuk menjalankan (Frontend, Backend, dan Database)

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

# Gateway installation

![image](https://user-images.githubusercontent.com/106061407/173381927-bdba7835-d64c-437a-ba05-c5dfe9586485.png)

![image](https://user-images.githubusercontent.com/106061407/173382017-2bf3eae2-5118-493c-968e-3ddba96d95db.png)


# Create Docker Images

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

Apabila berhasil akan muncul repository baru

Sebelum lanjut ke step selanjutnya tentang konfigurasi pada app frontend saya akan membuat DNS pada app backend menggunakan [CloudFlare](cloudflare.com)

![image](https://user-images.githubusercontent.com/106061407/173374237-8c4c897d-8080-4db5-972b-d4d1a309523a.png)

Selanjutnya saya akan konfigurasi api.js pada direktori /home/app/wayshub-frontend/src/config yang gunanya untuk menghubungkan FE & BE 

![image](https://user-images.githubusercontent.com/106061407/173386895-eaca7623-9b91-4781-9c19-1e3b6a691fa0.png)

Kemudian buat dockerfile pada frontend

![image](https://user-images.githubusercontent.com/106061407/173387557-eae604fc-8ef8-468b-ae60-438cc5594cc2.png)


```
nano dockerfile
```

```
FROM node:dubnium-alpine3.11
WORKDIR /usr/app
COPY . .
RUN npm install
EXPOSE 3000
CMD [ "npm", "start" ]
```

![image](https://user-images.githubusercontent.com/106061407/173387642-33a4f5dc-9212-4664-a7bd-871e081474a7.png)


Selanjutnya saya langsung membuat docker-compose.yml pada frontend

```
nano docker-compose.yml
```
```
version: '3.8'
services: 
 frontend:
   build: .    
   container_name: fe
   image: pinoezz/wayshub-fe:stable
   stdin_open: true
   ports: 
    - 3030:3000
```

Kemudian save lalu exit

![image](https://user-images.githubusercontent.com/106061407/173389157-cafb02f6-c65b-462a-84d1-f6505a9e89f3.png)

Untuk build serta jalankan docker compose secara daemon menggunakan 

```
docker-compose up -d
```
Kemudian cek image pada docker

![image](https://user-images.githubusercontent.com/106061407/173390643-45f57c21-7c54-4924-b4e5-3827a21505c3.png)

![image](https://user-images.githubusercontent.com/106061407/173390725-0780a14b-6d6d-40f6-a212-0b0573375bc2.png)

Kemudian untuk memastikan cek juga menggunakan web browser

![image](https://user-images.githubusercontent.com/106061407/173390455-687de95b-5309-4d6f-be63-0ae129862ef2.png)

# Setup Gateway (Proxy & SSL)

Beralih ke server gateway saya akan cek terlebih dahulu nginxnya

![image](https://user-images.githubusercontent.com/106061407/173391618-18a3e9d0-2244-48a4-8689-57edefe67eab.png)

Kali ini saya gunakan nginx version: nginx/1.18.0 (Ubuntu)

Kemudian saya akan membuat reverse proxy FE dan BE , Saya akan membuat direktori baru bernama wayshub pada /etc/nginx

Untuk domain saya mengggunakan domain dari [CloudFlare](cloudflare.com)

![image](https://user-images.githubusercontent.com/106061407/173392704-ee6c1405-a600-4230-8af0-2bdbd093da7c.png)

![image](https://user-images.githubusercontent.com/106061407/173393350-892a6e13-08bc-42d3-8915-bf749209bc2d.png)


KONFIGURASI REVERSE PROXY FE 

```
server {
        server_name alfino.studentdumbways.my.id;
 
        location /{
        proxy_pass http://103.179.57.222:3030;
        }
}
```

KONFIGURASI REVERSE PROXY BE

```
server {
        server_name api.alfino.studentdumbways.my.id;
 
        location /{
        proxy_pass http://103.179.57.222:5050;
        }
}
```

Kemudian kembali pada direktori/etc/nginx dan menambahkan konfigurasi reverse proxy yang ada pada direktori wayshub

![image](https://user-images.githubusercontent.com/106061407/173393700-a161f42d-78bf-4ac2-ac43-e631605b81ad.png)

```
include /etc/nginc/wayshub/*;
```

Kemudian save dan exit

![image](https://user-images.githubusercontent.com/106061407/173393811-73ec84aa-54c4-441b-8ad2-a25c7070fb4b.png)

Cek konfigurasi menggunakan

```
sudo nginx -t
```

![image](https://user-images.githubusercontent.com/106061407/173393920-9886895e-84e9-43d8-bd71-49eac39f85af.png)

Kemudian restart nginx.service 

```
sudo systemctl restart nginx.service 
```
