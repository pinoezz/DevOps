![Img 1](assets/1.png)
# Tutorial Install Ubuntu Server 20.04 LTS Menggunakan VirtualBox

Sebelum di mulai ini merupakan postingan pertama saya di medium.com perkenalkan saya Alfino Dwi Nugroho , salah satu peserta Bootcamp DevOps Dumbways. Ini merupakan Tugas pertama saya , DevOps menurut pandangan saya yaitu gabungan antara Development dan Operation yang berarti menggabungkan proses development/pengembangan dari sebuah sistem/aplikasi dengan operation/operasional yang bertujuan untuk mempercepat pembuatan aplikasi dan meminimalisir adanya kesalahan pada saat deploying aplikasi.

![Img 1](assets/2.png)

Server atau dalam bahasa Indonesia biasa disebut peladen merupakan suatu sistem komputer yang memiliki layanan khusus berupa penyimpanan data. Data yang disimpan melalui server berupa informasi dan beragam jenis dokumen yang kompleks. Layanan tersebut ditujukan khusus untuk client yang berkebutuhan dalam menyediakan informasi untuk pengguna atau pengunjungnya.

Sistem operasi ada bermacam — macam mulai dari yang gratis sampai berbayar. Ubuntu server merupakan salah satu OS yang paling banyak digunakan untuk kebutuhan komputer server. Ubuntu dipilih karena dianggap lebih aman dari virus dan memiliki performa yang lebih kuat daripada OS lain. Pengembangan ubuntu terus dilakukan dan selalu ada update yang tersedia jika ditemukan celah keamanan.

Kali ini saya akan memberikan tutorial menginstall Ubuntu Server versi 22.04 LTS , LTS adalah kepanjangan dari Long Term Service, dengan kata lain kamu akan mendapat update selama 5 tahun penuh sebelum disarankan untuk melakukan upgrade ke versi yang lebih tinggi dan saya menggunakan VM (Virtual Machine) Virtual Box

Untuk bahan- bahan yang kalian butuhkan akan saya cantumkan link di bawah ini :

