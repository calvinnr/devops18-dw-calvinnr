# 1. Deploy Wayshub

## 1.1 Konfigurasi VM di IdCloudHost
<img width="1440" alt="Screenshot 2023-09-21 at 02 21 34" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/56fbecd3-288f-43be-a2a5-62ea12631365">
<br>
<br>
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
<br>
<br>
Setelah Masuk kedalam VM, Hal pertama yang dilakukan adalah melakukan clone repository yang dibutuhkan untuk keperluan task dengan menjalankan perintah:
<br>
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
<br>
<br>
Setelah Cloning Repository selesai dilakukan, Langkah selanjutnya kita perlu meng-install NVM Terlebih dahulu dengan menjalankan perintah:
<br>
<br>

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
<br>
<br>
Langkah selanjutnya yang kita perlu lakukan meng-install PM2 yang dimana nanti akan kita gunakan untuk men-deploy aplikasi Frontend & Backend-nya dengan menjalankan perintah:

```shell
npm install -g pm2
```
<br>

## 1.5 Konfigurasi API pada Wayshub-Frontend
<img width="1440" alt="Screenshot 2023-09-21 at 02 32 14" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/05a85419-deaa-49c9-b380-8016e45901b7">
<br>
<br>
Setelah semua package yang dibutuhkan telah ter-install, Tahap pertama agar Wayshub Frontend dapat terhubung dengan Wayshub Backend kita perlu mengkongfigurasi API-nya. Lalu kita masuk ke directory Wayshub Frontend lalu masuk ke dir Src/ setelah itu masuk ke dir Config/ setelah itu kita edit api.js-nya
<br>
<br>
<img width="1440" alt="Screenshot 2023-09-21 at 02 32 26" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/911837c7-cfc7-4ad3-b9ed-83aa8a0c42ea">
<br>
<br>
Disini kita rubah BaseURL-nya dengan URL yang telah disediakan. Disini saya menggunakan domain

> api.calvin.studentwayshub.my.id
<br>

## 1.6 
