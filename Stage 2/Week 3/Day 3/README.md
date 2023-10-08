# Infrastructre as Code
## Ansible
### Task
* Lokal
  * Buat konfigurasi Ansible & dan lakukan semua setup melalui lokal sebanyak mungkin
* Appserver
  * Gunakan Ansible-Playbook
    * Membuat user baru, Gunakan login SSH key
    * Instalasi Docker & Node-Exporter
    * Buat Konfigurasi Prometheus (Monitoring)
    * On Top Docker menjalankan Grafana & Prometheus
* Gateway
  * Gunakan Ansible-Playbook
    * Membuat User Baru, Gunakan Login SSH Key
    * Instalasi Nginx
    * Buat Konfigurasi Proxy lalu Masukkan Kedalam Gateway
    * Gunakan Docker Compose untuk deploy aplikasi Wayshub-Frontend

<br>
<br>

#### 1. Instalasi Ansible

<img width="1440" alt="Screenshot 2023-10-08 at 16 24 44" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/3abc3a92-6334-423f-ab3d-17bcc012292a">

Pertama-tama langkah yang perlu dilakukan adalah melakukan instalasi Ansible pada server lokal. Karena disini saya menggunakan OS Ubuntu 20.04 maka instalasi dapat dilihat dari [Referensi Instalasi Ansible versi Ubuntu](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu) berikut. Setelah itu saya melakukan verifikasi bahwa Ansible telah berjalan pada server lokal dengan menjalankan perintah:

```ansible
ansible --version
```

#### 2. Membuat file yang dibutuhkan untuk menjalankan Ansible-Playbook

Lalu setelah itu saya membuat direktori bernamakan `ansible` lalu di dalamnya terdapat file yang berisikan `ansible.cfg`, `Inventory`, `adduser.yml`, `docker.yml`, `docker-compose.yml`, `wayshub-fe.yml`, `nginx.yml`,  . Berikut isi script dari file file tersebut

- Inventory

```ansible
[appserver]
103.175.218.224

[gateway]
103.175.217.130

[all:vars]
ansible_connection=ssh
ansible_port=22
ansible_user="calvin"
ansible_python_interpreter=/usr/bin/python3.8
```

- ansible.cfg

```ansible
[defaults]
inventory = Inventory
private_key_file = /home/ubuntu/.ssh/id_rsa
host_key_checking  = False
timeout = 10
remote_port = 22
interpreter_python = auto_silent
```

- adduser.yml

```ansible
---
- become: true
  gather_facts: false
  hosts: all
  vars:
    - user: calvin2
    - passwd: $5$rgdh8Kfr5ZmRr7m4$TMzhvPQ4ml9D1uxB5eBlaF4CbL7KKtEwrRO/ubMqtfC
  tasks:
    - name: Creating User
      ansible.builtin.user:
        append: true
        groups: sudo
        name: "{{user}}"
        password: "{{passwd}}"
        home: /home/({user})
        state: present
        system: true
        generate_ssh_key: true
        ssh_key_file: .ssh/calvin2
```

- docker.yml

```ansible
---
- become: true
  hosts: all
  gather_facts: false
  tasks:
    - name: Install Prerequisite
      apt:
        update_cache: yes
        name:
          - apt-transport-https
          - ca-certificates
          - curl
          - software-properties-common
          - gnupg
          - python3-pip
          - python3-venv
          - python3-docker
    - name: Add Docker GPG Key
      apt_key:
        url: https://download.docker.com/linux/ubuntu/gpg
    - name: Add Docker Repository
      apt_repository:
        repo: deb https://download.docker.com/linux/ubuntu focal stable
    - name: Install Docker Engine
      apt:
        update_cache: true
        name:
          - docker-ce
          - docker-ce-cli
          - docker-buildx-plugin
    - name: Add User Docker Group
      user:
        name: calvin
        groups: docker
        append: yes
```

- docker-compose.yml

```ansible
version: "3.8"
services:
   frontend:
    container_name: wayshub-fe
    image: calvinnr/wayshub-fe:latest
    stdin_open: true
    ports:
      - 3000:3000
```

- wayshub-fe.yml

```ansible
- become: true
  gather_facts: false
  hosts: appserver
  tasks:
    - name: Pull Image from Docker Hub
      docker_image:
       name: calvinnr/wayshub-fe:latest
       source: pull
    - name: Copy Docker Compose File to Gateway
      copy:
        src: /home/ubuntu/ansible/docker-compose.yml
        dest: /home/calvin
    - name: Run Docker Compose
      command: docker compose up -d
```

- nginx.yml

```ansible
---
- become: true
  gather_facts: false
  hosts: gateway
  tasks:
    - name: Installing NGINX
      apt:
        name: nginx
        state: present
        update_cache: no
    - name: Copy rproxy.conf
      copy:
        src: /home/ubuntu/ansible/rproxy.conf
        dest: /etc/nginx/sites-enabled
    - name: Reload NGINX
      service:
        name: nginx
        state: reloaded
```

- rproxy.conf

```ansible
server {
    server_name calvin.studentdumbways.my.id;
    location / {
    proxy_pass http://103.175.218.224:3000;
    }
}
```

#### 3. Hasil Ansible-Playbook

Berikut Hasil dari `adduser.yml`, `docker.yml`, `wayshub-fe.yml`, `nginx.yml`

<img width="1440" alt="Screenshot 2023-10-09 at 00 51 19" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/1e412e83-c811-49c7-bb77-6d908d81fded">

> adduser.yml

<img width="1440" alt="Screenshot 2023-10-09 at 01 58 19" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/6a9b55dc-bd38-44b2-b7f2-ae28092e8409">

> docker.yml

<img width="1440" alt="Screenshot 2023-10-09 at 02 39 04" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/f14bbd79-3a2a-4d67-baeb-19fbb16ea85d">

> wayshub-fe.yml

<img width="1440" alt="Screenshot 2023-10-09 at 02 27 06" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/05ffea69-c453-4f9a-bd14-029fae374996">

> nginx.yml

#### 4. Hasil Deploy Aplikasi

<img width="1440" alt="Screenshot 2023-10-09 at 02 39 25" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/5a5dc78a-e4f2-4ad5-be88-0dd51761300d">

Dan berikut hasil dari Wayshub-Fe yang sudah Terdeploy dan Reverse Proxy-nya teraplikasikan dengan baik
