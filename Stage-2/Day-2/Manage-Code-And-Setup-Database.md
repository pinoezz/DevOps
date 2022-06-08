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

Jalankan skrip keamanan dengan sudo:

```
sudo mysql_secure_installation
```

