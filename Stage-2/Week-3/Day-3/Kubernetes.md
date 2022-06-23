# Kubernetes 

![image](https://user-images.githubusercontent.com/106061407/175206118-a6b8588e-ee85-4235-8cfd-57134e2e2a33.png)

Kubernetes adalah platform open source untuk mengelola kumpulan kontainer dalam suatu cluster server. Platform ini pertama kali dikembangkan oleh Google dan kini dikelola oleh Cloud Native Computing Foundation (CNCF) sebagai platform manajemen kontainer yang cukup populer.

Kontainer sendiri adalah environment dengan sumber daya, CPU, dan sistem file untuk satu aplikasi. Jadi, aplikasi tersebut akan memiliki sumber daya sendiri. Keuntungannya, aplikasi jadi tidak mudah mengalami downtime.

Atau singkatnya KUBERNETES itu adalah salah satu aplikasi opensource  untuk automation scaling dan manajemen aplikasi berbasis container

![image](https://user-images.githubusercontent.com/106061407/175206855-649823c2-c1dd-4e27-9bda-53576bd8ecad.png)

Untuk konsep cara kerja dari kubernetes adalah seperti di atas atau spesifiknya :

# KUBERNETES MASTER :

Kube-apiserver bertugas sebagai API yang digunakan untuk berinteraksi dengan Kubernetes Cluster

Etcd bertugas untuk sebagai database untuk menyimpan data Kubernetes Cluster

Kube-scheduler bertugas untuk memperhatikan aplikasi yang kita jalankan dan meminta Node untuk menjalankan aplikasi yang kita jalankan

Kube-controller-manager bertugas melakukan kontrol terhadap Kubernetes Cluster

Cloud-controller-manager bertugas untuk melakukan kontrol terhadap interaksi dengan cloud provider

# Kubernetes Nodes : 

Kubelet berjalan di setiap Node dan bertugas untuk memastikan bahwa aplikasi kita berjalan di Node

Kube-proxy berjalan di setiap Node dan bertugas sebagai proxy terhadap arus network yang masuk ke aplikasi kita dan sebagai load balancer juga

Container-manager berjalan di setiap Node dan bertugas sebagai container manager. Kubernetes mendukung beberapa container manager seperti Docker, containerd, cri-o, rktlet, dan yang lainnya.

-----------------------------------

Cluster: Beberapa server yang seolah-olah dijadikan 1 kesatuan sehingga tercipta lingkungan server yang dinamis.

Node / Worker: Merupakan server-server yang dijadikan cluster, berguna untuk menjalankan container

Pods: Satuan terkecil dalam kubernetes yang berguna sebagai pembungkus container. Biasanya dalam 1 pods terdapat 1 container atau lebih.

Containers: Aplikasi yang berjalan di dalam pods seperti halnya docker container, dimana semua kebutuhan untuk aplikasi sudah berada di dalam container tersebut.

CNI: Container Network Interface merupakan penghubung antara cluster, worker, container, volume dan sebagainya. Beberapa cni yang terkenal adalah calico, flannel, weavenet, canal

Persistent Volume: Sama halnya seperti docker volume yang sifatnya untuk menyimpan data di local server.

Ingress: Merupakan cara untuk supaya aplikasi dapat diakses menggunakan http / https, biasanya dalam bentuk domain seperti https://subdomain.example.co

-----------------------------------

# Setup Kubernetes And Deploy Microservices

Sebelumnya apa itu Microservices? Microservices adalah kebalikannya dari Monolith, dimana aplikasi dipecah menjadi kecil-kecil, dimana tiap aplikasi hanya mengurus satu tugas dengan baik, dan semua aplikasi saling berkomunikasi.

Sekarang saya akan mempersiapakan 3 server (1 Manager / sebagai controller) , (2 Worker) dari [IdCloudHost](idcloudhost.com)

![image](https://user-images.githubusercontent.com/106061407/175207641-ce3c5dec-9964-4e4a-96c1-ecbd2ea092d4.png)

![image](https://user-images.githubusercontent.com/106061407/175207791-e8751bb7-3d6b-4332-8835-3f2c36575800.png)


Untuk Manager saya gunakan CPU 2 Core, RAM 4 GB, SSD 20 GB

Untuk masing-masing worker saya gunakan CPU 1 Core, RAM 1GB, SSD 20 GB

![image](https://user-images.githubusercontent.com/106061407/175208025-2abab260-c644-4b52-9614-4485328fc8cc.png)

Tunggu hingga proses building selesai ...

![image](https://user-images.githubusercontent.com/106061407/175208197-ee22d02f-0447-475d-94ea-6941e2ac3dd5.png)

Test login menggunakan terminal

-----------------------------

# Install Docker & Kubernetes

Sebelum melakukan instalasi kubernetes diwajibkan terlebih dahulu untuk NON-Aktifkan firewall dan SWAP

![image](https://user-images.githubusercontent.com/106061407/175208485-b5913de6-a2c9-4b69-9037-1c8fe02081ea.png)

```
ufw disable
```

```
swapoff -a; sed -i '/swap/d' /etc/fstab
```

kemudian kita perlu juga update kernel

![image](https://user-images.githubusercontent.com/106061407/175209233-edb3389e-6712-4568-9a7f-7be4353b190b.png)

```
cat >>/etc/sysctl.d/kubernetes.conf<<EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
```

Kemudian Restart system

![image](https://user-images.githubusercontent.com/106061407/175210657-962d782a-211a-4381-98c3-6fec4fa20deb.png)

```
sysctl --system
```

--------------------------------------------

KETERANGAN : Dikarenakan saya sudah menambahkan catalog Docker pada saat pembuatan server jadi saya tidak perlu install docker lagi

Untuk Instalasi docker kalian dapat ikuti tutorial di bawah ini :

[Install Docker](https://docs.docker.com/engine/install/)

[Install Docker Compose](https://docs.docker.com/compose/install/)

![image](https://user-images.githubusercontent.com/106061407/175212482-5ad79a98-7496-4e74-bf70-0b1413b515fa.png)

Saat ini saya gunakan Docker Version:  20.10.7

-------------------------------------------------------

Selanjutnya saya akan konfigurasi docker daemon

![image](https://user-images.githubusercontent.com/106061407/175217228-dcad2a7d-fd12-4570-b0fa-cd7f67d0c47a.png)

```
cat <<EOF | sudo tee /etc/docker/daemon.json
{
"exec-opts": ["native.cgroupdriver=systemd"],
"log-driver": "json-file",
"log-opts": {
"max-size": "100m"
},
"storage-driver": "overlay2"
}
EOF
```

Lalu restart docker

![image](https://user-images.githubusercontent.com/106061407/175217538-a3efe1aa-c970-438e-8e59-eeef5199bf21.png)

```
sudo systemctl enable docker
sudo systemctl daemon-reload
sudo systemctl restart docker
```

![image](https://user-images.githubusercontent.com/106061407/175217606-e98f3092-4224-478c-984d-26c5cfe9f598.png)

-----------------------------------------------

Selanjutnya Instalasi Kubernetes dan sekaligus install kubelet kubeadm kubectl

![image](https://user-images.githubusercontent.com/106061407/175219579-ed8d1629-df38-419a-bfa7-854f7ebfc70b.png)

```
sudo apt-get update && sudo apt-get install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
sudo apt-get update
```

![image](https://user-images.githubusercontent.com/106061407/175256043-28749bec-0cbe-47a5-809c-daf933753b92.png)


```
sudo apt-get install -y kubelet kubeadm kubectl kubernetes-cni
```

```
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```

Konfigurasi kubeadm

![image](https://user-images.githubusercontent.com/106061407/175256146-2129dad6-568d-48a6-a4fc-2ea3e2288ee5.png)

![image](https://user-images.githubusercontent.com/106061407/175256791-3db628ef-4293-46fa-b918-5a0f839ff0fa.png)


```
kubeadm init
```

Untuk versi Kubernates yang saya pakai yaitu versi: v1.24.2

-----------------------------------------

Konfigurasi kubernetes agar dapat menjalankan perintah

![image](https://user-images.githubusercontent.com/106061407/175257010-a692cd28-29b8-4bdf-acc9-f8c7898a9e8f.png)

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Selanjutnya kita harus deploy Container Network Interface (CNI) yang berbasis add-ons Pod network seperti calico, kube-router, dan weave-net. Add-ons Pod network tersebut berfungsi untuk membuat Pod berhubungan satu sama lain.

Deploy Add-on Pod Network Calico :

![image](https://user-images.githubusercontent.com/106061407/175257895-50a85393-00aa-4064-93b5-74a71419a71c.png)


```
kubectl apply -f https://docs.projectcalico.org/v3.14/manifests/calico.yaml
```

Mengecek semua pods gunakan perintah

![image](https://user-images.githubusercontent.com/106061407/175258120-ef1cc075-7c5d-4e38-ae6e-872bfd027f3d.png)


```
kubectl get pods --all-namespaces
```

Lalu lakukan join cluster dengan perintah berikut 

![image](https://user-images.githubusercontent.com/106061407/175259583-a3861bea-b1ce-4573-b5a4-ece1ae8f5955.png)

```
kubeadm token create --print-join-command
```

Kemudian copy semua hasil outputnya 

NOTE : INSTALL DAHULU KUBERNATES DENGAN VERSI YANG SAMA !!!

Copy pada kedua worker

![image](https://user-images.githubusercontent.com/106061407/175268798-2d003801-1972-44ba-9b52-dd890fa178c8.png)

[WORKER 1]

![image](https://user-images.githubusercontent.com/106061407/175269655-b86ee3f8-3d87-48b3-a5e4-754114829776.png)

[WORKER 2]

Kemudian cek koneksi nodes menggunakan perintah

![image](https://user-images.githubusercontent.com/106061407/175270141-ef88106e-9eef-4eee-8871-d9ac20a3245a.png)

```
kubectl get nodes
```

# Deploy Simple App

Kemudian saya akan mendeploy nginx 

![image](https://user-images.githubusercontent.com/106061407/175273336-72329767-50b9-4bea-bf00-dc7be61d94de.png)

```
kubectl create deploy nginx --image nginx
```

dan untuk buildnya gunakan perintah

```
kubectl expose deploy nginx --port 80 --type NodePort
```

Cek service gunakan perintah 

```
kubectl get svc
``` 

Selanjutnya saya akan cloning aplikasi microservices

![image](https://user-images.githubusercontent.com/106061407/175278462-e360398a-ab81-4866-83b6-1f9f7d0c6ee2.png)

FORK : https://github.com/dumbwaysdev/dumbways-microservices.git

```
git clone https://github.com/dumbwaysdev/dumbways-microservices.git
```

Kemudian masuk ke directory aplikasi microservices dan edit docker-compose dan kubernetes.yml nya

[file docker-compose]

![image](https://user-images.githubusercontent.com/106061407/175279611-8945ae3e-1637-40ac-8a52-4ae74c37edfc.png)

```
version: '3'

services:
    mongo:
        image : mongo
        container_name: mongo
        environment:
        - PUID=1000
        - PGID=1000
        volumes:
        - /home/pinoezz/mongo/database:/data/db
        ports:
        - 27017:27017
        restart: unless-stopped

    todo-profile:
        build: ./profile
        command: "ts-node /app/src/server"
        image: pinoezz/todo-profile
        restart: always
        container_name: todo-profile
        ports:
        - 5001:5001
    
    todo-services:
        build: ./services
        command: "node /app/src/server.js"
        image: pinoezz/todo-services
        restart: always
        container_name: todo-services
        ports:
        - 4000:4000
    
    todo-skill:
        build: ./skill
        command: "ts-node /app/src/server"
        image: pinoezz/todo-skill
        restart: always
        container_name: todo-skill
        ports:
        - 5000:5000

    todo-todo:
        build: ./todo
        command: "ts-node /app/src/server"
        image: pinoezz/todo-todo
        restart: always
        container_name: todo-todo
        ports:
        - 5002:5002

    todo-user:
        build: ./user
        command: "ts-node /app/src/server"
        image: pinoezz/todo-user
        restart: always
        container_name: todo-user
        ports:
        - 7000:7000
```

[File kubernetes.yml]

![image](https://user-images.githubusercontent.com/106061407/175280798-fb600461-5209-4af7-ba7b-1c4b1ccb078e.png)

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: todo-profile
spec:
  selector:
    matchLabels:
      app: todo-profile
  replicas: 1 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: todo-profile
    spec:
      containers:
      - name: todo-profile
        image: pinoezz/todo-profile
        ports:
        - containerPort: 5001
        command: ["/bin/sh"]
        args: ["-c", "while true; do echo hello; sleep 10;done"]
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: todo-services
spec:
  selector:
    matchLabels:
      app: todo-services
  replicas: 1 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: todo-services
    spec:
      containers:
      - name: todo-services
        image: pinoezz/todo-services
        ports:
        - containerPort: 4000
        command: ["/bin/sh"]
        args: ["-c", "while true; do echo hello; sleep 10;done"]
---
apiVersion: apps/v1
kind: Deployment
metadata:
name: todo-skill
spec:
  selector:
    matchLabels:
      app: todo-skill
  replicas: 1 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: todo-skill
    spec:
      containers:
      - name: todo-skill
        image: pinoezz/todo-skill
        ports:
        - containerPort: 5000
        command: ["/bin/sh"]
        args: ["-c", "while true; do echo hello; sleep 10;done"]
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: todo-todo
spec:
  selector:
    matchLabels:
      app: todo-todo
  replicas: 1 # tells deployment to run 2 pods matching the template
  template:
    metadata:
labels:
        app: todo-todo
    spec:
      containers:
      - name: todo-todo
        image: pinoezz/todo-todo
        ports:
        - containerPort: 5002
        command: ["/bin/sh"]
        args: ["-c", "while true; do echo hello; sleep 10;done"]
---

```

