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


```
server {
        listen 80;
        listen [::]:80;

        root /var/www/pipeline.alfino.studentdumbways.my.id/html;
        index index.html index.htm index.nginx-debian.html;
 
        server_name pipeline.alfino.studentdumbways.my.id;
 
        location / {
                proxy_pass http://103.214.113.81:8080;
        }
}

```

```
server {

    # SSL configuration

    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    ssl        on;
    ssl_certificate         /etc/ssl/certs/cert.pem;
    ssl_certificate_key     /etc/ssl/private/key.pem;

    server_name pipeline.alfino.studentdumbways.my.id;

    root /var/www/example.com/html;
    index index.html index.htm index.nginx-debian.html;


    location / {
            proxy_pass http://103.214.113.81:8080;
    }
}
```

![image](https://user-images.githubusercontent.com/106061407/176396354-d9602ac2-530e-40d4-9bfd-f17262e54bce.png)





-----------------------------------------------

Saya akan menggunakan SSL Mkcert 

Pertama-tama saya perlu menginstallnya dengan perintah berikut:

```
sudo apt-get install wget libnss3-tools
```

![image](https://user-images.githubusercontent.com/106061407/176401169-35a20eb0-1340-4b47-8960-e85ec1e94371.png)

Selanjutnya download mkcert versi terbaru dari Github.

```
wget https://github.com/FiloSottile/mkcert/releases/download/v1.4.3/mkcert-v1.4.3-linux-amd64
```

![image](https://user-images.githubusercontent.com/106061407/176401373-af7175f7-106b-4d32-98e9-3d912d4c99ff.png)

Setelah mendownload Mkcert, pindahkan biner yang didownload ke sistem:

```
sudo mv mkcert-v1.4.3-linux-amd64 /usr/bin/mkcert
```

Selanjutnya, tetapkan izin eksekusi ke mkcert:

```
chmod +x /usr/bin/mkcert
```

![image](https://user-images.githubusercontent.com/106061407/176401653-671be097-4908-445a-852f-70c1b9227a0b.png)


Sekarang, jalankan perintah berikut untuk menghasilkan sertifikat CA lokal:

```
mkcert -install
```

Untuk melihat letak sertifikat CA menggunakan perintah berikut:

```
mkcert -CAROOT
```

![image](https://user-images.githubusercontent.com/106061407/176401945-f5f78123-ec83-49de-8623-3b5739a77376.png)

Selanjutnya, kita dapat membuat sertifikat dan key file situs web yang dihosting secara lokal menggunakan perintah berikut:

```
mkcert pipeline.alfino.studentdumbways.my.id jenkins 103.214.113.81 ::1
```

![image](https://user-images.githubusercontent.com/106061407/176404146-fb052853-07ac-417e-9cf5-f8ee1ae88288.png)

Selanjutnya, kita perlu mengkonfigurasi Nginx untuk menggunakan sertifikat yang dihasilkan. Pertama, salin file sertifikat yang dihasilkan ke direktori /etc/ssl/:

![image](https://user-images.githubusercontent.com/106061407/176404624-7fe5385e-42ad-4ff3-946a-7881f8d19dc6.png)

Selanjutnya, atur kepemilikan yang tepat ke direktori root web Nginx:

```
chown -R nginx:nginx /var/www/html/
```



![image](https://user-images.githubusercontent.com/106061407/176405634-511f5f47-d97b-4bef-a8ab-dd302529389f.png)


