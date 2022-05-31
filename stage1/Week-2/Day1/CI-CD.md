Cloudflare adalah salah satu layanan Content Delivery Network (CDN) yang mempunyai fitur yang lebih baik dari standar CDN dan merupakan sebuah layanan web security. Layanan ini didapatkan dengan mudah dan memiliki tarif yang gratis

registrasi Clouflare

https://dash.cloudflare.com/

![image](https://user-images.githubusercontent.com/106061407/171104648-410e465a-bf9b-4aa1-aa6f-ac38c5836edd.png)


Kemudian membuat repository pada github

![image](https://user-images.githubusercontent.com/106061407/171104861-85244540-d8e8-4a7d-9839-f333bfb8da7c.png)

Create new repository

![image](https://user-images.githubusercontent.com/106061407/171104927-6557137a-e302-4717-8a0c-dba5005e5c63.png)

![image](https://user-images.githubusercontent.com/106061407/171104952-c4f6f176-a156-4c9e-a8c2-4d29c26f642b.png)

![image](https://user-images.githubusercontent.com/106061407/171105229-7b0e5570-0337-4291-9c7f-5d623d3eec2e.png)

Selanjutnya kalian buat direktori baru , contohnya disini saya membuat direktori bernama cicd
lalu saya akan mengcloning fork repository yang sudah di sediakan

```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

![image](https://user-images.githubusercontent.com/106061407/171105519-dadd81c6-ed4e-42cb-96b4-cd8e9304a21e.png)

Selanjutnya git init

![image](https://user-images.githubusercontent.com/106061407/171105602-8b065f45-eec3-4ee4-8812-2c7427af2739.png)

![image](https://user-images.githubusercontent.com/106061407/171105760-630437ae-ffcb-4cbe-9b34-fff744a448a6.png)

Selanjutnya



![image](https://user-images.githubusercontent.com/106061407/171107428-f7657963-3bc9-42c2-9103-af178612a149.png)

![image](https://user-images.githubusercontent.com/106061407/171107576-62c7f0ab-2c6a-4d9d-8ad1-c4a46a4422e2.png)


Selanjutnya kita buka https://dash.cloudflare.com/ lalu pilih pages dan create project

![image](https://user-images.githubusercontent.com/106061407/171107874-2d72c9ff-8088-4656-b6ad-833f3d715d34.png)

Kemudia pilih repository nya

![image](https://user-images.githubusercontent.com/106061407/171108043-c7d774e1-cfc3-48db-8f14-fca57f4aaaac.png)

![image](https://user-images.githubusercontent.com/106061407/171108351-6ac9c879-a3a4-4878-b9e3-be1e43a32023.png)

![image](https://user-images.githubusercontent.com/106061407/171109652-1875e9e4-7361-410c-997b-2b99bfea983c.png)


![image](https://user-images.githubusercontent.com/106061407/171108379-c03aa1d5-d751-416f-85c5-06193ef544e2.png)

Berikut adalah proses deploy aplikasi kita harus menunggu hingga proses selesai

![image](https://user-images.githubusercontent.com/106061407/171108588-27171872-6796-4647-96a7-28e05287c945.png)

Pilih continue to project

![image](https://user-images.githubusercontent.com/106061407/171108665-dcfa0f38-0cd8-41e2-9b6b-e0842bb171c1.png)

![image](https://user-images.githubusercontent.com/106061407/171110041-7bea0a92-546e-4d46-982e-b56e7669e29e.png)


![image](https://user-images.githubusercontent.com/106061407/171110104-e3be8386-c229-45c2-b188-78725476ed73.png)

![image](https://user-images.githubusercontent.com/106061407/171110142-fba454db-d0d8-4d64-a50a-27c28e4e4a71.png)

Kemudian saya akan melakukan perubahan pada file /public/index.html bagian <title>WaysHub</title> menjadi <title>WaysHub - Nama Anda</title>

![image](https://user-images.githubusercontent.com/106061407/171110279-d4875b3b-c8cd-4f46-9b26-8adbdef03a12.png)

Buka repo CI-CD lalu pilih index.html

![image](https://user-images.githubusercontent.com/106061407/171110437-bbf2f772-ded4-4458-b5f4-91dad24806d5.png)

Lalu pilih edit file

![image](https://user-images.githubusercontent.com/106061407/171110672-8a81d30e-2f1e-4767-a105-10791e0f983d.png)

Kemudian commit change

Kembali lagi ke website cloudflares

![image](https://user-images.githubusercontent.com/106061407/171110895-e765379c-366e-4b32-aecf-ead2c0dcf30d.png)

Akan otomatis mendeteksi adanya perubahan pada aplikasi sebelumnya karena saya sudah mengganti title 

![image](https://user-images.githubusercontent.com/106061407/171111026-74b34721-759a-4d1c-8ba1-3ef9209607cb.png)

![image](https://user-images.githubusercontent.com/106061407/171111367-6fce4995-32f4-4bed-a8ad-cb9fc3d2a338.png)

Untuk hasil akhir akan jadi seperti ini