[Virtual Box](https://www.virtualbox.org/wiki/Downloads) (90MB–100MB)

[Ubuntu Server 20.04 LTS](https://ubuntu.com/download/server) (1.2GB)

Apabila file sudah di download, kalian install virtual box dan pilih lokasi untuk menyimpan file Virtual Boxnya

Berikut adalah langkah langkah menginstall Ubuntu Server 20.04 LTS

![Img 1](assets/3.png)

Buka Aplikasi VirtualBox

![Img 1](assets/4.png)

Pilih New

![Img 1](assets/5.png)

Masukan nama dan pilih lokasi folder lalu “Next”

![Img 1](assets/6.png)

Sesuai Task untuk RAM nya 2GB (2048MB) lalu pilih “Next”

![Img 1](assets/7.png)

 Pilih Create a virtual hard disk now lalu “Create”
 
![Img 1](assets/8.png)
 
 Pilih VDI (Virtual Box Disk Image) lalu “Next”
 
![Img 1](assets/9.png)
 
 Pilih Dynamically allocated lalu “Next”
 
 ![Img 1](assets/10.png)
 
 Atur kapasitas storage menjadi 10GB lalu “Create”
 
![Img 1](assets/11.png)

Apabila berhasil akan muncul mesin yang sudah di buat

![Img 1](assets/12.png)
![Img 1](assets/13.png)

Kemudian pilih “Start”

![Img 1](assets/14.png)

Pilih file Ubuntu Server 20.04LTS yang sudah di downlad lalu “Start”

![Img 1](assets/15.png)

Tunggu hingga proses selesai

![Img 1](assets/16.png)

Pada step ini kita diminta memilih bahasa , untuk bahasa yang saya pilih saya pakai bahasa inggris lalu “Enter”

![Img 1](assets/17.png)

Pilih Continue without updating lalu “Enter”

![Img 1](assets/18.png)

Pilih “Done” lalu “Enter”

![Img 1](assets/19.png)

Pada step ini karena intruksinya menggunakan static kalian “Enter” enp0s3

![Img 1](assets/20.png)

Pilih “Edit IPv4”

![Img 1](assets/21.png)

Pilih “Manual”

![Img 1](assets/22.png)

Setelah memih metode manual IPv4 / static kalian perlu mengisi Subnet,Address,Gateway, dan Name Server lalu pilih “Save”

![Img 1](assets/23.png)

Setelah itu DHCPv4 akan berubah menjadi Static lalu pilih “Done”

![Img 1](assets/24.png)

Pada step configure proxy langsung saja pilih “Done”

![Img 1](assets/25.png)

Pilih "Done"

![Img 1](assets/26.png)

Untuk Storage configuration kalian pilih “Costum storage layout” lalu “Done”

![Img 1](assets/27.png)

![Img 1](assets/28.png)

Pilih “free space” lalu pilih “Add GPT Partition”

![Img 1](assets/29.png)

untuk step selanjutkan saya memberikan 1GB untuk format “swap”

Swap adalah ruang pada disk yang digunakan ketika jumlah memori RAM fisik penuh. Ketika sistem Linux kehabisan RAM, halaman yang tidak aktif akan dipindahkan dari RAM ke ruang swap.

Swap space dapat berbentuk partisi swap khusus atau file swap. Dalam kebanyakan kasus, ketika menjalankan Linux pada mesin virtual, partisi swap tidak ada sehingga satu-satunya pilihan kita adalah membuat file swap.

![Img 1](assets/30.png)

![Img 1](assets/31.png)


Pilih “Create”

![Img 1](assets/32.png)

Lalu kalian pilih “free space” > “Add GPT Partition”

![Img 1](assets/33.png)

Untuk Size saya berikan Max / atau semua space yang tersisa “8.997GB” , Format pilih “ext4”, Mount “/’ , Lalu pilih “Create”


![Img 1](assets/34.png)

Kemudian pilih “Done”

![Img 1](assets/35.png)

Pilih "Cotinue"

![Img 1](assets/36.png)

Kalian perlu mengisi beberapa kolom profile . Jika sudah pilih “Done”

![Img 1](assets/37.png)

# Baca juga [Pengertian SSH](https://bit.ly/3wUAylc)

![Img 1](assets/38.png)

Pada step SSH Setup kalian pilih “Install OpenSSH Server” lalu pilih done

![Img 1](assets/39.png)

Pada step ini kalian diminta untuk menginstal beberapa fitur . Apabila tidak ada yang ingin di install bisa langsung pilih “Done”

Sebagai tambahan saya akan mengintall docker pada step diatas

![Img 1](assets/40.png)
![Img 1](assets/41.png)

Pilih “stable” dan “close”

![Img 1](assets/42.png)

Lalu pilih "Done"

![Img 1](assets/43.png)

Proses instalasi biasanya memakan beberapa menit , apabila sudah selesai kalian bisa pilih “Reboot Now”

![Img 1](assets/44.png)
![Img 1](assets/45.png)

Setelah pilih “Reboot Now” kalian tekan “Enter”

![Img 1](assets/46.png)

Setelah Server memasuki tampilan ini kalian perlu memasukan username dan password

![Img 1](assets/47.png)

Apabila sudah login tampilan kalian akan seperti ini

# Baca juga [Basic Command CLI Ubuntu](https://techlog360.com/basic-ubuntu-commands-terminal-shortcuts-linux-beginner/)

![Img 1](assets/48.png)

Selanjutnya saya tes koneksi dengan ping 8.8.8.8.com (dns google)
Apabila hasilnya seperti gambar diatas artinya kalian sudah mendapatkan koneksi internet

![Img 1](assets/49.png)

Pada step ini saya tes ping google.com

Setelah saya ping google.com , muncul pesan “temporary failure in name resolution” yang merupakan kesalahan resolusi nama dan menunjukkan bahwa server DNS Anda tidak dapat menyelesaikan nama domain ke alamat IP masing-masing. Ini dapat menghadirkan tantangan besar karena Anda tidak akan dapat memperbarui, meningkatkan, atau bahkan menginstal paket perangkat lunak apa pun di sistem Linux Anda.

# File resolv.conf yang Hilang atau Salah Dikonfigurasi


File /etc/resolv.conf adalah file konfigurasi resolver dalam sistem Linux. Ini berisi entri DNS yang membantu sistem Linux Anda untuk menyelesaikan nama domain ke alamat IP

Cara memperbaiki kegagalan ketika ping google.com ikuti langkah langkah berikut :

Note : sudo (/ˈsuːduː/ atau /ˈsuːdoʊ/) adalah suatu program untuk sistem operasi komputer sejenis Unix yang memungkinkan para pengguna untuk menjalankan program-program hak keamanan pengguna lain, secara default merupakan “superuser”


![Img 1](assets/50.png)

kalian ketikan sudo su lalu “enter’ dan masukan password kemudian “enter”

![Img 1](assets/51.png)

Kemudian tekan "Enter"

nano /etc/resolv.conf

![Img 1](assets/52.png)

Kalian akan masuk kedalam nano(text editor) /etc/resolv.conf

![Img 1](assets/53.png)

Ubah dan tambahkan nameserver

Ketika sudah di ubah kalian perlu menekan ctrl + o (Write Out) , lalu enter , Kemudian ctrl + x untuk exit

Kemudan kalian save dan restart systemd-resolved nya menggunakan command berikut:

$ sudo systemctl restart systemd-resolved.service

![Img 1](assets/54.png)

Kemudian test kembali ping goole.com
Gambar diatas menunjukan ping google.com telah berhasil
