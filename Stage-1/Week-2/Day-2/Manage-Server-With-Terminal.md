# Manage Server With Terminal

![image](https://user-images.githubusercontent.com/106061407/171598737-62506798-576d-42b7-9267-ac9639c43ba2.png)

# Terminal

# Apa itu Terminal?

Menurut saya terminal adalah sebuah aplikasi command prompt yang berfungsi sebagai penghubung User dengan system komputer contoh dalam mengontrol file, membuat folder, ataupun membuat akses 

# Keuntungan Menguasai Terminal

Keuntungan menguasai terminal menurut saya adalah suatu yang sangat penting karena di DevOps kita sering kali melakukan remoting server berbasis CLI.
Oleh karena itu penting nya mengusai terminal supaya kita dapat mengoprasikan OS berbasis CLI

# Memuat sebuah file bash sederhana yang bertugas untuk update dan upgrade sistem

Pada task kali ini saya menggunakan Ubuntu Server 20.04 

Baca juga [Cara Install Ubuntu Server 20.04 Menggunakan VM](https://github.com/pinoezz/DevOps/blob/main/stage1/Week-1/Day1/Instalasi-Ubuntu-Server.md)

![image](https://user-images.githubusercontent.com/106061407/171608954-5956fde3-b11d-4092-ac14-055e79a6dd10.png)

Setelah meremote server saya akan membuat direktori baru

![image](https://user-images.githubusercontent.com/106061407/171649912-e6b81bc5-3b4d-4d86-969e-17e3a4911d54.png)

![image](https://user-images.githubusercontent.com/106061407/171650478-f0e8396a-c079-4fe0-9384-29459d2e21ae.png)

![image](https://user-images.githubusercontent.com/106061407/171651049-fb04d4c2-775f-4619-8340-9fd9a9b012fc.png)

![image](https://user-images.githubusercontent.com/106061407/171651147-e2b95642-9352-48cc-badb-c80aac67923c.png)

# Membuat sebuah file bash sederhana yang bertugas untuk mencari file bernama `sysctl.conf`(file system etc)

![image](https://user-images.githubusercontent.com/106061407/171665298-2605985f-77ea-41fb-bda5-43c3ac2b7110.png)

![image](https://user-images.githubusercontent.com/106061407/171666631-db26a5b8-cddc-4bf7-9c10-61de80f8dd4d.png)

![image](https://user-images.githubusercontent.com/106061407/171666685-92fee15e-b772-4433-9aa0-ab99b8b838e9.png)

![image](https://user-images.githubusercontent.com/106061407/171666722-d1ff0e0d-1e28-44c4-86bc-49d43a18bf8c.png)


# Membuat sebuah file bash sederhana yang bertugas untuk mencari file bernama `sysctl.conf`(create file)

![image](https://user-images.githubusercontent.com/106061407/172058672-a44dc9cc-534d-4185-8c83-af0b9aedde8e.png)


![image](https://user-images.githubusercontent.com/106061407/172058473-82d9a0fa-c9af-4a58-ab3d-ba61a0bac59e.png)

![image](https://user-images.githubusercontent.com/106061407/172058829-d1bbe9e7-b2b5-4773-87e0-b0523e810436.png)



![image](https://user-images.githubusercontent.com/106061407/172058818-bfe8424c-8c91-4ce8-bda7-7bc18b9118bb.png)


```
find -type f -name sysctl.conf
```
![image](https://user-images.githubusercontent.com/106061407/172058554-31efb6a4-1771-4a53-a9ed-2f2ade761c8f.png)

![image](https://user-images.githubusercontent.com/106061407/172058729-4db98e8f-d981-4084-9c06-c2ba8fdc4a1c.png)


# Membuat sebuah file bash serderhana yang bertugas untuk membuat firewall port 22, 80 dan 443 

Uncomplicated Firewall (UFW) adalah sebuah interface dari Linux iptables. iptables sendiri adalah tools yang sangat bagus untuk melakukan konfigurasi firewall di sistem operasi berbasis Linux. Namun iptables cukup rumit untuk dipahami oleh sebagian orang. UFW hadir untuk mengatasi permasalahan tersebut dengan cara menyederhanakan perintah konfigurasi firewall sehingga memudahkan sistem administrator dalam mengelola firewall.

Lagkah pertama isntall ufw 

```
sudo apt install ufw -y
```
![image](https://user-images.githubusercontent.com/106061407/171670190-1a86cdb2-b1bd-4ecb-a600-0df3ccce1540.png)


![image](https://user-images.githubusercontent.com/106061407/171671972-b68b4c96-468c-458b-b33a-4aac5e3e94cc.png)


![image](https://user-images.githubusercontent.com/106061407/171671866-8be45c22-bc53-4767-912a-73b48f9ab224.png)

```
echo "file 22"

sudo ufw allow 22

echo "file 80"

sudo ufw allow 80

echo "file 443"

sudo ufw allow 443
```

![image](https://user-images.githubusercontent.com/106061407/171672197-2f7c7a60-aa41-4205-a447-97f9092629cd.png)

Untuk mengeceknya kita bisa menggunakan

```
sudo ufw enable
```

```
sudo ufw status
```

![image](https://user-images.githubusercontent.com/106061407/171675203-c1e358ec-fbe4-4cb2-8948-f5195bd8babe.png)
