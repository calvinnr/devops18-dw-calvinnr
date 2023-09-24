# 1. Deploy Wayshub

## 1.1 Konfigurasi VM untuk App Server di IdCloudHost
<img width="1440" alt="Screenshot 2023-09-21 at 02 21 34" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/56fbecd3-288f-43be-a2a5-62ea12631365">
Berikut konfigurasi VM untuk App Servernya

> Processor: 2 vCPU,
> 
> Memory: 2GB RAM,
>
> Storage: 20GB,
> 
> Operating System: Ubuntu 20.04 LTS
>
> IP Public: 103.187.146.52
>
> IP Private: 10.36.116.221
<br>

## 1.2 Clone Repository Wayshub
<img width="1440" alt="Screenshot 2023-09-21 at 02 22 23" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/b54be6d1-0984-4df6-996c-28f4542de5cc">
Setelah Masuk kedalam VM, Hal pertama yang dilakukan adalah melakukan clone repository yang dibutuhkan untuk keperluan task dengan menjalankan perintah:
<br>

(Wayshub-Frontend)
```git
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

(Wayshub-Backend)
```git
git clone https://github.com/dumbwaysdev/wayshub-backend
```
<br>

## 1.3 Instalasi NVM & NodeJS v14
<img width="1440" alt="Screenshot 2023-09-21 at 02 25 54" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/c388ed40-e37d-47d8-910e-324e4055df50">
Setelah Cloning Repository selesai dilakukan, Langkah selanjutnya kita perlu meng-install NVM Terlebih dahulu dengan menjalankan perintah:

```shell
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

Setelah NVM telah ter-install, Jalankan perintah berikut agar NVM dapat terbaca pada shell bash dengan menjalankan perintah:

```shell
exec bash
```

Lalu, Jalankan perintah berikut untuk meng-install NodeJS v14:

```shell
nvm install 14
```
<br>

## 1.4 Instalasi PM2
<img width="1440" alt="Screenshot 2023-09-21 at 02 28 31" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/d249a611-c921-4e16-91ae-8abbe9c942d2">
Langkah selanjutnya yang kita perlu lakukan meng-install PM2 yang dimana nanti akan kita gunakan untuk men-deploy aplikasi Frontend & Backend-nya dengan menjalankan perintah:

```shell
npm install -g pm2
```
<br>

## 1.5 Konfigurasi Ecosystem PM2 di Wayshub Frontend & Backend
<img width="1440" alt="Screenshot 2023-09-21 at 02 50 46" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/7edd2812-5098-4ddb-b324-01e8e830db8b">
Setelah instalasi PM2 selesai, agar kita mudah men-deploy aplikasi Frontend & Backendnya. Kita perlu mengkonfigurasi Ecosystem PM2-nya. Pertama, kita generate terlebih dahulu konfigurasi simpel-nya dengan menjalankan perintah:

```pm2
pm2 ecosystem simple
```

<img width="1440" alt="Screenshot 2023-09-21 at 02 51 21" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/65006a3a-8ce2-4bee-a52e-34c16d01373c">
Jika berhasil ter-generate akan muncul pemberitahuan seperti diatas ini

<img width="1440" alt="Screenshot 2023-09-21 at 02 51 48" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/def7231a-669f-4dbc-a4da-c64375f81a8c">
Setelah file PM2 Ecosystem-nya ter-generate pada direktori Wayshub Frontend, kita perlu merubah isi-nya dengan konfigurasi singkat sebagai berikut:

> name: "wayshub-frontend"
> 
> script: "npm start"

<img width="1440" alt="Screenshot 2023-09-21 at 02 52 26" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/0ff58e62-58ac-4ac8-9757-be8f0625dc1b">
Sekarang, kita lanjut generate Ecosystem PM2 ke Backend-nya dengan menjalankan perintah yang sama pada direktori Wayshub Backend yaitu:

```pm2
pm2 ecosystem simple
```

<img width="1440" alt="Screenshot 2023-09-21 at 02 52 45" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/a9ac44b3-9d8b-4784-9d69-fc3cd1257f17">
Setelah file PM2 Ecosystem-nya ter-generate pada direktori Wayshub Frontend, kita perlu merubah isi-nya dengan konfigurasi singkat sebagai berikut:

> name: "wayshub-backend"
> 
> script: "npm start"


## 1.6 Deploy Aplikasi Wayshub Frontend & Backend
<img width="1440" alt="Screenshot 2023-09-21 at 02 53 26" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/038a483b-fd05-4f34-a6f9-b428eb6b7f18">
Setelah Ecosystem PM2-nya telah selesai kita konfigurasi, lalu kita tes dengan men-deploy aplikasi Wayshub Frontend & Backendnya menggunakan PM2 pada masing-masing direktori dengan menjalankan perintah:

```pm2
pm2 start
```

<img width="1440" alt="Screenshot 2023-09-21 at 02 54 51" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/1dfc5f5d-aa1f-4158-92b7-ab71475d6b58">
Berikut tampilan Wayshub Frontend yang berhasil di deploy menggunakan PM2
<br>
<br>
<img width="1440" alt="Screenshot 2023-09-21 at 02 54 56" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/2e330f11-ce60-4fb8-827f-5b7177fa88a9">
Berikut tampilan Wayshub Backend yang berhasil di deploy menggunakan PM2


