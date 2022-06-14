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







