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

![image](https://user-images.githubusercontent.com/106061407/170869792-5f7c3633-9dbb-4766-bf60-0e080901280a.png)

Setelah melakukan git init akan muncul file .git pada repository kalian


# Membuat 3 buah branch pada masing-masing aplikasi tersebut yaitu development, staging dan production

Selanjutnya saya akan membuat branch pada masing masing aplikasi 

Untuk melihat status pada branch gunakan perintah

```
git status
```

![image](https://user-images.githubusercontent.com/106061407/170835532-03a325c5-98cd-4f5a-b24a-2e5ad0cd7321.png)

Keterangan : gambar di atas menunjukan bahwa sekarang saya sedang berada pada branch master

![image](https://user-images.githubusercontent.com/106061407/170836586-09c233bb-e0cb-4700-acb0-8f5f417a4744.png)

Selanjutya saya akan melakukan stage pada index.js meggunakan perintah

```
git add index.js 
```

Apabila ingin melakukan stage pada semua file kalian gunakan 

```
git add .
```

![image](https://user-images.githubusercontent.com/106061407/170866108-67e2235b-7443-427c-a8de-ee76c6e9f980.png)


Untuk membuat commit kalian harus menjalankan perintah git commit -m "first commit"

![image](https://user-images.githubusercontent.com/106061407/170836729-38d76a8c-0d45-4af6-8045-b26053b3aae1.png)

Selanjutnya saya akan melalukan git push (Git push merupakan proses upload data yang ada di database git local ke database git di server. Untuk melakukan hal tersebut kita harus melakukan perintah di bawah ini.)

```
git push origin master
```


![image](https://user-images.githubusercontent.com/106061407/170866429-32d202f1-ea13-4fc5-a713-98de5649d3f5.png)

Setelah melakukan push pada repository kalian refresh reporitory github kalian , akan ada file yang baru kita push

Selanjutnya saya akan membuat 3 branch baru bernama (development, staging dan production) menggunakan perintah git branch 

```
git branch development
```

```
git branch staging
```

```
git branch production
```

Kemudia untuk cek branch yang tersedia gunakan perintah 

```
git branch -a
```

![image](https://user-images.githubusercontent.com/106061407/170866923-da6177cd-3e75-43dc-84fd-52f8907b1ea0.png)

Selanjutnya saya akan berpindah ke branch lain (contoh branch development) menggunakan perintah

```
git checkout development
```

![image](https://user-images.githubusercontent.com/106061407/170866998-9a063ee3-bce9-4a29-a0ab-6a66b3cd1970.png)

![image](https://user-images.githubusercontent.com/106061407/170870268-2dd5fe23-954e-4421-8d41-e89a11e9d00d.png)

Setelah masuk branch development kita akan melakukan push di branch development

![image](https://user-images.githubusercontent.com/106061407/170870579-1b8173d1-2050-43e3-ab36-fe8434525792.png)

![image](https://user-images.githubusercontent.com/106061407/170870659-3d5bf55a-477c-40d9-a77a-5369df88631f.png)

Selanjutnya akan saya lakukan push pada branch staging

![image](https://user-images.githubusercontent.com/106061407/170870757-7488da0f-0e49-4417-979b-64edac0ae659.png)

![image](https://user-images.githubusercontent.com/106061407/170870830-af2a9eaa-9c98-4731-8db4-cd154e5db6e4.png)


Selanjutnya akan saya lakukan push pada branch production

![image](https://user-images.githubusercontent.com/106061407/170870881-c232197b-3673-40d9-93b0-625a99c91bc7.png)

![image](https://user-images.githubusercontent.com/106061407/170870905-27f4faa0-9503-49bd-9105-01c0651a11b5.png)

Untuk Repository NodeJs kita sudah berhasil membuat 3 branch dan masing masing berisi aplikasi index.js

![image](https://user-images.githubusercontent.com/106061407/170871193-b6296275-217f-40c3-bb25-4d4a8b420f52.png)

Selanjutnya lakukan hal yang sama pada Repository Python dan Golang