## 1.7 Instalasi MySQL
<img width="1440" alt="Screenshot 2023-09-21 at 02 37 03" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/115238dc-448f-4d66-8e0f-d098d7b844fe">
Langkah pertama yang perlu dilakukan sebelum instalasi package MySQL yaitu melakukan update pada index package-nya dengan menjalankan perintah:

```shell
sudo apt update
```
<br>
<img width="1440" alt="Screenshot 2023-09-21 at 02 43 19" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/6c00daca-9220-431f-9943-726de684cd99">
Setelah indeks ter-update, instalasi package MySQL dapat kita lakukan dengan menjalankan perintah:

```shell
sudo apt install mysql-server
```

## 1.8 Menjalankan Script MySQL Secure Installation
<img width="1440" alt="Screenshot 2023-09-21 at 02 47 51" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/127fd213-44a8-443c-8721-87027f38f7b6">
Ada satu langkah penting yang perlu dilakukan setelah instalasi MySQL, yaitu dengan menjalankan MySQL Secure Installation. Mengapa demikian? Karena MySQL sesaat setelah di-install, Konfigurasinya masih bersifat <i>default</i> sehingga mudah untuk diakses. Maka dengan menjalankan script MySQL Secure Installation kita tidak perlu repot-repot mengubah konfigurasi-nya secara manual. Berikut perintah yang perlu kita jalankan:

```shell
sudo mysql_secure_installation
```

<img width="1440" alt="Screenshot 2023-09-21 at 02 48 13" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/6d940b7d-b130-40dc-a5d0-739c6c0b2669">
Disini saya memasukan <i><b>Y</b></i> karena saya ingin menetapkan standar dari password yang akan digunakan kedepannya
<img width="1440" alt="Screenshot 2023-09-21 at 02 48 19" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/ce6addc3-de7d-4e0a-8aa8-79eb528c634c">
Disini saya memasukan <i><b>0</b></i> karena saya ingin menetapkan standar dari password dimana harus memiliki lebih dari sama dengan 8 karakter
<img width="1440" alt="Screenshot 2023-09-21 at 02 48 27" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/199830b8-f95e-4221-a8ee-c1819c942f89">
Disini saya memasukan <i><b>Y</b></i> karena saya ingin menghapus akun <i>Anonymous</i> agar MySQL tidak dapat diakses oleh sembarang orang
<img width="1440" alt="Screenshot 2023-09-21 at 02 48 36" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/152a4da2-d5a7-4a5a-8aaa-ffe90e9e2eba">
Disini saya memasukan <i><b>N</b></i> karena saya ingin tetap mempertahankan akses agar MySQL dapat diakses meskipun saya melakukan remote/SSH pada VM
<img width="1440" alt="Screenshot 2023-09-21 at 02 48 42" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/162ca8e9-b104-4be5-9e80-db6e3591dc42">
Disini saya memasukan <i><b>N</b></i> karena saya ingin tetap membiarkan Test Database yang telah tersedia dari awal
<img width="1440" alt="Screenshot 2023-09-21 at 02 48 48" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/45032ffd-5fd0-4b50-934b-0c2aa972eccb">
Disini saya memasukan <i><b>Y</b></i> agar semua konfigurasi yang telah diikuti dan dikonfirmasi perubahannya diatas maka MySQL perlu mengecek ulang hak akses dan pengguna yang terdaftar
<br>

## 1.9 Membuat User di MySQL
<img width="1440" alt="Screenshot 2023-09-21 at 02 45 01" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/ab58c85a-490b-4b23-9356-1b43196a720a">
Langkat pertama kita masuk kedalam MySQL-nya terlebih dahulu sebagai root dengan menjalankan perintah:

```shell
sudo mysql -u root -p
```

<img width="1440" alt="Screenshot 2023-09-21 at 02 45 08" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/db08b7f2-e121-4913-8da1-fbadd1f52a04">
Lalu, sesaat kita masuk kedalam MySQL, kita buat user dengan menjalankan perintah:

```mysql
CREATE USER 'calvin'@'%' IDENTIFIED BY 'calvin0411';
```

