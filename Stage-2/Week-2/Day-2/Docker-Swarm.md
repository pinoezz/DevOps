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

![image](https://user-images.githubusercontent.com/106061407/173577070-e100793d-3e2c-47f4-b419-2ce947c810b2.png)

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

Kemudian build 
