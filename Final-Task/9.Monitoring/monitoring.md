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
     - targets: ['103.55.37.187:9090']
 - job_name: 'node_exporter_metrics'
   scrape_interval: 5s
   static_configs:  
     - targets: ['103.55.37.187:9100','103.55.37.185:9100']
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