<img width="1440" alt="Screenshot 2023-09-21 at 02 45 13" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/3955971d-9e90-4ee3-8561-c008a2960dda">
Setelah user terbuat, User tersebut tidak memiliki akses apapun. Maka, Kita perlu memberikan akses pada user tersebut dengan menjalankan perintah:

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'calvin'@'%' WITH GRANT OPTION;
```
<sup>Perintah diatas dapat membuat user memiliki akses seperti user ROOT. Maka perintah diatas perlu digunakan secara hati-hati jika diterapkan pada kasus nyata.</sup>
<br>

## 1.10 Konfigurasi API pada Wayshub-Frontend
<img width="1440" alt="Screenshot 2023-09-21 at 02 32 14" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/05a85419-deaa-49c9-b380-8016e45901b7">
Setelah semua package yang dibutuhkan telah ter-install, Tahap pertama agar Wayshub Frontend dapat terhubung dengan Wayshub Backend kita perlu mengkongfigurasi API-nya. Lalu kita masuk ke direktori Wayshub Frontend lalu masuk ke dir Src/ setelah itu masuk ke dir Config/ setelah itu kita edit api.js-nya
<br>
<br>
<img width="1440" alt="Screenshot 2023-09-21 at 02 32 26" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/911837c7-cfc7-4ad3-b9ed-83aa8a0c42ea">
Disini kita rubah BaseURL-nya dengan URL yang telah disediakan. Disini saya menggunakan domain:

> baseURL: "api.calvin.studentwayshub.my.id/api/v1"
<br>

## 1.11 Konfigurasi Database pada Wayshub-Backend
<img width="1440" alt="Screenshot 2023-09-21 at 02 34 51" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/7817ef7b-60ec-427e-80fd-178ffde8d19c">
Lalu, kita konfigurasi database MySQL pada Wayshub Backend agar MySQL dapat terhubung dengan Wayshub Backend dengan masuk ke direktori Wayshub Backend lalu masuk ke Config/ lalu kita edit config.json-nya
<br>
<br>
<img width="1440" alt="Screenshot 2023-09-21 at 02 34 36" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/71b767f1-fd36-421c-98a7-a1c20f96b73a">
Disini saya merubah pada environment <i><b>Development</b></i> dengan isian sebagai berikut:

> username: "calvin"
> password: "calvin0411"
> database: "db-wayshub"
<br>

## 1.12 Instalasi Sequelize-CLI di Wayshub Backend
<img width="1440" alt="Screenshot 2023-09-21 at 02 56 33" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/3178c307-9e3e-42fc-a68c-45552719b75d">
Setelah selesai kita konfigurasi MySQL-nya, Langkah selanjutnya adalah kita meng-install package Sequelize-CLI menggunakan NPM pada direktori Wayshub Backend. Fungsi Sequelize-CLI disini adalah sebagai alat untuk untuk mengelola database dalam aplikasi NodeJS yang menggunakan Sequelize sebagai ORM (Object-Relational Mapping) untuk berinteraksi dengan database SQL. Berikut perintah yang perlu dijalankan untuk instalasi package-nya:

```nodejs
npm install -g sequelize-cli
```

Lalu setelah instalasi package Sequelize-CLI-nya selesai, kita perlu membuat database baru pada Wayshub Backend yang berguna untuk menyimpan data yang akan dimasukan kedepannya di Wayshub Backend dengan menjalankan perintah:

```mysql
sequelize db:create
```

<img width="1440" alt="Screenshot 2023-09-21 at 03 03 10" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/8f98b4f7-fa29-4da8-8734-e57776c33e15">
Setelah database terbuat, kita perlu melakukan migrasi struktur database pada isi direktori <i><b>migrations</b></i> agar setiap perubahan yang dilakukan tidak menghilangkan data yang ada dengan menjalankan perintah:

```mysql
sequelize db:migrate
```

## 1.13 Validasi Database Hasil Migrasi
<img width="1440" alt="Screenshot 2023-09-21 at 03 03 56" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/ea7588f0-db38-4748-922a-697d0620771c">
Setelah semua tahap diatas kita lakukan, Kita validasi kembali apakah database yang telah migrasi terbuat dengan benar. Caranya adalah kita masuk kembali ke MySQL lalu kita masukan perintah dibawah untuk melihat daftar database yang ada

```mysql
SHOW DATABASES;
```

Setelah itu kita pilih database ***db-wayshub*** dengan menjalankan perintah:

```mysql
use db-wayshub;
```

Lalu kita munculkan isi table pada database ***db-wayshub*** dengan menjalankan perintah:

```mysql
SHOW TABLES;
```
<br>
Dapat dilihat dari gambar diatas bahwa database yang ada telah ter-migrasi dengan lengkap, Maka dapat disimpulkan bahwa langkah-langkah yang dilakukan diatas sudah benar kita lakukan.

# 2. Gateway NGINX

## 2.1 Konfigurasi VM untuk Gateway Server di IdCloudHost
<img width="1440" alt="Screenshot 2023-09-22 at 16 35 38" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/15e7c17b-bd43-4681-93e8-4d96c67c6ac7">
Berikut konfigurasi VM untuk Gateway Servernya

> Processor: 2 vCPU,
> 
> Memory: 2GB RAM,
>
> Storage: 20GB,
> 
> Operating System: Ubuntu 20.04 LTS
>
> IP Public: 103.187.146.52
>
> IP Private: 10.36.116.221
<br>

## 2.2 Instalasi NGINX
<img width="1440" alt="Screenshot 2023-09-21 at 03 12 31" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/14466f4d-0b1a-4745-872f-d3c2d193f2cf">
Langkah pertama, Sebagai Gateway yang akan menjaga App Server dari serangan yang tidak diinginkan, Maka kita memerlukan NGINX sebagai Proxy agar App Server tidak mudah diserang oleh pihak yang tidak bertanggung jawab. Lalu kita install service NGINX dengan menjalankan perintah:

```shell
sudo apt install nginx
```

## 2.3 

