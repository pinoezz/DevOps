Saya akan mengganti ke branch production terlebih dahulu

![image](https://user-images.githubusercontent.com/106061407/176349334-ef8b535e-4fa0-4c87-a9f6-ea75ea8d8ae6.png)

Edit file `api`.js pada /housy-frontend/src/config untuk menghubungkan app frontend dan backend

![image](https://user-images.githubusercontent.com/106061407/176350029-0649e568-9957-4b5d-b842-7fbc6003c5cb.png)

Edit file `config.json` pada /housy-backend/config untuk menghubungkan backend dengan database

![image](https://user-images.githubusercontent.com/106061407/176350773-85b0fab3-51af-4994-bb11-5b6352ebc133.png)


Selanjutnya membuat dockerfile backend

```
FROM node:dubnium-alpine3.11
WORKDIR /usr/app
COPY . .
RUN yarn install
RUN yarn build
RUN yarn install sequelize-cli -g
RUN npx sequelize db:migrate
EXPOSE 5000
CMD [ "yarn", "start" ]

```

![image](https://user-images.githubusercontent.com/106061407/176650992-f93d3bdf-69c7-4791-9996-12e5c1a193f3.png)


Selanjutnya membuat docker-compose backend

```
version: '3.7'
services:
 backend:
   build: .
   container_name: be
   image: pinoezz/housy-be:stable
   stdin_open: true
   ports:
    - 5050:5000
```

![image](https://user-images.githubusercontent.com/106061407/176355566-b9904f5d-6f84-4e09-b03b-71eac12bdb50.png)

Jalankan `docker-compose.yml` 

```
docker-compose up -d
```

![image](https://user-images.githubusercontent.com/106061407/176361665-0bcd410a-6a0f-439a-afaa-15c1096b2b4d.png)

Kemudian cek pada `docker` 

```
docker ps
```

![image](https://user-images.githubusercontent.com/106061407/176365877-e06494b4-ac2c-4b1a-8762-6a7a4a68190b.png)

Kemudian cek juga pada database apakah sudah berhasil di migrate (Saya akan cek melalui local)

![image](https://user-images.githubusercontent.com/106061407/176366075-b7cf78d7-eb58-42ab-8100-24a7d93f5095.png)

Berhasil migrasi data 

Kemudian saya akan membuat `Dockerfile` frontend

```
FROM node:dubnium-alpine3.11
WORKDIR /usr/app
COPY . .
RUN yarn install
EXPOSE 3000
CMD [ "yarn", "start" ]


```

![image](https://user-images.githubusercontent.com/106061407/176650592-a04398b7-6be9-4a3f-8f2f-9bdcf5291631.png)

docker-compose :

```
version: '3.8'
services:
 frontend:
   build: .
   container_name: fe
   image: pinoezz/housy-fe:stable
   stdin_open: true
   ports:
    - 3030:3000
```

![image](https://user-images.githubusercontent.com/106061407/176432830-17a65beb-8ee0-416c-96f1-c44cb024f472.png)

```
docker-compose up -d
```

![image](https://user-images.githubusercontent.com/106061407/176650684-688c001f-37aa-44e1-ad17-7705fbdb05ba.png)



Saya akan test buat akun

![image](https://user-images.githubusercontent.com/106061407/176441900-af6f0d00-a0fc-4586-8e2b-45e5eb373e6d.png)

