# Create Server

Disini saya akan membuat 4 server dengan spesifikasi

- Server App (Frontend & Backend) or (Frontend, Backend, Database), 2 Core 2Gb RAM
- Server Nginx, 1 Core 1Gb RAM
- Server Monitoring, 1 Core 1Gb RAM
- Server CI/CD , 1 Core 2Gb RAM

![image](https://user-images.githubusercontent.com/106061407/175889635-2a0bec49-78bb-45dc-84ff-9b9b9bd48fd9.png)

![image](https://user-images.githubusercontent.com/106061407/175891816-565a6edd-584a-4d52-8645-cbd1d2bc8ae1.png)

# Install Docker

Untuk instalasi docker saya akan install menggunakan ansible playbook supaya lebih mudah dan cepat

Untuk menggunakan ansible ada beberapa bahan yang diperlukan antara lain :

- Install Ansible di local
- Membuat file keypem yang digunakan supaya ansible dapat mengenali server
- Membuat inventory yang berisi semua ip server target
- Membuat ansible.cfg yang berisi konfigurasi letak dari keypem dan inventory

