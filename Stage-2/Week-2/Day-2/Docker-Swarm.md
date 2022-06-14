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


```
docker stack deploy --compose-file docker-compose.yml stack-todo
```
![image](https://user-images.githubusercontent.com/106061407/173596753-a554d5d4-3ab5-43c0-a9a9-fc270e4a9ac8.png)

Gunakan docker service ls untuk melihat service berjalan

```
docker service ls
```

Selanjutnya saya akan cek salah satu port contohnya port 4000 stack todo service di web browser

![image](https://user-images.githubusercontent.com/106061407/173597101-d6105dd6-a2c1-4f35-b35d-d86c24364419.png)

Berjalan dengan lancar kemudian saya akan scaling stack-todo_todo-skill kepada kedua worker 

![image](https://user-images.githubusercontent.com/106061407/173604877-c7625c8f-5589-4b61-8bda-3cf822d2a3c2.png)

```
docker service scale stack-todo_todo-skill=5
```

Selanjutnya saya akan cek hasil nya di worker
