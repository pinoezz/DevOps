# Instalasi Webserver menggunakan Nginx

Berikut ansible-playbook instalasi nginx pada server nginx

```
- hosts: nginx
  become: yes
  gather_facts: yes
  tasks:
        - name: 'install nginx'
          apt: 
            name:
             - nginx
            state: latest
 ```
 
Pertama-tama saya akan tes ping dan cek syntax file `nginx.yml`.
 
```
ansible-playbook --syntax-check nginx.yml 
```
 
```
ansible nginx -m  ping
```
 
![image](https://user-images.githubusercontent.com/106061407/176121499-b08ff57e-7867-48a7-80ca-3fabc3c1fd0e.png)

Kemudian jalankan ansible-playbook `nginx.yml`.

```
ansible-playbook nginx.yml
```

![image](https://user-images.githubusercontent.com/106061407/176124472-25cae9e9-64a6-420c-b6e0-6a6f09ff3e9c.png)

Kemudian saya akan cek pada Server Nginx

![image](https://user-images.githubusercontent.com/106061407/176124651-e1508c8a-6f73-49f4-b8e9-9513207dc7dc.png)

Nginx berhasil di install dan sudah berjalan , kemudian saya akan cek juga pada web browser

![image](https://user-images.githubusercontent.com/106061407/176124902-c9f23418-19b5-444e-8b45-a5a7b6a91e70.png)

## Konfigurasi WebServer

Saya akan menggunakan domain dari [CloudFlare](https://dash.cloudflare.com/)

- Reverse proxy the frontend -> https://alfino.studentdumbways.my.id
- Reverse proxy the backend -> https://api.alfino.studentdumbways.my.id
- Reverse proxy the nodeexporter -> https://exporter.alfino.studentdumbways.my.id
- Reverse proxy the prometheus -> https://prometheus.alfino.studentdumbways.my.id
- Reverse proxy the grafana -> https://monitoring.alfino.studentdumbways.my.id
- Reverse proxy the Jenkins -> https://pipeline.alfino.studentdumbways.my.id

Kemudian selanjutnya kofigurasi reverse proxy pada nginx, saya akan membuat folder bernama `housy` yang nantinya berisi konfigurasi reverse proxy semua server yang akan saya gunakan

![image](https://user-images.githubusercontent.com/106061407/176133314-3e003952-6f1f-4c32-9d23-6dcab726432d.png)

Kemudian saya akan memasukan konfigurasi diatas pada `nginx.conf`

![image](https://user-images.githubusercontent.com/106061407/176134065-932999c8-cced-4f0e-9a62-94c3b189b851.png)

Kemudian cek syntax 

```
sudo nginx -t
```
![image](https://user-images.githubusercontent.com/106061407/176134219-0077dfa8-574a-49ac-97eb-640185458f0f.png)

Kemudian restart services menggunakan

```
sudo systemctl restart nginx.service
```

![image](https://user-images.githubusercontent.com/106061407/176140728-410d184e-c027-4ad5-8be4-11c17e5bb678.png)


# SSL CLoudFlare

Step 1 — Generating an Origin CA TLS Certificate

![image](https://user-images.githubusercontent.com/106061407/176168383-2019d4d8-e8c8-4c76-b683-ec252816a5e7.png)

![image](https://user-images.githubusercontent.com/106061407/176168433-59f7fd54-f9c8-4da0-88ea-38e981d0fff6.png)

saya akan menggunakan direktori /etc/ssl/certs di server untuk menyimpan sertifikat asal. Direktori /etc/ssl/private akan menyimpan file kunci privat. Kedua folder tersebut sudah ada di server.

Pertama, salin isi Sertifikat Asal yang ditampilkan di kotak dialog di browser Anda.

Kemudian, di server Anda, buka /etc/ssl/certs/cert.pem untuk mengedit:

```
sudo nano /etc/ssl/certs/cert.pem
```

![image](https://user-images.githubusercontent.com/106061407/176179383-a9e8f503-c8a7-44fe-90a0-3d325bb31e28.png)

Kemudian kembali ke browser Anda dan salin konten kunci Pribadi. Buka file /etc/ssl/private/key.pem untuk mengedit:

```
sudo nano /etc/ssl/private/key.pem
```
![image](https://user-images.githubusercontent.com/106061407/176179620-f5b61f2a-e8d1-4b32-bb17-ea2a9c844726.png)


Step 2 — Installing the Origin CA certificate in Nginx

Di bagian sebelumnya, saya sudah membuat sertifikat asal dan kunci pribadi menggunakan dasbor Cloudlfare dan menyimpan file ke server saya. Sekarang saya akan memperbarui konfigurasi Nginx untuk situs saya untuk menggunakan sertifikat asal dan kunci pribadi untuk mengamankan koneksi antara server Cloudflare dan server saya.

Nginx membuat blok server default selama instalasi. Hapus jika ada, karena saya telah mengonfigurasi blok server khusus untuk domain :

```
sudo rm /etc/nginx/sites-enabled/default
```

Selanjutnya, buka file konfigurasi Nginx untuk domain Anda:

```
sudo nano /etc/nginx/sites-available/pipeline.alfino.studentdumbways.my.id
```

Selanjutnya  saya membuat config host agar dapat login hanya menggunakan nama host seperti gambar berikut :



![image](https://user-images.githubusercontent.com/106061407/176204705-cdd93ca1-d092-4cfa-92a0-7a95c0944565.png)
