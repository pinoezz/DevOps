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

# Setup Kubernetes And Deploy Microservices

Sebelumnya apa itu Microservices? Microservices adalah kebalikannya dari Monolith, dimana aplikasi dipecah menjadi kecil-kecil, dimana tiap aplikasi hanya mengurus satu tugas dengan baik, dan semua aplikasi saling berkomunikasi.

Sekarang saya akan mempersiapakan 3 server (1 Manager) , (2 Worker) dari [IdCloudHost](idcloudhost.com)

![image](https://user-images.githubusercontent.com/106061407/175207641-ce3c5dec-9964-4e4a-96c1-ecbd2ea092d4.png)

![image](https://user-images.githubusercontent.com/106061407/175207791-e8751bb7-3d6b-4332-8835-3f2c36575800.png)


Untuk Manager saya gunakan CPU 2 Core, RAM 4 GB, SSD 20 GB

Untuk masing-masing worker saya gunakan CPU 1 Core, RAM 1GB, SSD 20 GB

![image](https://user-images.githubusercontent.com/106061407/175208025-2abab260-c644-4b52-9614-4485328fc8cc.png)

Tunggu hingga proses building selesai ...

-----------------------------


