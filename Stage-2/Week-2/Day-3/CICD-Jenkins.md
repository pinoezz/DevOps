# CI/CD JENKINS

![image](https://user-images.githubusercontent.com/106061407/173822002-c970a6c2-a1c3-4341-909c-9e22d2db3f60.png)

# Apa itu CI/CD?​

CI/CD atau Continuous Integration dan Continuous Deployment merupakan metode untuk mengirimkan perubahan code secara terus menerus hingga aplikasi dapat release ke publik dengan otomatis.

Continuous integration merupakan proses otomatis untuk memastikan semua code sudah berjalan dengan baik, jika terjadi error maka proses tersebut akan diulangi dari awal hingga code tersebut sudah tidak ada error.

Continuous deployment merupakan proses otomatis agar aplikasi yang telah siap di kirim ke server hingga aplikasi dapat diakses secara public.

# Jenkins

Jenkins merupakan sebuah automasi server berbasis open source yang ditulis menggunakan bahasa Java. Salah satu kegunaan Jenkins adalah untuk mengimplementasikan Continuous Integration dan Continous Delivery atau biasa yang disebut CI/CD proses. lebih jelasnya jenkins memudahkan kita untuk Proses seperti testing, building dan deployment yang dapat dijalankan secara otomatis.

# Membuat VPS menggunakan [IDCloudhost](idcloudhost.com)

![image](https://user-images.githubusercontent.com/106061407/173823119-f32549ec-4e8d-46e3-a8e3-d5add83f063d.png)

Saya akan membuat server dengan OS Ubuntu versi 20.04 LTS yang nantinya akan digunakan untuk Jenkins di dalam docker

![image](https://user-images.githubusercontent.com/106061407/173824476-10520fa7-bb7b-4b7a-861a-443d39c083dd.png)

Apabila aplikasi selesai di build , langsung saja saya login menggunakan terminal

![image](https://user-images.githubusercontent.com/106061407/173832621-a4a0f68f-d91e-4875-90dd-78304ca87d07.png)


# Install Docker

```
sudo apt  install docker.io
```

![image](https://user-images.githubusercontent.com/106061407/173832665-a3a3b9a8-9005-4d83-bb57-7f3e655ba462.png)

Kemudian saya akan memberikan akses root kepada docker supaya saat menjalankan docker tidak perlu menggunakan sudo

![image](https://user-images.githubusercontent.com/106061407/173832877-169d64cc-b2bb-4ff1-9e64-295e78dfcb15.png)

```
sudo usermod -aG docker $user
```
Kemudian relogin

```
logout
```

![image](https://user-images.githubusercontent.com/106061407/173833161-27e4e6a1-7dcd-465f-ba03-42014116a05d.png)

--------

Login Docker

![image](https://user-images.githubusercontent.com/106061407/173833981-3cbbb4e8-62ba-4326-8da5-9e5c5e89e7ae.png)

Lakukan login docker terlebih dahulu 

```
docker login
```

# Install Jenkins on Docker

![image](https://user-images.githubusercontent.com/106061407/173849622-b11bd4e2-3073-4dc0-95f8-d9ccd7e5ba6d.png)


Download images jenkins

```
docker pull jenkins/jenkins
```

# Setup network jenkins

Saya akan membuat network untuk jenkins

![image](https://user-images.githubusercontent.com/106061407/173845076-f24e2fda-f70e-4ab0-bfda-cb1292e5a0c2.png)

```
docker network create jenkins
```

 # Setup work direktory dan run jenkins sebagai container
 
 ![image](https://user-images.githubusercontent.com/106061407/173849794-96a44b9e-7d98-4df0-9fe8-a3fb00f26667.png)

 
 ```
 docker create --name jenkins --network jenkins --publish 8080:8080 jenkins
 ```

![image](https://user-images.githubusercontent.com/106061407/173850149-30033066-2547-46cc-8d64-547a5253f670.png)

 
 Untuk menjalankan jenkins gunakan perintah 
 
 ```
 docker container start jenkins
 ```
 
 # Setup jenkins
 
 ![image](https://user-images.githubusercontent.com/106061407/173845847-4be58ee8-3f20-433c-926f-671cf3c96fe4.png)

Setelah jenkins containter run, setup jenkins menggunakan browser. Akses jenkin di http://localhost:8080.

![image](https://user-images.githubusercontent.com/106061407/173850427-63782e18-5f9c-4040-9939-21aa059904b7.png)

Kemudian masuk ke /var/jenkins_home/secrets/initialAdminPassword pada container jenkins dan buka file initialAdminPassword kemudian copy

![image](https://user-images.githubusercontent.com/106061407/173846762-f942af2b-d938-45e6-9afb-3f031211b7fe.png)

Kemudian pilih install suggested plugins 

![image](https://user-images.githubusercontent.com/106061407/173850825-f7023561-5451-42c7-94b5-22c920c4fa65.png)

Dan tunggu proses hingga selesai

![image](https://user-images.githubusercontent.com/106061407/173853659-9ae2e9d9-f7b4-4a81-b088-933cd8f4050b.png)

Isi semua kolom lalu save and continue

![image](https://user-images.githubusercontent.com/106061407/173854120-537f4c4b-bf22-4933-9f09-c80de3599890.png)

Save and finish

![image](https://user-images.githubusercontent.com/106061407/173854190-86378e5b-b0dd-461c-8dee-d1db2c124d1d.png)

Start using jenkins


# Menghubungkan Github dengan mengirimkan ssh key 

![image](https://user-images.githubusercontent.com/106061407/173855625-273385ab-59e6-4323-b5a8-a3a86f5f04b3.png)

Sebelumnya saya sudah menghubungkan akun github saya dengan ssh local

![image](https://user-images.githubusercontent.com/106061407/173857887-3698f0df-86d9-4d87-ba5f-2a0f10adf650.png)

Buat file authorized_keys sebelum mengirimkan ssh

kemudian saya akan memberikan ssh dari local menuju server jenkins saya

![image](https://user-images.githubusercontent.com/106061407/173859044-5c086f20-b98e-4683-beb0-26a91b9ebee0.png)

```
scp -r id_rsa id_rsa.pub jenkins@103.171.85.155:/home/jenkins/.ssh
```

KET : apabila gagal kalian perlu membuat direktori .ssh pada server jenkins

![image](https://user-images.githubusercontent.com/106061407/173859265-5d7b33df-8bd8-4698-9e84-87a061111606.png)

Kemudian cek ssh di server keygen akan otomatis muncul

![image](https://user-images.githubusercontent.com/106061407/173859328-4d5de41d-6266-449d-82df-be2976951008.png)




