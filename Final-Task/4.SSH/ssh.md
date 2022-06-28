# SSH

Membuat SSH kostum dengan nama pino@dumbways 

![image](https://user-images.githubusercontent.com/106061407/176076379-4731e1fa-a900-4638-8348-96d1ed36c7a4.png)


Kemudian copy ssh ke semua server menggunakan `scp -r user@ip host`

example :

```
scp -r .ssh pino@103.226.139.62:/home/pino
```

Kemudian test menogneksikan ssh tanpa password 

![image](https://user-images.githubusercontent.com/106061407/176076519-21c4f637-34f4-4fe2-8353-39f7c69f6da9.png)

Kemudian sebagai tambahan saya akan melakukan ping ke semua server dengan ansible


![image](https://user-images.githubusercontent.com/106061407/176076790-5d35220d-35ad-48b9-a84f-b57b247dc5fd.png)

