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


