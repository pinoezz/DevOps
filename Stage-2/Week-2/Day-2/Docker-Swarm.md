# Docker Swarm

![image](https://user-images.githubusercontent.com/106061407/173556733-3eb91639-b5d2-4ff9-8167-d26237204c72.png)

Docker Swarm merupakan Container Orchestration System yang disediakan oleh docker untuk memdistribusikan docker contrainer pada system cluster. Dengan kita memanfaatkan docker swarm, kita dapat membuat sebuah management yang centralized baik itu create, destroy, scaling up dan scaling down container pada docker swarm manager.

Kelebihan
Scalable — aplikasi arsitektur layanan mikro umumnya mudah untuk di upgrade dan diatur sesuai dengan kebutuhan pengguna.
Aman — microservices juga umumnya sangat aman dan secure karena telah dirancang untuk mampu mengatasi semua kegagalan yang mungkin terjadi.

Kekurangan 
Rawan error antar service

![image](https://user-images.githubusercontent.com/106061407/173557011-b6eb2a36-6044-46f8-bcd2-8cc40af49834.png)

Pada task kali ini saya akan membuat konfigurasi dari docker swarm yang nantinya saya akan menggunakan VPS dari [IDCLoudHost](idcloudhost.com)


Saya membuaat 3 buah server (Manager, Worker1, Dan Worker2)

![image](https://user-images.githubusercontent.com/106061407/173571159-c7ff9217-54b7-42e7-baeb-008910d6158a.png)

Setelah membuat 3 Server kemudian saya login ke3 server nya

![image](https://user-images.githubusercontent.com/106061407/173571087-f924c28b-931b-42a3-9bf0-4bf85280d216.png)

![image](https://user-images.githubusercontent.com/106061407/173571324-147c9817-23de-4305-ba38-de55cdef7479.png)


Kemudian cek versi docker menggunakan 

```
docker version
```

KETERANGAN : Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/version": dial unix /var/run/docker.sock: connect: permission denied

Apabila ada error seperti diatas artinya untuk menjalankan docker kita perlu akses root . Untuk solusinya saya akan memberikan akses root pada docker

![image](https://user-images.githubusercontent.com/106061407/173571609-f4dd2db3-60e8-4340-8d86-6eae4a79bb9f.png)

![image](https://user-images.githubusercontent.com/106061407/173571792-a3f1d07f-ebb7-410e-9cdc-5bdbaf586f3a.png)


```
sudo usermod -aG docker worker
```

Kemudian Relogin dan cek kembali menggunakan docker version

![image](https://user-images.githubusercontent.com/106061407/173571893-9b34792d-524a-4ba0-abf7-344c2979a4aa.png)

Sekarang saya dapat menjalankan perintah docker tanpa harus mengetikan sudo

KETERANGAN : Lakukan pada ke 3 server supaya masing-masing mendapatkan akses root pada docker



![image](https://user-images.githubusercontent.com/106061407/173575556-faf62a28-b290-4412-818a-a9ce7ae0ebee.png)


Pertama tama saya akan mengcloning fork https://github.com/sgnd/dumbways-docker-microservices

Kemudian masuk pada direktori /home/pino/dumbways-docker-microservices

Lalu edit file docker-compose.yml

![image](https://user-images.githubusercontent.com/106061407/173576768-1aed50c7-950e-4079-ba6a-60e045c84ca3.png)

![image](https://user-images.githubusercontent.com/106061407/173577030-c34524da-5096-4a1f-9ff9-8cf55f9bde2a.png)

![image](https://user-images.githubusercontent.com/106061407/173589895-a0577a8b-c372-47be-aaf2-84a0a897f905.png)

Saya akan mengubah tempat direktori dan image

Kemudian save dan exit

# Konfigurasi Manager untuk Inisialisasi Swarm Cluster

Sekarang kita akan membuat swarm cluster untuk ketiga server. Untuk membuatnya, memerlukan inialisasi pada dockermanager 

KETERANGAN : Saya membuat 3 server docker (pino), (worker), (worker)
user pino 103.183.74.76 (manager) dan worker 103.186.1.150 (worker 1) dan worker 103.186.1.179 (worker 2)

![image](https://user-images.githubusercontent.com/106061407/173579806-8ca2de48-f576-46cc-ad64-4ca92bd3c6d3.png)


```
docker swarm init –advertise-addr <manager node IP address>
```

Pada hasil diatas, join token sudah digenerate oleh dockermanager, ini nanti digunakan untuk join dockerworkers


Konfigurasi Docker2 dan Docker3 Node untuk join Swarm Cluster

![image](https://user-images.githubusercontent.com/106061407/173580512-4cdde54b-009e-4da8-9995-12359a64b170.png)

![image](https://user-images.githubusercontent.com/106061407/173580556-c235add2-8798-4a30-bb7a-a1586f3f8e62.png)



Verifikasi Swarm Cluster

![image](https://user-images.githubusercontent.com/106061407/173580993-783baecd-1221-4993-aa7b-68b9a90f0bb6.png)

Untuk melihat status node menggunakan command berikut di dockermanager

```
docker node ls
```

Kemudian saya akan build docker-compose 

![image](https://user-images.githubusercontent.com/106061407/173589955-35954769-4eb0-4310-84e9-5b35a239cd55.png)

```
docker-compose build
```

![image](https://user-images.githubusercontent.com/106061407/173592799-070f6556-da3a-4dc8-8657-041d9066e98e.png)

Apabila proses build image sudah selesai bisa cek menggunakan perintah 

```
docker images
```

Selanjutnya saya akan mengcloning fork dan mengedit file docker-compose seperti sebelumnya pada kedua worker dan kemudian di build

![image](https://user-images.githubusercontent.com/106061407/173599135-a66144e2-a227-49d7-ac35-f74e0856dd1f.png)

![image](https://user-images.githubusercontent.com/106061407/173599526-4a8720f0-53b8-4547-9f49-8c58241ef48a.png)

![image](https://user-images.githubusercontent.com/106061407/173600004-d56cd299-0fe5-4367-8bdb-d5fd6c21d0a4.png)



Selanjutnya saya akan mendeploy stack todo dan nantinya akan saya scaling pada worker

![image](https://user-images.githubusercontent.com/106061407/173596689-6ea579bc-3b90-44e9-8d11-1e88eb34de65.png)

![image](https://user-images.githubusercontent.com/106061407/173724251-c6156477-8049-4eef-97a5-6a9c731db102.png)


```
docker stack deploy --compose-file docker-compose.yml stack-todo
```

![image](https://user-images.githubusercontent.com/106061407/173596753-a554d5d4-3ab5-43c0-a9a9-fc270e4a9ac8.png)

![image](https://user-images.githubusercontent.com/106061407/173724386-afb98078-b170-4d5d-96c9-875763d08377.png)

![image](https://user-images.githubusercontent.com/106061407/173724408-1846b60c-6bb3-4a08-aa91-f30317ddb76e.png)


Gunakan docker service ls untuk melihat service berjalan

```
docker service ls
```
![image](https://user-images.githubusercontent.com/106061407/173725204-dd2c87ee-44d8-4005-801f-c31b0158657e.png)


Kemudian saya akan  melakukan deploy aplikasinya

```
docker stack deploy --compose-file docker-compose.yml stack-todo
```

![image](https://user-images.githubusercontent.com/106061407/173725504-c64600d1-3cc7-4ff7-9c17-b71087a7cfbf.png)


Selanjutnya saya akan cek salah satu port contohnya port 4000 stack todo service di web browser

![image](https://user-images.githubusercontent.com/106061407/173597101-d6105dd6-a2c1-4f35-b35d-d86c24364419.png)

![image](https://user-images.githubusercontent.com/106061407/173725635-4448cf82-5ad7-4595-9a1c-200a413c3042.png)


Berjalan dengan lancar kemudian saya akan scaling stack-todo_todo-profile kepada kedua worker 

![image](https://user-images.githubusercontent.com/106061407/173731292-d81225f2-9392-4b4b-ae53-bf50e965b73a.png)


```
docker service scale stack-todo_todo-profile=5
```

Selanjutnya akan terpecah beberapa compose menuju worker

# Contoh 2 docker swarm create yang lebih ringan

Baik cara ke 2 ini saya akan membuat file yang nantinya akan di scale

![image](https://user-images.githubusercontent.com/106061407/173755241-4d1b81eb-fe0d-407e-bc39-8e65a6825f98.png)


```
docker service create --replicas 1 --name helloworld alpine ping google.com
```

Untuk melihat service berjalan gunakan 

![image](https://user-images.githubusercontent.com/106061407/173755484-ab39d10d-d87e-494e-b61e-dff5e25d86e2.png)

```
docker service ls
```

Dan untuk melihat container yang sedang berjalan bisa gunakan 


```
docker ps
```

Kemudian saya akan melakukan scaling

![image](https://user-images.githubusercontent.com/106061407/173755865-e4b813b8-4fe8-4bd1-bfe0-4bc227075dab.png)

```
docker service scale helloworld=5
```

Kemudian cek menggunakan docker ps

![image](https://user-images.githubusercontent.com/106061407/173755972-b905d01e-dd10-42a4-9d16-377a853c841d.png)

Pada manager terdapat 2 container

![image](https://user-images.githubusercontent.com/106061407/173756145-206281ff-4aeb-44a1-b833-130de1d669b3.png)

Pada worker 1 terdapat 1 container

![image](https://user-images.githubusercontent.com/106061407/173756208-8722f533-28e6-4b17-ba70-98f6f5a6a6b9.png)

Pada worker 2 terdapat 2 container 



