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

![image](https://user-images.githubusercontent.com/106061407/174757260-c557f0bb-068b-4f3d-9b53-6fd416cf9fdc.png)


```
ansible-playbook nginx.yml
```

Kemudian cek pada web browser

![image](https://user-images.githubusercontent.com/106061407/174757425-4834b203-9fff-4bd0-9fdf-789fc64bf7cb.png)

Apabila muncul tampilan seperti diatas maka hasilnya berhasil !!!

------------------------------------------------

# Install Docker menggunakan ansible-playbook

![image](https://user-images.githubusercontent.com/106061407/174772970-5c256505-613e-4781-b200-e34accb7b603.png)

Referensi

https://docs.docker.com/engine/install/ubuntu/

https://docs.docker.com/compose/install/compose-plugin/#installing-compose-on-linux-systems

```
- hosts: monitoring
  become: yes
  gather_facts: yes
  tasks:
         - name: 'update'
           apt:
            update_cache: yes

         - name: 'upgrade'
           apt:
            upgrade: dist


         - name: 'install dependencies'
           apt:
             name:
             - ca-certificates
             - curl
             - gnupg
             - lsb-release

         - name: 'add docker gpg key'
           apt_key:
            url: https://download.docker.com/linux/ubuntu/gpg

         - name: 'add repository docker'
           apt_repository:
             repo: deb  https://download.docker.com/linux/ubuntu focal stable

         - name: 'install docker engine'
           apt: 
            name:
             - docker-ce
             - docker-ce-cli
             - containerd.io
             - docker-compose-plugin

         - name: 'update'
           apt:
            update_cache: yes

         - name: 'install docker-compose'
           shell: curl -SL https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose


         - name: 'set permision for docker'
           shell: sudo chmod +x /usr/local/bin/docker-compose
        
         - name: 'docker without sudo'
           shell: sudo usermod -aG docker monitor


```

Setelah beberapa kali kesalahan akhirnya saya dapat membuat playbook untuk docker dan apabila sukses akan seperti gambar diatas

Kemudian saya akan install docker.yml nya

![image](https://user-images.githubusercontent.com/106061407/174779151-f2ef05c4-e834-49ba-96d0-a3982126d76b.png)

```
ansible-playbook --syntax-check docker.yml 
```

Kemudian saya akan cek hasil install docker pada server

![image](https://user-images.githubusercontent.com/106061407/174779567-63c99cee-ebef-47a5-8d78-31f97ff208fe.png)

Apabila berhasil , dapat menjalankan docker , dan dapat menjalankan docker tanpa sudo

# Install Monitoring server dengan Node Exporter , Prometheus dan Grafana

![image](https://user-images.githubusercontent.com/106061407/174795189-45be4acf-cfdc-4581-abca-2405bf0a42e6.png)

Pertama tama saya akan menginstall docker pada server app  menggunakan ansible-playbook

![image](https://user-images.githubusercontent.com/106061407/174796273-d3c04fcc-8866-42ce-a3e8-1ee7298cf64e.png)

Kirim ssh dari server monitor/local supaya dapat dikenali lokal

![image](https://user-images.githubusercontent.com/106061407/174796432-d78f574e-72ae-42cd-b651-e0b4a4603c50.png)

Kemudian kirim atau masukan id_rsa.pub ke autorized_keys

![image](https://user-images.githubusercontent.com/106061407/174795348-b54caac6-c83b-42ae-b753-ce75b5119267.png)

Kemudian tambahkan user pada inventory

![image](https://user-images.githubusercontent.com/106061407/174796602-a700d697-aff2-4e3b-87c2-f7a64fdcb0fa.png)

Cek koneksi ansible

---------------------------------------------

# Install Docker

![image](https://user-images.githubusercontent.com/106061407/174796982-366fa96e-3c60-4d0b-befd-a0299b5bb1e8.png)

Edit file docker.yml ganti host dan docker without sudo nya menjadi app lalu save

![image](https://user-images.githubusercontent.com/106061407/174797040-e3d51183-186d-4d75-8d37-86a56401f26e.png)

```
- hosts: app
  become: yes
  gather_facts: yes
  tasks:
         - name: 'update'
           apt:
            update_cache: yes

         - name: 'upgrade'
           apt:
            upgrade: dist


         - name: 'install dependencies'
           apt:
             name:
             - ca-certificates
             - curl
             - gnupg
             - lsb-release

         - name: 'add docker gpg key'
           apt_key:
            url: https://download.docker.com/linux/ubuntu/gpg

         - name: 'add repository docker'
           apt_repository:
             repo: deb  https://download.docker.com/linux/ubuntu focal stable

         - name: 'install docker engine'
           apt: 
            name:
             - docker-ce
             - docker-ce-cli
             - containerd.io
             - docker-compose-plugin

         - name: 'update'
           apt:
            update_cache: yes

         - name: 'install docker-compose'
           shell: curl -SL https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose


         - name: 'set permision for docker'
           shell: sudo chmod +x /usr/local/bin/docker-compose
        
         - name: 'docker without sudo'
           shell: sudo usermod -aG docker app
```

```
ansible-playbook docker.yml
```

![image](https://user-images.githubusercontent.com/106061407/174798811-fa96aa1a-72f4-4786-aae3-1368041f30b9.png)

Berhasil install docker di server app 

-----------------------------------------------------------------

# Membuat ansible-playbook Monitoring 

Sekarang setelah berhasil install docker menggunakan ansible-playbook kemudian saya akan membuat ansible-playbook untuk menginstall node_exporter , prometheus dan grafana on top docker

 Referensi : 
 
 [Install Node Exporter](https://medium.com/nerd-for-tech/tutorial-how-to-deploy-prometheus-and-node-exporter-as-containers-on-a-remote-server-with-5-af5b449be49b)

 [Pull Image](https://docs.ansible.com/ansible/2.9/modules/docker_image_module.html)
 
 [Bitnami Prometheus Image](https://hub.docker.com/r/bitnami/prometheus/)
 
 [Docker Create Container](https://docs.ansible.com/ansible/2.5/modules/docker_container_module.html)
 
 [Yaml editor online](https://codebeautify.org/yaml-editor-online)
 
 [Grafana Dashboard](https://grafana.com/grafana/dashboards/)
 
 Pertama-tama membuat file kongigurasi prometheus 
 
 ![image](https://user-images.githubusercontent.com/106061407/174966094-2b86314e-4446-4331-9d13-a9e7da4225c2.png)

File diatas saya simpan di folder ansibleku

```

global:
 scrape_interval: 10s
scrape_configs:
 - job_name: 'prometheus_metrics'
   scrape_interval: 5s
   static_configs:
     - targets: ['103.55.37.187:9090'] #Localhost:port
 - job_name: 'node_exporter_metrics'
   scrape_interval: 5s
   static_configs:  
     - targets: ['103.55.37.187:9100','103.55.37.185:9100'] #Localhost:port
 
```

Berikut adalah file konfigurasi prometheus.yml

![image](https://user-images.githubusercontent.com/106061407/174966869-4c166089-ee6d-4af9-9045-65bcb137a121.png)


Kemudian untuk file Inventory tambahkan [all] (menggabungkan semua user)

```
[all]
103.55.37.187 ansible_user=monitor
103.55.37.185 ansible_user=app

[monitoring]
103.55.37.187 ansible_user=monitor

[app]
103.55.37.185 ansible_user=app
```
NOTE : GANTI IP DIATAS DENGAN IP SERVER KALIAN 

Kemudian saya akan membuat ansible-playbook untuk instalasi Node Exporter , Prometheus dan Grafana

```
- hosts: all
  become: yes
  gather_facts: yes
  tasks:
       - name: 'update'
         apt:
          update_cache: yes

       - name: 'upgrade'
         apt:
          upgrade: dist

       - name: 'Run Node Exporter'
         shell: docker run -d --net="host" --pid="host" -v "/:/host:ro,rslave" --name node_exporter quay.io/prometheus/node-exporter --path.rootfs=/host

- hosts: monitoring
  tasks:
        - name: 'Make volume folder'
          file:
           path: /home/monitor/prometheus
           state: directory

        - name: 'Copy Configuration Prometheus'
          copy:
           src: /home/pino/ansibleku/prometheus.yml
           dest: /home/monitor/prometheus
        
        - name: 'install ptyhon docker'
          shell: sudo apt install python3-docker -y


        - name: 'Login DockerHub'
          docker_login:
           username: {username}
           password: {password}

        - name: 'Pull Prometheus'
          docker_image:
           name: bitnami/prometheus
           source: pull
           

        - name: 'Container Prometheus'
          docker_container:
           name: prometheus
           image: bitnami/prometheus
           ports:
             - 9090:9090
           volumes: /home/monitor/prometheus:/etc/prometheus

        - name: 'Pull Grafana'
          docker_image:
           name: grafana/grafana    
           source: pull

        - name: 'Container Grafana'
          docker_container:
           name: grafana
           image: grafana/grafana
           ports:
             - 3000:3000
```             

Saya akan check file yml apakah sudah valid menggunakan [Yaml editor online](https://codebeautify.org/yaml-editor-online)

![image](https://user-images.githubusercontent.com/106061407/174968381-d49e5588-150c-4eaa-a28a-4c367d29a48c.png)

Apabila hasil seperti ini artinya sudah valid dan untuk mengecek nya jg bisa gunakan perintah 

![image](https://user-images.githubusercontent.com/106061407/174968953-27e0fb69-13b1-498c-b5a5-b540033f5bef.png)

```
ansible-playbook --syntax-check monitoring.yml
```

![image](https://user-images.githubusercontent.com/106061407/174969018-a802b31b-46d6-461a-bdb4-e924f409f013.png)

Selanjutnya running playbook

```
ansible-playbook monitoring.yml 
```

Apabila proses sudah selesai akan seperti gambar diatas kemudian kita cek pada docker di server monitor dan app

![image](https://user-images.githubusercontent.com/106061407/174969548-b9e64353-9d09-442a-851c-b4f69db37e55.png)

![image](https://user-images.githubusercontent.com/106061407/174975264-8821bf51-2317-4aa8-a723-5372d8b1bec8.png)

Semua container sudah berjalan kemudian cek juga pada web browser

![image](https://user-images.githubusercontent.com/106061407/174969712-936ac5d7-0026-42e9-ac42-b91abb3a747e.png)

Node Exporter [OK]

![image](https://user-images.githubusercontent.com/106061407/174969800-743c9563-bb17-4590-a0c6-9bed7c9b62bf.png)

![image](https://user-images.githubusercontent.com/106061407/174969825-1913fe2e-7bcc-4712-8783-579195042237.png)

Prometheus [OK]

![image](https://user-images.githubusercontent.com/106061407/174970073-5018dac9-67d8-4dfc-afa2-5ba295f364f2.png)

Grafana [OK]

Selanjutnya saya akan konfigurasi pada grafana 

![image](https://user-images.githubusercontent.com/106061407/174970313-b7a4a3ac-8e8d-4573-acec-ca233df72657.png)

Masukan username dan password default (admin) / (admin)

Kemudian buat password baru sesuai keinginan kalian lalu submit

![image](https://user-images.githubusercontent.com/106061407/174970569-c6a0f93d-506e-4fdd-92fe-a7de41884dac.png)

Pada tampilan ini kalan "DATA SOURCES"

![image](https://user-images.githubusercontent.com/106061407/174970689-319b4df6-4fc1-41f4-89b6-00ff31a8619a.png)

Kemudian pilih Prometheus

![image](https://user-images.githubusercontent.com/106061407/174970898-06cf601a-62ee-490d-be83-8ce7fce6caf0.png)

Kemudian pada URL kalian isikan IP dan port dari Prometheus

![image](https://user-images.githubusercontent.com/106061407/174970991-ffa8cb43-cb64-443f-8314-0b32d3467215.png)

Save & Test

![image](https://user-images.githubusercontent.com/106061407/174971884-000fd73b-7a91-4745-9f51-20bc05639b14.png)

Kemudian pilih Dashboard dan pilih New Dashboard

![image](https://user-images.githubusercontent.com/106061407/174972071-77f31679-c22a-484e-8b2c-873ddf8a68f5.png)

Pilih add new panel

![image](https://user-images.githubusercontent.com/106061407/174972723-a720a849-ff2c-4c44-9919-3844e55244d0.png)

Disini pilih metric apa yang mau kita monitoring kemudian run queries

![image](https://user-images.githubusercontent.com/106061407/174972897-0a6d0785-3988-4735-812d-57bf4ce7a6e3.png)

Kemudian untuk mengganti tampilan dashboard kalian bisa mengambil template nya di [Grafana Dashboard](https://grafana.com/grafana/dashboards/)

![image](https://user-images.githubusercontent.com/106061407/174974175-0cce7298-a415-4e54-9872-85ccacbfe628.png)

Contoh saya akan gunakan dashboard ini , Klik bagian copy ID to Clipboard [1860]

![image](https://user-images.githubusercontent.com/106061407/174974706-936dfd15-b6e5-42ee-86b8-1291b33ae9e4.png)

Selanjutnya perlu import pada grafana dashboard

![image](https://user-images.githubusercontent.com/106061407/174974785-655fd877-a163-4066-90f0-753a65dec41a.png)

Kemudian load dan pilih prometheus

![image](https://user-images.githubusercontent.com/106061407/174974837-e05623a3-ed72-47f4-9c31-efc21d0a3482.png)

Apabila tampilan seperti ini artinya berhasil di import :D

