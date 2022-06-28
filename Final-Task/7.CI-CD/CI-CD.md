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
