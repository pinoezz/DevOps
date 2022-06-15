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

![image](https://user-images.githubusercontent.com/106061407/173836861-f8d26a2f-ac84-4073-acfe-67d28598a4be.png)


Download images jenkins

```
docker pull jenkins:2.60.3
```

 # Setup work direktory dan run jenkins sebagai container
 
 ![image](https://user-images.githubusercontent.com/106061407/173838453-a8cc855b-c30d-4ba3-9941-d5cdcb9ada5c.png)

```
docker run -d -it -p 8080:8080 -p 50000:50000 --name jenkins -u root:root -v /docker/jenkins:/var/jenkins_home jenkins:2.60.3
```

```
docker ps
```

# Setup jenkins

![image](https://user-images.githubusercontent.com/106061407/173838792-a1992a58-5b20-4534-987d-5f1490402f9d.png)


Setelah jenkins containter run, setup jenkins menggunakan browser. Akses jenkin di http://localhost:8080 

Pada saat pertama kali mengakses jenkins akan meminta password administrator untuk unlock jenkins. Passwordnya ada pada file /docker/jenkins/secrets/initialAdminPassword , kemudian masukan kodenya untuk unlock jenkins

