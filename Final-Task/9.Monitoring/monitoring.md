Ansible-playbook untuk monitoring

KET : `prometheus.yml` adalah konfigurasi untuk prometheus

prometheus.yml :

```
global:
 scrape_interval: 10s
scrape_configs:
 - job_name: 'prometheus_metrics'
   scrape_interval: 5s
   static_configs:
     - targets: ['103.171.85.159:9090']
 - job_name: 'node_exporter_metrics'
   scrape_interval: 5s
   static_configs:  
     - targets: ['103.179.56.190:9100','103.226.139.62:9100','103.214.113.81:9100','103.171.85.159:9100']

```

monitoring.yml :

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
           path: /home/monitoring/prometheus
           state: directory

        - name: 'Copy Configuration Prometheus'
          copy:
           src: /home/pino/ansibleku/prometheus.yml
           dest: /home/monitor/prometheus

        - name: 'Login DockerHub'
          docker_login:
           username: pinoezz
           password: <PW KALIAN>

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
           volumes: /home/monitoring/prometheus:/etc/prometheus

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
 
 Pertama-tama saya akan tes ping ke semua server dan cek syntax
 
 ```
 ansible all -m  ping
 ```

```
ansible-playbook --syntax-check monitoring.yml
```

 ![image](https://user-images.githubusercontent.com/106061407/176582943-ef9d72ff-f712-415f-b94a-1db6581cabb6.png)


Jalankan ansible-playbook menggunakan perintah :

```
ansible-playbook monitoring.yml 
```

Saya mendapatkan error karena salah membuat direktori , kemudian saya akan perbaiki dan jalankan ulang ansible-playbook

![image](https://user-images.githubusercontent.com/106061407/176584195-15d57f96-f88b-4bd5-9192-b602fc634c4f.png)

Apabila sudah berhasil di tiap server akan otomatis terinstall node exporter

![image](https://user-images.githubusercontent.com/106061407/176585129-f819e9b9-7f5c-4f51-8fdd-9447053186de.png)

![image](https://user-images.githubusercontent.com/106061407/176585167-9dc59de8-6d88-4c17-a9cc-693afa7ab9f3.png)


Kemudian cek juga pada server monitor

![image](https://user-images.githubusercontent.com/106061407/176585230-20ad3038-e5ef-42ec-9df3-86a32024afb1.png)

KET BERIKUT PORT PADA MONITORING: 
- node exporter [9100]
- prometheus [9090]
- grafana [3000]

Kemudian saya akan cek pada browser

![image](https://user-images.githubusercontent.com/106061407/176586687-a78af39b-b2c1-47cd-86da-71eb604b3355.png)

[NODE EXPORTER OK]

![image](https://user-images.githubusercontent.com/106061407/176587595-b4c6a30d-f5e4-44dc-b799-a530bfeaa2ca.png)

[PROMETHEUS OK]

![image](https://user-images.githubusercontent.com/106061407/176587717-a3ce32bb-1063-4bd6-82b7-49be97337952.png)

[GRAFANA OK]

----------------------------------------------

Kemudian saya akan konfigurasi pada grafana dan berikut adalah hasilnya

![image](https://user-images.githubusercontent.com/106061407/176588847-db36ba80-06d7-444d-95c7-3dd273928226.png)



