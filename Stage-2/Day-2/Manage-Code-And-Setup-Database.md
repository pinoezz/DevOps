# SSH

![image](https://user-images.githubusercontent.com/106061407/172600910-c615bda3-6a7c-4b2e-a1b7-ed4eb74019d9.png)

Secure shell atau SSH adalah protokol transfer yang memungkinkan penggunanya untuk mengontrol sebuah perangkat secara remote atau dari jarak jauh melalui koneksi internet yang pastinya aman. Atau bahasa mudahnya adalah sebagai kunci untuk mengakses perangkat

Pada [case sebelumnya](https://github.com/pinoezz/DevOps/blob/main/Stage-2/Day-1/Cloud-Computing-with-IDCH-(IdCloudhost).md) saya sudah membuat suatu aplikasi frontend yang sudah dapat di akses menggunakan domain https://alfino.studentdumbways.my.id/login dan sudah tersertifikasi SSL


![image](https://user-images.githubusercontent.com/106061407/172577620-198f2257-c4f2-4194-a2c3-75b9300c7a1c.png)

# Membuat server backend dan database menggunakan [IdCloudhost](https://console.idcloudhost.com/) 

# Membuat server backend

![image](https://user-images.githubusercontent.com/106061407/172601392-20acfb02-0ea9-4ee0-be3d-7e3acf2c7b3f.png)

Lakukan registrasi atau login 

![image](https://user-images.githubusercontent.com/106061407/172601690-ebe9827c-8fee-48a4-81e1-210266713f83.png)

Kemudian pilih compute dan NEW 

![image](https://user-images.githubusercontent.com/106061407/172602315-b2b60131-e8a7-4b35-a90d-2a953f13ffc1.png)

Saya akan menggunakan ubuntu versi 20.04 LTS Server Indonesia

![image](https://user-images.githubusercontent.com/106061407/172603110-1f23f487-bc1d-4c92-aaa3-d2531f3c2e6c.png)

Kemudian isi username password dan resource name lalu create

![image](https://user-images.githubusercontent.com/106061407/172603271-1dc63de9-e8fc-4798-a45f-56eaaa349ded.png)

Tunggu hingga proses selesai

![image](https://user-images.githubusercontent.com/106061407/172603682-e6281f80-7cb9-4a26-8c1d-451b3f96da30.png)

Apabila sudah selesai saya akan login pada terminal saya

![image](https://user-images.githubusercontent.com/106061407/172603855-dd815694-43f3-4422-a06d-2b4b9e0f4034.png)


# Membuat server database

![image](https://user-images.githubusercontent.com/106061407/172604207-36a4566e-7f6b-4886-ae25-f1ee28c4ce71.png)

Untuk server database juga saya menggunakan ubuntu versi 20.04 LTS

![image](https://user-images.githubusercontent.com/106061407/172604498-1adbe102-0e53-4f28-a5fc-034622d31900.png)

Kemudian isi username password dan resource name lalu create

![image](https://user-images.githubusercontent.com/106061407/172604647-d5a3b271-d849-42f4-9168-3f9455912e0e.png)

Tunggu hingga proses selesai

![image](https://user-images.githubusercontent.com/106061407/172605332-cc29bba4-34f7-4993-ac06-0db9a2386558.png)

Apabila sudah selesai saya akan login pada terminal saya

![image](https://user-images.githubusercontent.com/106061407/172605592-938a4bf2-f9f3-4057-8bdc-8b4f14adf995.png)

# Generate SSH Key dan transfer ke semua server

![image](https://user-images.githubusercontent.com/106061407/172610603-f9fd97ee-47f2-4da3-81cf-51baaa463b93.png)

Pertama tama gunakan ssh-keygen untuk membuat ssh key

```
ssh-keygen
```

![image](https://user-images.githubusercontent.com/106061407/172611219-3419308f-b99d-46c0-8c76-00c0ced47ac1.png)

Kemudian masuk ke direktori .ssh lalu gunakan perintahcat untuk melihat id_rsa.pub

```
cat id_rsa.pub
```

![image](https://user-images.githubusercontent.com/106061407/172611763-dda5db7a-9ffa-401c-be15-df3862a7bba7.png)


![image](https://user-images.githubusercontent.com/106061407/172611607-39629c75-117a-48ef-9b85-a810ba4d58ac.png)

Kemudian buat file authorized_keys dan masukan id_rsa.pub kalian disini lalu save dan exit

![image](https://user-images.githubusercontent.com/106061407/172622706-a23bbc06-50b0-4704-bec5-0daf339d4fd0.png)

Sebelumnya buat terlebih dahulu direktori .ssh pada server frontend

![image](https://user-images.githubusercontent.com/106061407/172622028-ee959230-51a4-4c68-accb-28d2c2fc6214.png)


Kemudian saya akan memigrasikan file ssh id_rsa.pub ke server aplikasi frontend menggunakan perintah scp id_rsa.pub "username"@ip:./


Pada server gateway masukan perintah

```
scp id_rsa.pub aplikasi@103.31.38.84:/home/aplikasi/.ssh/
```

![image](https://user-images.githubusercontent.com/106061407/172622771-524245fc-2bd1-4cc8-aa7a-ddc24bc0c9c3.png)

id_rsa.pub berhasil di migrasi kemudian buat authorized_keys

![image](https://user-images.githubusercontent.com/106061407/172623251-c461e2ea-b5cf-4b4e-a621-3e217f67daff.png)

Masukan id_rsa.pub

Kemudian kita coba login server frontend tanpa password pada server gateway 

![image](https://user-images.githubusercontent.com/106061407/172623656-c89d4722-929d-4649-a8bf-4ebb0efc7acd.png)

Berhasil ya

Kemudian lakukan hal serupa pada ke 3 server lainnya

![image](https://user-images.githubusercontent.com/106061407/172664502-f9244bdc-d796-422e-a174-f02dded8dbd5.png)



# MySQL 

![image](https://user-images.githubusercontent.com/106061407/172576179-ee943b9b-3b38-4cf6-9464-f97ce2c14ae0.png)

MySQL adalah sebuah database management system (manajemen basis data) menggunakan perintah dasar SQL (Structured Query Language) yang cukup terkenal. Database management system (DBMS) MySQL multi pengguna dan multi alur ini sudah dipakai lebih dari 6 juta pengguna di seluruh dunia.


# Membuat server Database menggunakan [IdCloudhost](https://console.idcloudhost.com/) 

![image](https://user-images.githubusercontent.com/106061407/172664926-210ad0ee-2c98-4c76-8ef5-97245ce275b0.png)

# Membuat user baru untuk database

![image](https://user-images.githubusercontent.com/106061407/172666900-6d040ad9-b4d3-4960-8640-a65204130622.png)


Menggunakan perintah adduser untuk menambahkan user

```
sudo adduser mysql
```

![image](https://user-images.githubusercontent.com/106061407/172667228-fbf23b88-0bc5-4ea9-91e2-744933278cb4.png)


Untuk memberikan izin sudo pada user baru gunakan perintah

```
sudo usermod -aG sudo mysql
```

![image](https://user-images.githubusercontent.com/106061407/172667452-8fa3cd7a-ae7b-44e4-bf92-938995e45609.png)


# Menginstall mysql pada server Database

![image](https://user-images.githubusercontent.com/106061407/172667573-ecc517d8-1d6f-4dec-8c75-23acdd29f15a.png)

```
sudo apt update ; sudo apt upgrade
```
![image](https://user-images.githubusercontent.com/106061407/172667664-7fc2956d-32ea-4079-93cf-9bf70c15c25e.png)

```
sudo apt install mysql-server
```

![image](https://user-images.githubusercontent.com/106061407/172668800-e738057d-cdae-4acb-bb6d-cdf427de0198.png)


Untuk instalasi baru MySQL, Anda akan menjalankan skrip keamanan DBMS yang disertakan. Skrip ini mengubah beberapa opsi asali yang kurang aman untuk hal-hal seperti log masuk root jarak jauh dan pengguna sampel.

![image](https://user-images.githubusercontent.com/106061407/172743210-e9c2a673-eeb7-4e21-a86c-f327a0d091b6.png)

Untuk instalasi mysql gunakan perintah

```
sudo apt get install mysql-server
```


![image](https://user-images.githubusercontent.com/106061407/172742646-88b9cfd3-b619-4a70-be21-d398403d55b4.png)

Untuk melihat versi gunakan perintah 

```
mysql --version
```

Untuk masuk ke mysql gunakan perintah

```
sudo mysql -u root
```
![image](https://user-images.githubusercontent.com/106061407/172743618-43ab0597-de12-4e7e-a533-ae9b2b7737b0.png)


Jalankan skrip keamanan dengan sudo (Keluar terlebih dahulu dari mysql)

```
sudo mysql_secure_installation

```
kemudian isi password yang akan kalian inginkan

![image](https://user-images.githubusercontent.com/106061407/172769267-c796a58b-8f98-4d34-821f-8e6a7f06ec88.png)

Lalu login ulang menggunakan password dengan

```
sudo mysql -u root -p
```

# Membuat Database Baru pada user baru
![image](https://user-images.githubusercontent.com/106061407/172772387-336b9634-6127-4ceb-9032-665fb4c81f61.png)


![image](https://user-images.githubusercontent.com/106061407/172772128-3d3cda41-191a-4be5-ae32-9beabf10a936.png)


Untuk membuat pengguna yang dapat terhubung dari host mana pun, gunakan wildcard ‘%‘ sebagai bagian host:

```
CREATE USER 'user_database'@'%' IDENTIFIED BY 'password_user';
```

Opsi ini biasanya digunakan oleh para webmaster yang menginginkan MySQL server ditempat terpisah dengan web server.

![image](https://user-images.githubusercontent.com/106061407/172772292-70c3617c-66f1-4904-8e6e-43269620b2e8.png)


Memberikan semua hak istimewa ke akun pengguna untuk semua database :

```
GRANT ALL PRIVILEGES ON *.* TO 'user_database'@'localhost';
```

Kemudian 
```
FLUSH PRIVILEGES;
```


![image](https://user-images.githubusercontent.com/106061407/172773159-db2afa08-3a40-4faa-8573-6d60d531f27f.png)

Kemudian saya login dengan user baru yang tadi di buat

![image](https://user-images.githubusercontent.com/106061407/172773698-6b19db6c-0f99-4536-865c-56f391a3f343.png)

```
SELECT user,host FROM mysql.user;
```

# Membuat database wayshub pada mysql

![image](https://user-images.githubusercontent.com/106061407/172792201-307934c0-174b-416d-b708-3f63de4d181d.png)

```
CREATE DATABASE wayshub;
```

Untuk melihat isi dari database gunakan perintah

```
show databases;
```

# Mengganti bind address

Fungsi melakukan bind address yaitu supaya database dapat di akses oleh client

![image](https://user-images.githubusercontent.com/106061407/172782841-369a03a8-76ec-4350-88d9-707f308f0485.png)

![image](https://user-images.githubusercontent.com/106061407/172783781-d23177f9-3d44-43e6-9f5f-944aea3aa778.png)


```
bind-address            = 0.0.0.0  
mysqlx-bind-address     = 0.0.0.0 
```

![image](https://user-images.githubusercontent.com/106061407/172789706-20e88bbc-20f8-4452-b5c9-e97991e0fcda.png)


Lalu restart mysql

```
systemctl restart mysql.service
```

# Dapat meremote database dari client

![image](https://user-images.githubusercontent.com/106061407/172869783-e0e14126-a082-45e6-9b4a-c8096088beca.png)

```
sudo apt install mysql-client
```

Gunakan perintah diatas untuk menginstall mysql untuk client supaya client dapat meremote database

![image](https://user-images.githubusercontent.com/106061407/172870449-e920ba26-36f3-4e5d-98ad-7471373a7149.png)


```
mysql -u alfino -h 116.193.190.66 -p
```

# Deployment

Cloning fork https://github.com/dumbwaysdev/wayshub-backend

![image](https://user-images.githubusercontent.com/106061407/172870730-7565b778-4a34-45b6-8284-fac98c0af0ed.png)

```
git clone https://github.com/dumbwaysdev/wayshub-backend
```

Mengubah direktori menjadi backend dan deploy aplikasi menggunakan PM2

![image](https://user-images.githubusercontent.com/106061407/172871098-a60d1394-bf1e-421e-9f2d-24ba95ea89b6.png)

![image](https://user-images.githubusercontent.com/106061407/172871171-f9e08e3a-4192-4a97-bba5-ba95f6374359.png)

Karena disini saya akan mendeploy aplikasi frontend dengan konfigurasi node js jadi terlebih dahulu saya akan menginstall NPM (Node Package Manager) dan NVM (Node Version Manager) terlebih dahulu

![image](https://user-images.githubusercontent.com/106061407/172871460-ed898b95-b1ed-440c-9b54-4b189a04ef87.png)


```
sudo apt install npm
```

![image](https://user-images.githubusercontent.com/106061407/172871622-91fa5564-6b84-45c8-8d14-ddf312468b24.png)


Selanjutnya saya akan Install NVM (Node Version Manager) menggunakan link di bawah ini

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```

```
exec bash
```

![image](https://user-images.githubusercontent.com/106061407/172871718-dc1b754a-e36f-4794-8f0e-a27102fbf48f.png)

![image](https://user-images.githubusercontent.com/106061407/172871845-b288bfcc-4698-4e92-8e8b-5103e112b9c9.png)


# Migrasi data backend ke Database

![image](https://user-images.githubusercontent.com/106061407/172873243-e24b61b3-f884-48b7-8765-fd9cc6723c32.png)


![image](https://user-images.githubusercontent.com/106061407/172873199-c09e051f-5ff7-4855-a36b-32b36116352e.png)

Edit file config.json pada /backend/config

![image](https://user-images.githubusercontent.com/106061407/172872658-0e9ae5b1-0ab5-4780-bad1-c1449859125e.png)

```
npm install -g sequelize-cli
```

![image](https://user-images.githubusercontent.com/106061407/172872976-035ad8e9-1ce8-4d8a-a7f8-530b3090a126.png)

```
npx sequelize db:migrate
```
Setelah itu cek pada database

![image](https://user-images.githubusercontent.com/106061407/172874301-b895ba76-45cf-497a-99f0-5098414c4fd7.png)

Proses migrasi berhasil

# Install PM2

![image](https://user-images.githubusercontent.com/106061407/172875264-319dd47a-07cd-4151-9d5d-cc1143fb8e66.png)


Untuk [Instalasi PM2](https://pm2.keymetrics.io/docs/usage/quick-start/) gunakan perintah

```
npm install pm2
```

Kemudian kita perlu membuat file ecosystem untuk menjalankan backend

![image](https://user-images.githubusercontent.com/106061407/172875609-968d0023-3ff3-400d-8388-9da0d7088837.png)

```
pm2 ecosystem simple
```
![image](https://user-images.githubusercontent.com/106061407/172875809-1a71d0e4-17d6-4336-a6b1-a30384a5ac09.png)


![image](https://user-images.githubusercontent.com/106061407/172875769-9938bc29-a634-414a-8afa-2019f6a6563a.png)

```
module.exports = {
  apps : [{
    name   : "backend-wayshub",
    script : "npm start"
  }]
}
```

Lalu jalankan pm2 menggunakan perintah

![image](https://user-images.githubusercontent.com/106061407/172876142-0e2f1aeb-fb93-4e4a-8444-679c5f242ab3.png)


```
pm2 start ecosystem
```

![image](https://user-images.githubusercontent.com/106061407/172876247-d3288706-2e55-4829-b576-4ebedbca55bc.png)

# Mengoneksikan aplikasi frontend dan backend

Sebelum mengoneksikan aplikasi frontend dan backend kita perlu mengatur domain untuk backend

![image](https://user-images.githubusercontent.com/106061407/172877512-c66ce321-c9e3-4894-a48f-d7989c60fc6b.png)

Disini saya menggunakan domain dari [CloudFlare](cloudflare.com) , ke menu dns dan buat domain

Domain yang saya buat untuk backend yaitu api.alfino.studentdumbways.my.id 

Kemudian saya akan membuat reverse proxy untuk server backend menggunakan domain api.alfino.studentdumbways.my.id 

![image](https://user-images.githubusercontent.com/106061407/172878244-45843397-d284-46e6-bbd6-4b0d0d01e854.png)

buka direktori /etc/nginx/dumbways kemudian buat file reverse proxy baru 

```
server { 
        server_name alfino.api.studentdumbways.my.id; 

        location /{
        proxy_pass http://103.172.204.30:5000;
        }
}

# Menggunakan SSL CertBot untuk memperaman website

#Apa itu SSL ?

SSL adalah singkatan dari Secure Socket Layer, salah satu komponen penting yang harus dimiliki website. Dengan SSL, transfer data di dalam website menjadi lebih aman dan terenkripsi. Bahkan saking pentingnya, Google Chrome melabeli website tanpa sertifikat SSL sebagai Not Secure.

Apabila sistem keamanan ini ditambahkan pada website Anda, maka URL website akan berubah menjadi HTTPS. Tujuan utama pemasangan SSL adalah sebagai pengaman pertukaran data yang terjadi melalui jaringan internet.

![image](https://user-images.githubusercontent.com/106061407/172879121-1e1b3ff6-30e7-4360-a5f7-80a826309b13.png)


```
sudo snap install core; sudo snap refresh core
```


![image](https://user-images.githubusercontent.com/106061407/172879269-e3888f57-d600-40dd-9680-953cf10d9be6.png)



```
sudo snap install --classic certbot
```


Jalankan certbot menggunakan perintah


```
sudo certbot
```


![image](https://user-images.githubusercontent.com/106061407/172879457-01794678-ebb6-4df7-ba67-e4b2029001a8.png)

Pilih No 2

Lalu kita cek lagi file proxy nya

![image](https://user-images.githubusercontent.com/106061407/172879720-3cbba1b1-32c9-4a7b-a70d-73396d9ea9b2.png)

Konfigurasi SSL / HTTPS pada server backend berhasil


---------------------------

![image](https://user-images.githubusercontent.com/106061407/172876741-eae2c42e-1575-47b7-9919-d2fef1b47c03.png)

Masuk ke server frontend kemudian masuk pada direktori wayshub-frontend

![image](https://user-images.githubusercontent.com/106061407/172876883-6d4a1a39-6125-454b-b377-a4a12ad005a7.png)

Masuk pada direktori aplikasi/wayshub-frontend/src/config kemudian edit file api.js , isi gunakan domain backend

```
import axios from 'axios';

const API = axios.create({
    baseURL: "https://api.alfino.studentdumbways.my.id/api/v1"
});

const setAuthToken = (token) => {
    if(token){
        API.defaults.headers.common['Authorization'] = `Bearer ${token}`;
    } else {
        delete API.defaults.headers.common['Authorization'];
    }
}

export {
    API,
    setAuthToken
}
```

![image](https://user-images.githubusercontent.com/106061407/172880246-e0a1db1e-d60e-43e5-ac95-43d38ef30bff.png)

Kemudian tes menggunakan web browser dan registrasi

![image](https://user-images.githubusercontent.com/106061407/172880646-b04d3022-2f6e-45a2-b3c0-82f1eedf8ead.png)

![image](https://user-images.githubusercontent.com/106061407/172880668-26deabbd-a1a2-4c39-9ffd-3b088d0b63c2.png)

![image](https://user-images.githubusercontent.com/106061407/172880697-bfa17813-0e97-494a-97ac-bc7d6b3c7b93.png)

![image](https://user-images.githubusercontent.com/106061407/172880730-b52fff8b-5414-4d49-b2a2-c688ca7252c4.png)

![image](https://user-images.githubusercontent.com/106061407/172880819-0449670c-c858-4a68-b175-63726b0a858e.png)

Semua berjalan normal apabila tidak ada error

