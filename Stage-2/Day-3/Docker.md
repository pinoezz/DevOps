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

![image](https://user-images.githubusercontent.com/106061407/173321026-4dab550a-0f98-46d0-99b4-226eea776a08.png)


```
sudo usermod -aG docker pino
```
Lakukan kepada 2 server


# Create Docker Images

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

