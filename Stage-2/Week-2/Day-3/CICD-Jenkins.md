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

![image](https://user-images.githubusercontent.com/106061407/174042621-cdeb7a39-2875-46d2-91c4-0aa1e99bd938.png)


```
docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11
```

# Install Nginx

![image](https://user-images.githubusercontent.com/106061407/174030952-27e3fe6a-837d-458e-aab2-550e506f48b7.png)


```
sudo apt install nginx
```

![image](https://user-images.githubusercontent.com/106061407/174032495-7cfb49aa-eb2d-4c34-b62b-385340f2d9eb.png)

Kemudian cek pada web browser

# Create a new server block 

![image](https://user-images.githubusercontent.com/106061407/174031634-4e8536dd-420c-4681-8da4-d8a9cf3e912b.png)

Sayaakan mempersiakan domai terlebih dahulu

![image](https://user-images.githubusercontent.com/106061407/174032052-30b31120-1772-47f6-a21a-2f400aeab133.png)


```
sudo nano /etc/nginx/conf.d/jenkins.conf
```

```
upstream jenkins{
    server 103.171.85.155:8080;
}
 
server{
    listen      80;
    server_name jenkinsalfino.studentdumbways.my.id;
 
    access_log  /var/log/nginx/jenkins.access.log;
    error_log   /var/log/nginx/jenkins.error.log;
 
    proxy_buffers 16 64k;
    proxy_buffer_size 128k;
 
    location / {
        proxy_pass  http://jenkins;
        proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
        proxy_redirect off;
 
        proxy_set_header    Host            $host;
        proxy_set_header    X-Real-IP       $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header    X-Forwarded-Proto https;
    }
 
}
```
Kemudian save dan exit

Kemudian cek pada web browser

![image](https://user-images.githubusercontent.com/106061407/174033086-3577e94b-b9a5-406f-b36c-8b1188243cd5.png)


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

# Create a job

![image](https://user-images.githubusercontent.com/106061407/173871182-66141bbd-736c-48e0-a0b8-313873577469.png)

Pilih create a job / new item 

![image](https://user-images.githubusercontent.com/106061407/173883310-766dd297-4291-4f21-89ba-7d8b6a014772.png)

Pilih pipeline project lalu ok

![image](https://user-images.githubusercontent.com/106061407/173883429-14f7a781-b54d-44e5-818b-eb10cbdcc8a5.png)

Isi description lalu apply


# Add Credential

Sekarang kita akan mencoba membuat credentials pada jenkins, sehingga nantinya jenkins dapat melakukan clone dan deployment otomatis ke Github. Silahkan pilih menu credentials pada menu jenkins yang berada di bawah enu My views, maka akan muncul menu system yang telah di expand, silahkan pilih menu system tersebut. Lalu pilih domain Global credentials (unrestricted), dan kemudian pilih menu Add Credentials. Untuk user jenkins silahkan isikan seperti berikut

![image](https://user-images.githubusercontent.com/106061407/173869107-fe062ed6-58c5-41c2-9991-16709a64a7ec.png)

Copy id_rsa 

![image](https://user-images.githubusercontent.com/106061407/173869504-471077f0-ac4f-48fe-8eac-21a370b39863.png)

Pilih ssh username with private key

![image](https://user-images.githubusercontent.com/106061407/173870044-fb9efb2e-d83f-4a88-ac88-3c667ba3b8a0.png)

Pastekan id_rsa pada keynya

lalu create

![image](https://user-images.githubusercontent.com/106061407/173870174-9039733f-adcb-42e0-8f5d-9daf33fbdc90.png)

Kemudian saya ingin mencoba untuk me rename jenkins menjadi frontend

![image](https://user-images.githubusercontent.com/106061407/173872683-c060787c-bfcf-4f2e-aad6-09fa07cd161d.png)

![image](https://user-images.githubusercontent.com/106061407/173872744-bdb56e4c-9750-4813-8fb7-9727554a2cb1.png)

![image](https://user-images.githubusercontent.com/106061407/173872784-45985579-8c2f-4ac8-864b-f7d7f9416402.png)

# Integrasi dengan git

Langkah pertama saya akan membuat repository baru pada github

![image](https://user-images.githubusercontent.com/106061407/173873473-e11b03f3-bf90-41ea-a0a2-2f331f8a1f1d.png)


![image](https://user-images.githubusercontent.com/106061407/173874159-8d2c8064-758e-4ce0-8ed8-0ccfc6b03977.png)


Cloning fork https://github.com/dumbwaysdev/wayshub-frontend

Masuk ke direktori wayshub-frontend

![image](https://user-images.githubusercontent.com/106061407/173891858-b1b0e448-5148-4d2c-a7cc-11a5d0a22118.png)

Lalu ubah/tambahkan remote

```
git remote add origin git@github.com:pinoezz/Jenkins-Frontend.git
```

```
git remote -v
```

# Build FE

# Membuat [jenkinsfile](https://www.jenkins.io/doc/pipeline/tour/hello-world/)

![image](https://user-images.githubusercontent.com/106061407/173876637-589efdf2-05b8-4606-a182-3299f5823829.png)

Kemudian masuk ke server jenkins direktori wayshub-frontend lalu buat file jenkinsfile

![image](https://user-images.githubusercontent.com/106061407/173875523-a60a7208-d2b7-4e6b-be4e-f48b0398c362.png)

![image](https://user-images.githubusercontent.com/106061407/173880518-782e35e7-e171-4b43-81b9-a3153e6f614f.png)


```
def secret = 'pinoezz'
def server = 'jenkins.103.171.85.155'
def directory = 'wayshub-frontend'
def branch = 'master'

pipeline{
    agent any
    stages{
        stage ('compose down &  pull'){
            steps{
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker-compose down
                    docker system prune -f
                    git pull origin ${branch}
                    exit
                    EOF"""
                }
            }
        }
        stage ('docker build'){
            steps{
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker-compose build
                    exit
                    EOF"""
                }
            }
        }
        stage ('docker up'){
            steps{
                sshagent([secret]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker-compose up -d
                    exit
                    EOF"""
                }
            }
        }
    }
}

```

Kemudian save dan exit

Selanjutnya add semua , commit dan push ke github

![image](https://user-images.githubusercontent.com/106061407/173881428-d4bcf933-76d7-44b6-b9a4-15baa86ad59c.png)

Kemudian cek di github

![image](https://user-images.githubusercontent.com/106061407/173881487-8b26b6ca-ff35-4783-9e37-cb4615c0e299.png)

# Configure Pipeline

![image](https://user-images.githubusercontent.com/106061407/173881944-77e27220-6320-45c6-96a3-a728b5c46cf5.png)

Masuk ke localhost:8080 (jenkins)

![image](https://user-images.githubusercontent.com/106061407/173882080-3eaf3469-d5cb-4d9e-b136-d1f6ff1aa157.png)

Pada dashboard pilih project (frontend)

![image](https://user-images.githubusercontent.com/106061407/173883914-02568511-435b-476e-a239-8a7db067a596.png)

![image](https://user-images.githubusercontent.com/106061407/173883962-dda85ab9-0f5b-4cde-ae0b-e3b496d608e1.png)


Kemudian apply dan save

![image](https://user-images.githubusercontent.com/106061407/173884057-8e8ce7fe-341a-4d4c-a065-21856ef80ea8.png)

Kemudia pilih build now

![image](https://user-images.githubusercontent.com/106061407/173885251-d3b95d35-90f9-4518-973b-c8ea182d4c87.png)


Untuk melihat log pilih console output

![image](https://user-images.githubusercontent.com/106061407/173885570-f96889cd-31f8-496c-91dc-b9fe1310cfae.png)


![image](https://user-images.githubusercontent.com/106061407/174004196-546f0f05-73b9-4e7c-b2c5-07f7fc642561.png)

Saya mendapatkan error bahwa docker-compose tidak support harus mengganti versi kemudian selanjutnya

Saya upgrade docker compose 

Kemudian

![image](https://user-images.githubusercontent.com/106061407/174005417-74c18f7e-03b1-48c6-96f6-3ad9f43fcfe5.png)

git add . commit dan push , apabila gagal git pull terlebih dahulu 

![image](https://user-images.githubusercontent.com/106061407/174005689-b52d01b5-b6b2-44da-a876-4f18d6e98d76.png)

dan coba build ulang di jenkins

![image](https://user-images.githubusercontent.com/106061407/174006945-ba51c697-5401-4ee1-ae02-8cec1810dde7.png)

Sudah berhasil di build dan deploy selanjutnya saya akan cek image yang barusan dibuat pada docker

![image](https://user-images.githubusercontent.com/106061407/174007470-e4620de5-13bc-46b2-8310-1bec89ec6d0c.png)

```
docker images
```

Muncul image baru "pinoezz/wayshub-fe"

![image](https://user-images.githubusercontent.com/106061407/174010003-6fff9c4c-2e09-4ffd-b520-74a5544e011a.png)

Kemudian cek melalui web browser

![image](https://user-images.githubusercontent.com/106061407/174025513-836206f1-e3fc-4880-a947-6a10554c96db.png)

# Build BE
