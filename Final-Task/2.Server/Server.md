# Create Server

Disini saya akan membuat 4 server dengan spesifikasi

- Server App (Frontend & Backend) or (Frontend, Backend, Database), 2 Core 2Gb RAM
- Server Nginx, 1 Core 1Gb RAM
- Server Monitoring, 1 Core 1Gb RAM
- Server CI/CD , 1 Core 2Gb RAM


![image](https://user-images.githubusercontent.com/106061407/175889635-2a0bec49-78bb-45dc-84ff-9b9b9bd48fd9.png)

![image](https://user-images.githubusercontent.com/106061407/175891816-565a6edd-584a-4d52-8645-cbd1d2bc8ae1.png)

# Install Docker

Untuk instalasi docker saya akan install menggunakan ansible playbook supaya lebih mudah dan cepat

Untuk menggunakan ansible ada beberapa bahan yang diperlukan antara lain :



- Install Ansible di local
- Membuat file keypem yang digunakan supaya ansible dapat mengenali server
- Membuat inventory yang berisi semua ip server target
- Membuat ansible.cfg yang berisi konfigurasi letak dari keypem dan inventory

Tutorial [Ansible](https://github.com/pinoezz/DevOps/tree/master/Stage-2/Week-3/Day-1%262)

Kemudian saya membuat ansible-playbook untuk docker

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


         - name: 'install dependencies'
           apt:
             name:
             - ca-certificates
             - curl
             - gnupg
             - python3-pip
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
           shell: sudo usermod -aG docker pino
```

Saya akan ping terlebih dahulu ke semua server 

```
ansible all -m  ping
```

![image](https://user-images.githubusercontent.com/106061407/176083574-8a68659c-7465-4543-a468-281e7080cf77.png)

Kemudian saya cek juga syntax dari `docker.yml`

```
ansible-playbook --syntax-check docker.yml
```

![image](https://user-images.githubusercontent.com/106061407/176083673-79479176-39ef-42e1-95cb-5aaf313a2d09.png)

Kemudian jalankan ansible-playbook `docker.yml`

```
ansible-playbook docker.yml 
```

![image](https://user-images.githubusercontent.com/106061407/176085324-81718a09-cafe-4182-9ae2-fe3a1d56109f.png)

Kemudian cek docker pada masing masing server 

![image](https://user-images.githubusercontent.com/106061407/176085583-5e6c6a0e-8ed7-4e81-a401-60663ccc5695.png)

-----------------------------------------


ansible-playbook untuk monitoring

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
           path: /home/monitor/prometheus
           state: directory

        - name: 'Copy Configuration Prometheus'
          copy:
           src: /home/pino/ansibleku/prometheus.yml
           dest: /home/monitor/prometheus

        - name: 'Login DockerHub'
          docker_login:
           username: pinoezz
           password: zaq1XSW@212Andra

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
 
 
