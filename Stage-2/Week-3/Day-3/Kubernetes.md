# Kubernetes 

![image](https://user-images.githubusercontent.com/106061407/175206118-a6b8588e-ee85-4235-8cfd-57134e2e2a33.png)

Kubernetes adalah sistem orkestrasi kontainer sumber terbuka untuk mengotomatisasi penerapan, penskalaan, dan manajemen aplikasi komputer. Perangkat lunak ini awalnya dirancang oleh Google dan sekarang dikelola oleh Cloud Native Computing Foundation

Atau singkatnya KUBERNETES itu adalah salah satu aplikasi opensource  untuk automation scaling dan manajemen aplikasi berbasis container

![image](https://user-images.githubusercontent.com/106061407/175206485-3ec509e1-d62b-4c2e-803f-3caf75e24e10.png)

Untuk konsep cara kerja dari kubernetes adalah seperti di atas atau spesifiknya :

KUBERNETES MASTER :

Kube-apiserver bertugas sebagai API yang digunakan untuk berinteraksi dengan Kubernetes Cluster

Etcd bertugas untuk sebagai database untuk menyimpan data Kubernetes Cluster

Kube-scheduler bertugas untuk memperhatikan aplikasi yang kita jalankan dan meminta Node untuk menjalankan aplikasi yang kita jalankan

Kube-controller-manager bertugas melakukan kontrol terhadap Kubernetes Cluster

Cloud-controller-manager bertugas untuk melakukan kontrol terhadap interaksi dengan cloud provider

Kubernetes Nodes : 

Kubelet berjalan di setiap Node dan bertugas untuk memastikan bahwa aplikasi kita berjalan di Node

Kube-proxy berjalan di setiap Node dan bertugas sebagai proxy terhadap arus network yang masuk ke aplikasi kita dan sebagai load balancer juga

Container-manager berjalan di setiap Node dan bertugas sebagai container manager. Kubernetes mendukung beberapa container manager seperti Docker, containerd, cri-o, rktlet, dan yang lainnya.

-----------------------------------
