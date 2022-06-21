# Server Monitoring On Docker Using Ansible

![image](https://user-images.githubusercontent.com/106061407/174720424-cc037e82-16dd-4bac-9814-8dd1f2bfd007.png)

Monitoring server adalah kegiatan memantau sumber daya sistem server seperti: penggunaan CPU (CPU Usage), konsumsi memori (Memory RAM Consumption), jaringan, penggunaan disk (disk usage), dan lain sebagainya. Karena performa aplikasi atau website Anda sebagian besar bergantung pada performa server

Untuk task kali ini saya akan membuat suatu konfigurasi Monitoring server dan untuk semua instalasinya saya akan membuat menggunakan  Ansible

![image](https://user-images.githubusercontent.com/106061407/174721548-a0314e59-993d-43e5-8b7c-08cd3baf490a.png)

Menggunakan Ansible untuk Mengelola Server yang Lebih Mudah

Ansible adalah sebuah provisioning tool yang dikembangkan oleh RedHat. Dimana kamu dapat mencatat setiap proses deployment ataupun konfigurasi yang biasa dilakukan berulang - ulang terhadap beberapa server. Misal saat pertama kali kita memasang Ubuntu Server di 10 mesin, maka kita akan melakuan apt-get update serta memasang beberapa komponen seperti PHP5 dan Apache2. Sebenarnya tidak akan menjadi masalah, bila kita hanya melakukan sedikit hal. Tapi bayangkan bila harus melakukan konfigurasi yang cukup kompleks dan dilakukan secara berulang - ulang ke 10 mesin tersebut.

-------------------------------

# Skema Monitoring server

![image](https://user-images.githubusercontent.com/106061407/174721932-06833e54-aebe-4a2b-be9b-7985e78f1fc6.png)

Berikut adalah skema yang akan di bangun, jadi saya akan membuat skema diatas menggunakan server dari [IDCloudHost](https://console.idcloudhost.com/) dan akan berjalan menggunakan docker

--------------------------------

# Membuat VPS (Virtual Private Server) [IDCloudHost](https://console.idcloudhost.com/)

![image](https://user-images.githubusercontent.com/106061407/174722768-5789ae6d-a550-4795-b68a-6b8407d303c2.png)

Pertama-tama saya akan membuat 2 buah server yaitu server mentoring dan app menggunakan os Ubuntu 20.04 LTS

![image](https://user-images.githubusercontent.com/106061407/174723311-1398b777-7b79-448e-ace5-5134a08d4baa.png)

# Membuat Konfigurasi Ansible untuk install docker 

![image](https://user-images.githubusercontent.com/106061407/174724125-c2b44a9c-bb4b-4a89-8c79-a0a499f67591.png)

Install Ansible 

```
sudo apt install ansible
```

---------------------------------

![image](https://user-images.githubusercontent.com/106061407/174724230-224de96a-c147-4baf-a12f-fc5e6ab0402c.png)

Cek versi ansible

```
ansible --version
```
