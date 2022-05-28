# Version Control Systems

![image](https://user-images.githubusercontent.com/106061407/170829146-6659e918-d5b0-4f81-b203-650e747c020a.png)

# Git
Git menurut saya yaitu sebuah perangkat lunak atau software yang digunakan untuk mengembangkan suatu aplikasi

# Instalasi Git

Jika kamu menggunakan operating system Linux-Ubuntu/Mac-OS kamu bisa skip installasi ini karena Git sudah ada secara default.


Bagi yang menggunakan operating system Windows kalian dapat mendowload dan menginstall install git terlebih dahulu melalui link dibawah ini.

-------------
[Git Download](https://git-scm.com/downloads)

-------------

# Git Config

Hal pertama yang harus kalian lakukan adalah menetapkan nama pengguna dan alamat email, untuk perintahnya kalian dapat menggunakan perintah dibawah ini.

```
git config --global user.name "your.github-user.name"
```

```
git config --global user.email "your.github-user.email"
```

Jika kalian sudah menjalankan perintah di atas, kalian bisa cek user.name dan user.email kalian sudah tepat atau belum dengan menggunakan perintah dibawah ini.

```
git config --list
```

![image](https://user-images.githubusercontent.com/106061407/170834949-4f980dcb-9cb3-445d-9b19-7fb85f36ffa5.png)

# Git Remote

# Membuat Repository​

Repository adalah suatu penyimpanan file project. dimana kamu bisa menyimpan apapun yang berkaitan dengan project kalian, seperti code, gambar, ataupun 
audio. repo sendiri bertempat di penyimpanan atau storage github atau repository local di komputer anda.

![3](https://user-images.githubusercontent.com/106061407/170835864-ab2f2834-6cee-4ce1-b059-2166acc6036b.png)


Copy yang sudah disediakan Github, jangan lupa untuk memilih bagian SSH karena kita menggunakan SSH untuk mengkoneksikan local kita dengan Github.

![image](https://user-images.githubusercontent.com/106061407/170835790-02eed5a2-0705-4341-913c-163711fa61ba.png)

```
git remote add origin git@github.com:pinoezz/NodeJs.git
```

Untuk melihat remote yang kita gunakan kita bisa menggunakan perintah berikut :

```
git remote -v
```

![image](https://user-images.githubusercontent.com/106061407/170836066-e98e718a-c8a4-4e67-81e0-34459443b67b.png)

Apabila sebelumnya anda pernah remote lalu terjadi kesalahan seperti di atas kalian perlu menghapus remote yang sebelumnya terlebih dahulu

```
git remote remove origin
```

# Check remote​

Untuk melihat remote yang kita gunakan kita bisa menggunakan perintah berikut :

```
git remote -v
```
![image](https://user-images.githubusercontent.com/106061407/170836161-af1bc8e4-fa14-4d60-bc48-a11e2d32938f.png)


# Task

# Membuat 3 buah repository untuk masing-masing aplikasi (NodeJS, Python dan Go)

Untuk cara pertama membuat repository sendiri kita bisa menggunakan perintah berikut :
git init (nama-repository-yang-kalian-inginkan)

```
git init
```

![image](https://user-images.githubusercontent.com/106061407/170830880-594d11b7-d097-4f1b-8957-eedb820ff2a9.png)

Setelah membuat 3 repository selanjutnya saya akan membuat aplikasi di dalam repository

![image](https://user-images.githubusercontent.com/106061407/170835335-0d8227e8-dc69-4029-93ba-6c3b9ca1b048.png)


# Membuat 3 buah branch pada masing-masing aplikasi tersebut yaitu development, staging dan production

Selanjutnya saya akan membuat branch pada masing masing aplikasi 

Untuk melihat status pada branch gunakan perintah

```
git status
```

![image](https://user-images.githubusercontent.com/106061407/170835532-03a325c5-98cd-4f5a-b24a-2e5ad0cd7321.png)

Keterangan : gambar di atas menunjukan bahwa sekarang saya sedang berada pada branch master

