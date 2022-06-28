# Membuat User Baru Pada Masing-masing server

Pada pembuatan `user` ini saya akan menggunakan `ansible-playbook`

Pertama-tama kalian haus menginstall `whois` terlebih dahulu untuk generate suatu password

```
sudo apt install whois
```

Kemudian gunakan perintah berikut `mkpasswd -m sha-512 password_kalian` dan masukkan password yang kalian ingin gunakan

```
mkpasswd -m sha-512
```

![image](https://user-images.githubusercontent.com/106061407/176078103-3fec136d-122d-4a1c-b860-1774acd77162.png)

 

Berikut adalah `ansible-playbook` untuk membuat user baru pada masing-masing server

adduser.yml:

```
- hosts: nginx
  become: true
  tasks:
  - name: Add user for nginx
    user:
     name: nginx
     groups: sudo,docker
     shell: /bin/bash
     append: yes
     password: '$6$CGZ0zjUL.Xo/Wt$JbV2bbe7dLQWTJhxmFkrtp9Ng2RFwVcZ7VUEJ9a5A7I.X1G3egF.IhTs5GnWmV6Ap4ffHYkBNKUWZnV1rqo4v1'

- hosts: app
  become: true
  tasks:
  - name: Add user for app
    user:
     name: app
     groups: sudo,docker
     shell: /bin/bash
     append: yes
     password: '$6$CGZ0zjUL.Xo/Wt$JbV2bbe7dLQWTJhxmFkrtp9Ng2RFwVcZ7VUEJ9a5A7I.X1G3egF.IhTs5GnWmV6Ap4ffHYkBNKUWZnV1rqo4v1'

- hosts: jenkins
  become: true
  tasks:
  - name: Add user for jenkins
    user:
     name: jenkins
     groups: sudo,docker
     shell: /bin/bash
     append: yes
     password: '$6$CGZ0zjUL.Xo/Wt$JbV2bbe7dLQWTJhxmFkrtp9Ng2RFwVcZ7VUEJ9a5A7I.X1G3egF.IhTs5GnWmV6Ap4ffHYkBNKUWZnV1rqo4v1'

- hosts: monitoring
  become: true
  tasks:
  - name: Add user for monitoring
    user:
     name: monitoring
     groups: sudo,docker
     shell: /bin/bash
     append: yes
     password: '$6$CGZ0zjUL.Xo/Wt$JbV2bbe7dLQWTJhxmFkrtp9Ng2RFwVcZ7VUEJ9a5A7I.X1G3egF.IhTs5GnWmV6Ap4ffHYkBNKUWZnV1rqo4v1'

#Disable sign in without password
- hosts: all
  become: true
  tasks:
      - name: Change SSHD Config
        lineinfile:
          path: /etc/ssh/sshd_config
          regexp: '^PasswordAuthentication no'
          line: 'PasswordAuthentication yes'

      - name: Restart SSHD Service
        service:
          name: sshd
          state: restarted
          
```

Saya akan check syntax terlebih dahulu untuk memastikan `adduser.yml` dapat di jalankan

![image](https://user-images.githubusercontent.com/106061407/176080446-41278321-4217-4ee1-9473-e3be7f7e9058.png)


![image](https://user-images.githubusercontent.com/106061407/176080421-90cd74a9-dda6-41c8-b49e-071c1b157ae1.png)

Kemudian jalankan `ansible-playbook`  nya

```
ansible-playbook adduser.yml
```

![image](https://user-images.githubusercontent.com/106061407/176089152-35e1888c-31c9-40e3-9e9f-30532fe47c75.png)

Kemudian saya akan melakukan login ke user nginx menggunakan password

![image](https://user-images.githubusercontent.com/106061407/176089280-95b3d900-9d04-4560-a1cc-d870a3dfc268.png)

Apabila berhasil akan seperti ini kemudian saya akan tes pada server lainnya

![image](https://user-images.githubusercontent.com/106061407/176089522-2267357b-5a50-4ebb-b9c8-0c7592ba6af5.png)

![image](https://user-images.githubusercontent.com/106061407/176089559-92740a42-41b0-4312-ad36-6fc7a17d3dd8.png)


![image](https://user-images.githubusercontent.com/106061407/176089481-f34d4968-a9da-402c-af81-b23c4e63a48c.png)
