# Version Control Systems

![image](https://user-images.githubusercontent.com/106061407/170829146-6659e918-d5b0-4f81-b203-650e747c020a.png)

# Git
Git menurut saya yaitu sebuah perangkat lunak atau software yang digunakan untuk mengembangkan suatu aplikasi

# Instalasi Git


Tahap pertama kita perlu menginstall GIT pada laptop/komputer.

Jika kamu menggunakan operating system Linux-Ubuntu/Mac-OS kamu bisa skip installasi ini karena Git sudah ada secara default.


Bagi yang menggunakan operating system Windows kalian dapat mendowload dan menginstall install git terlebih dahulu melalui link dibawah ini.

-------------
[Git Download](https://git-scm.com/downloads)

-------------

# Konfigruasi Git

Hal pertama yang harus kalian lakukan adalah menetapkan nama pengguna dan alamat email, untuk perintahnya kalian dapat menggunakan perintah dibawah ini.

```
git config --global user.name "your.github-user.name"
```
```

git config --global user.email "your.github-user.email"
```

![1](https://user-images.githubusercontent.com/106061407/170829912-c5d32e7e-1adb-4896-9f42-3e5cc09c5ae4.png)

Untuk cek username dan email kalian bisa menggunakan perintah di bawah ini

```
git config --list
```
![2](https://user-images.githubusercontent.com/106061407/170829940-62b2407e-7e4b-4c4e-a1f9-6d454fa7c9d5.png)

# Generate SSH key

Untuk mendapatkan SSH key kalian dapat menggunakan perintah dibawah ini.

```
ssh-keygen
```
![image](https://user-images.githubusercontent.com/106061407/170830119-9c9c0637-5d5c-4bbe-89ac-0c3944c2f24c.png)


# SSH key Location​

Jika kalian sudah menjalankan perintah sebelumnya maka kalian sudah berhasil untuk men-generate SSH key yang akan kalian gunakannya. Untuk lokasi SSH key yang sudah kalian generate tadi berada di .ssh/id_rsa.pub. Jika sudah lakukan copy pada SSH-key tersebut.

```
cat .ssh/id_rsa.pub
```
![3](https://user-images.githubusercontent.com/106061407/170830000-f255192e-23fd-4037-8803-46376bba7ec7.png)
