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

------------------------------

# Membuat direktori untuk menyimpan file/konfigurasi ansible

![image](https://user-images.githubusercontent.com/106061407/174725451-0c60f2ad-5508-4934-8eee-dcf768c65d3c.png)

Untuk nama direktori bebas , disini saya akan buat direktori bernama "ansibleku"

```
mkdir ansibleku
```

---------------------------------

# Membuat SSH keygen 

![image](https://user-images.githubusercontent.com/106061407/174732046-7eefb23c-0bb4-413f-aeb9-81513c276051.png)

Membuat SSH keygen pada server supaya dapat dikenali oleh local

```
ssh-keygen
```

![image](https://user-images.githubusercontent.com/106061407/174735580-e2effd76-7758-4c03-9bed-48f63dce298c.png)


Copy isi dari id_rsa.pub dan pastekan di authorized_keys

![image](https://user-images.githubusercontent.com/106061407/174732582-b89b5a2a-5510-4cd5-8d05-1ba67988b8c5.png)

Kemudian copy id_rsa dan buat file .pem pada local/ansibleku

![image](https://user-images.githubusercontent.com/106061407/174732841-ee3415cf-7788-4576-8718-d5b274a9a225.png)

Lalu save dan exit

![image](https://user-images.githubusercontent.com/106061407/174737222-a174934b-eae5-471c-975c-446a956d6025.png)

Jangan lupa untuk mengubah hak akses file .pemnya menjadi read only kemudian test mengoneksikan ke server

----------------------------------

# Membuat Inventory Ansible

![image](https://user-images.githubusercontent.com/106061407/174740906-24b4235b-f4a9-42ac-a480-b3896c68bfbc.png)

Buat file bernama Inventory kemudian isi dengan ip server kalian

```
[monitoring]
103.55.37.187 ansible_user=monitor
```

-------------------------------------

# Membuat Ansible.cfg

![image](https://user-images.githubusercontent.com/106061407/174750267-ec377191-8cd7-4d06-8f5a-106ad9852c1e.png)
 
Buat file baru bernama ansible.cfg kemudian isi seperti berikut kemudian save
 
 ```
 [defaults]
inventory = Inventory
private_key_file = pino.pem
```
Kemudian cek menggunakan 

![image](https://user-images.githubusercontent.com/106061407/174750581-96ffd40d-a2c5-4d93-a478-b1106e82dc85.png)

```
ansible all-m ping
```

# Install nginx menggunakan ansible-playbook

![image](https://user-images.githubusercontent.com/106061407/174755972-16113ce1-b30b-4faa-a794-edd868fad4b7.png)

Buat file baru bernama nginx.yml

```
- hosts: monitoring
  become: yes
  gather_facts: yes
  tasks:
        - name: 'install nginx'
          apt: 
            name:
             - nginx
            state: latest
 ```
Kemudian saya akan install nginx.yml nya 



