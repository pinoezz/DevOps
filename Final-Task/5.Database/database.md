# Setup database SQL with PostgreSQL

Saya akan gunakan ansible-playbook untuk instalasi postgresql on top docker

berikut ansible-playbook postgre :

```
#Run Postgresql container

 - hosts: app
   gather_facts: yes
   tasks:
    - name: Start docker service
      service:
        name: docker
        state: started

    - name: install pip dependencies
      pip:
        name: docker
 
    - name: Create Postgres Container
      docker_container:
        name: postgres
        image: postgres:alpine3.16
        state: started
        recreate: yes
        ports:
          - "5432:5432"
        volumes:
          - /home/hitch_postgres_data:/var/lib/postgresql/data
        env:
          POSTGRES_USER: "admin"
          POSTGRES_PASSWORD: "P4ssw0rd"
  ```
  
Saya akan ping dan cek syntax terlebih dahulu 

![image](https://user-images.githubusercontent.com/106061407/176099429-de1c3569-3c60-4892-a5cb-32b2e96675f8.png)

Kemudian jalankan ansible-playbook `postgresql.yml`

```
ansible-playbook postgresql.yml
```

![image](https://user-images.githubusercontent.com/106061407/176100378-83192d50-be93-42a3-95a3-e130bfa18c9a.png)

Selanjutnya cek di docker server app 

![image](https://user-images.githubusercontent.com/106061407/176101418-73a5c09b-64f3-4e4f-aaf0-0c5a5ce5594e.png)


Selanjutnya saya akan membuat database baru bernama `housy`

```
CREATE DATABASE housy;
```

![image](https://user-images.githubusercontent.com/106061407/176104976-a9e48639-0acf-4970-90c1-4de1945505d8.png)

Selanjutnya saya akan menambah user baru  dan berikan privileges atau izin user ke database

![image](https://user-images.githubusercontent.com/106061407/176105746-a8f64771-f7c9-4432-9da3-f623c7b015a7.png)

![image](https://user-images.githubusercontent.com/106061407/176108135-a7f0a4a8-1128-485b-adf2-782eebe36e41.png)


Kemudian masuk postgresql menggunakan user dan database baru 

```
docker exec -it postgres psql -d housy -U pino
```

![image](https://user-images.githubusercontent.com/106061407/176107692-836dc78e-3e60-41f5-9a85-c3ae6e7971f6.png)
