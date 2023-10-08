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

<img width="1440" alt="Screenshot 2023-10-08 at 16 24 44" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/3abc3a92-6334-423f-ab3d-17bcc012292a">

Pertama-tama langkah yang perlu dilakukan adalah melakukan instalasi Ansible pada server lokal. Karena disini saya menggunakan OS Ubuntu 20.04 maka instalasi dapat dilihat dari [Referensi Instalasi Ansible versi Ubuntu](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu) berikut. Setelah itu saya melakukan verifikasi bahwa Ansible telah berjalan pada server lokal dengan menjalankan perintah:

```ansible
ansible --version
```

Lalu setelah itu saya membuat direktori bernamakan `ansible` lalu di dalamnya terdapat file yang berisikan `ansible-playbook` `ansible.cfg` dan `Inventory`. Berikut isi script dari file `Inventory` dan `ansible.cfg`

- Inventory

```ansible
[appserver]
103.175.218.224

[gateway]
103.175.217.130

[all:vars]
ansible_user="calvin"
ansible_python_interpreter=/usr/bin/python3
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

