# CI/CD With Jenkins

Untuk CI/CD Jenkins saya akan jalankan on top docker dan berikut ansible-playbook `jenkins.yml`.


```
- hosts: jenkins
  become: true
  tasks:
  - name: jenkins volume
    file:
     path: /home/jenkins/jenkins_home
     state: directory
     owner: 1000
     group: 1000
  - name: Pull jenkins
    docker_image:
     name: jenkins/jenkins:latest
     source: pull
  - name: Container jenkins
    docker_container:
     name: jenkins
     image: jenkins/jenkins
     ports:
      - 8080:8080
      - 50000:50000
     volumes: /home/jenkins/jenkins_home:/var/jenkins_home
```

Jalankan ansible-playbook `jenkins.yml`

```
ansible-playbook jenkins.yml
```

![image](https://user-images.githubusercontent.com/106061407/176146570-7fbbebb8-a063-4da2-b9e1-cd98b7aa464b.png)


Kemudian cek pada Server jenkins

![image](https://user-images.githubusercontent.com/106061407/176146725-28df1ca6-c490-4db2-9362-55ffe6cc6d07.png)

Kemudian langkah selanjutnya adalah buka jenkins di web browser 

![image](https://user-images.githubusercontent.com/106061407/176146923-af3315d8-ecf6-4c09-8d6a-d8923ab4f117.png)

Masuk ke direktori `/home/jenkins/jenkins_home/secrets/` kemudian buka `initialAdminPassword`  untuk melihat password administrator

![image](https://user-images.githubusercontent.com/106061407/176147157-1de304e0-9ee9-44ef-8d56-2af095180aa6.png)

![image](https://user-images.githubusercontent.com/106061407/176147364-123281d4-48ba-4baf-92d7-cb2922a2973a.png)

![image](https://user-images.githubusercontent.com/106061407/176147398-23fa3279-b57a-4f1f-ba90-a7a589afcbb9.png)

![image](https://user-images.githubusercontent.com/106061407/176147415-05e4baef-7b0b-4e6c-a56d-13faefe354f5.png)

![image](https://user-images.githubusercontent.com/106061407/176160793-df4983e4-9f6c-4b73-ab25-02bf58621881.png)


Pada dashboard pilih manage jenkins

![image](https://user-images.githubusercontent.com/106061407/176444802-c30bacc1-7692-4e29-b48a-cb35a7a13c18.png)

Kemudian pilih manage plugin 

![image](https://user-images.githubusercontent.com/106061407/176444906-8fd18d4e-40b4-4503-b8f6-51f8564cb4c4.png)

Install beberapa plugin (pipeline, publish over ssh, ssh agent) 

![image](https://user-images.githubusercontent.com/106061407/176444937-9bf1e2c8-e2b6-49f2-a89a-329fd77c7866.png)

lalu install dan restart jenkins

![image](https://user-images.githubusercontent.com/106061407/176447989-f8061197-0a56-45e0-b51c-ec95fc955dd7.png)

Kemudian pilih manage jenkins lalu manage credential dan membuat credential baru 

![image](https://user-images.githubusercontent.com/106061407/176448624-600608f7-4393-4f84-beb1-63357388ca96.png)

![image](https://user-images.githubusercontent.com/106061407/176449169-9d8055a8-1363-4616-8a07-e7b4de9b1c18.png)

KET : Key isi id_rsa server app kalian

Kemudian konfigurasi publish over ssh, masuk ke configure system dan pada bagian publish over ssh, masukkan private key nya dan host server app

![image](https://user-images.githubusercontent.com/106061407/176453312-238d3805-8696-4704-8d03-439b53d2460f.png)


Save dan apply

Sekarang saya akan buat job baru, klik new item dan masukkan nama project kita, disini saya menggunakan freestyle project untuk menggunakan publish over ssh dan pipeline

![image](https://user-images.githubusercontent.com/106061407/176459050-b6faedec-51d8-41ae-8d68-f576f004b26b.png)


Pilih Git

![image](https://user-images.githubusercontent.com/106061407/176459759-acf7d33c-9acb-443b-bd37-c19174d65153.png)


Centang GitHub hook trigger for GITScm polling agar dapat di trigger di perubahan github

![image](https://user-images.githubusercontent.com/106061407/176454326-cd21e7a5-0397-487b-8393-baacf9ab43bb.png)

Kemudian masuk ke github , pada repository pilih `setting`. Kemudian pilih `webook`

![image](https://user-images.githubusercontent.com/106061407/176459992-80fcc033-11b7-4882-8e13-74ea9abebaf2.png)

![image](https://user-images.githubusercontent.com/106061407/176460065-d48b9764-d069-4ba9-837e-72d9f276ffc7.png)

Add webhook

![image](https://user-images.githubusercontent.com/106061407/176460116-f226df3b-9766-4b5f-98aa-b6472b82dd47.png)


![image](https://user-images.githubusercontent.com/106061407/176460903-5eb42891-bfef-4ae9-9433-b9450dba3f08.png)


Save dan apply

----------------------------

Kemudian saya akan membuat pipeline untuk housy-frontend

![image](https://user-images.githubusercontent.com/106061407/176462150-3fb3c4d1-b53b-4c06-818e-c4195a3635d0.png)


![image](https://user-images.githubusercontent.com/106061407/176463520-0eaf1dc7-7475-4c4a-a7cd-d9089e1e6e29.png)

![image](https://user-images.githubusercontent.com/106061407/176463720-9933b507-c30b-4799-b0e4-cdfb48af8aec.png)

Selanjutnya kita perlu membuat jenkinsfile

