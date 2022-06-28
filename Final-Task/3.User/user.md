# Membuat User Baru Pada Masing-masing server

Pada pembuatan user ini saya akan menggunakan ansible-playbook

Pertama-tama kalian haus menginstall `whois` terlebih dahulu untuk generate suatu password

```
sudo apt install whois
```

Kemudian gunakan perintah berikut `mkpasswd -m sha-512 password_kalian` dan masukkan password yang kalian ingin gunakan

```
mkpasswd -m sha-512
```

![image](https://user-images.githubusercontent.com/106061407/176078103-3fec136d-122d-4a1c-b860-1774acd77162.png)

 

Berikut adalah ansible-playbook untuk membuat user baru pada masing-masing server

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

