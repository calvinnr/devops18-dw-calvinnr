# Infrastructre as Code

## Terraform

### 1. Dengan mendaftar akun free tier AWS/GCP/Azure, buatlah Infrastructre dengan terraform menggunakan registry yang sudah ada.

#### 1.1 Instalasi Terraform
<img width="1440" alt="Screenshot 2023-10-07 at 13 44 45" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/43af78a9-ee3d-4539-a8c1-3f3ed843af42">

Pertama-tama, kita harus memastikan bahwa package-package sudah ter-update dan pada server sudah ter-install `gnupg`, `software-properties-common` dan `curl` karena package-package tersebut akan digunakan untuk mem-verifikasi HashiCorp's GPG signature dan meng-install HashiCorp's Debian package repository dengan menjalankan perintah

```terraform
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
```
<br>

<img width="1440" alt="Screenshot 2023-10-07 at 13 45 24" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/27210f27-2aaa-4987-9868-491e668464e9">

Lalu, kita install HashiCorp's GPG key-nya dengan menjalankan perintah:

```terraform
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
```
<br>

<img width="1440" alt="Screenshot 2023-10-07 at 13 45 41" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/60dc040a-49c4-47a5-a44a-0bc97d0d95ec">

Setelah ter-install, kita verifikasi key-nya dengan menjalankan perintah:
```terraform
gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint
```
<br>

<img width="1440" alt="Screenshot 2023-10-07 at 13 45 59" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/be25df69-16e5-4d8d-9b3b-c913c759b4c2">

Tambahkan official HashiCorp repository ke server dengan menjalankan perintah:

```terraform
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
```
<br>

<img width="1440" alt="Screenshot 2023-10-07 at 13 46 28" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/7a7fc2ac-e610-457e-a598-c5beea1b3e43">

Download informasi-informasi package dari HashiCorp dengan menjalankan perintah:

```terraform
sudo apt update
```
<br>

<img width="1440" alt="Screenshot 2023-10-07 at 13 47 14" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/5d07beb3-ebe1-4a86-92b0-6c1ca3833bee">

Install Terraform-nya dengan menjalankan perintah:

```terraform
sudo apt-get install terraform
```
<br>

<img width="1440" alt="Screenshot 2023-10-07 at 13 47 33" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/3d7cccd9-4c0e-4fd2-bc54-2d6d510fefeb">

Lalu kita verifikasi bahwa Terraform sudah berjalan pada server dengan menjalankan perintah:

```terraform
terraform -help
```
Lalu jika muncul tampilan seperti gambar diatas, maka Terraform sudah berjalan pada server.

### 1.2 Instalasi AWS CLI
Karena disini saya menggunakan **Amazon Web Services** sebagai contoh implementasi *Infrastructure Provisioning* menggunakan Terraform. Maka ada 3 Prasyarat yang harus dipenuhi yaitu

> 1. Terraform CLI (1.2.0+) sudah ter-install.
> 2. AWS CLI sudah ter-install.
> 3. Akun AWS dan kredential terkait yang memberikan izin untuk membuat resources.

<img width="1440" alt="Screenshot 2023-10-07 at 13 56 45" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/e81c8fca-7d14-46d7-a2ae-b4a9534dfa56">

Download AWS CLI versi bundled installer menggunakan `curl` dengan menjalankan perintah:

```terraform
curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
```
<br>

<img width="1440" alt="Screenshot 2023-10-07 at 13 57 36" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/8630c484-d884-4a51-a2d0-4e7716b34b69">

Extraksi isi file yang ada di dalam package dengan menjalankan perintah:

```terraform
unzip awscli-bundle.zip
```
<br>

<img width="1440" alt="Screenshot 2023-10-07 at 13 59 34" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/2b473ca3-dcf7-4d26-a9d8-c4c4f8dee260">

Instalasi versi Python 3.8 Virtual Environment dengan menjalankan perintah:

```terraform
sudo apt install python3.8-venv
```
<br>

<img width="1440" alt="Screenshot 2023-10-07 at 13 59 23" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/6f581f66-8ee7-4cad-9222-66cd7e413055">

Secara default, script akan berjalan sesuai dengan Python bawaan yang sudah ter-install pada server. Tetapi karena disini saya ingin menggunakan versi Python 3.8 untuk menjalankan instalasi AWS CLI-nya, saya menjalankan perintah berikut dengan men-define library dari Python 3.8 dengan menjalankan perintah:

```terraform
sudo /usr/bin/python3.8 awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
```
<br>

<img width="1440" alt="Screenshot 2023-10-07 at 14 03 13" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/495ad72e-66f2-4fab-9ff2-ed8fd102903b">

Lalu jika sudah ter-install, kita verifikasi bahwa AWS CLI sudah berjalan pada server dengan menjalankan perintah:

```terraform
aws --version
```
<br>

### 1.3 Konfigurasi Access Keys
<img width="1440" alt="Screenshot 2023-10-07 at 14 05 30" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/bbdb3471-788d-4e56-bb1b-5899c23d969b">

Pertama, kita masuk ke Console AWS-nya. Lalu kita klik nama profile kita pada ujung kanan setelah itu akan muncul menu dropdown lalu pilih *Security credentials*
<br>
<br>

<img width="1440" alt="Screenshot 2023-10-07 at 14 05 54" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/757bf0c4-a4c0-463d-a5be-ff894990fa0d">

Setelah itu scroll kebawah hingga menemukan *Access keys* setelah itu klik *Create access key*
<br>
<br>

<img width="1440" alt="Screenshot 2023-10-07 at 14 06 06" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/ed169c23-7a86-4f97-a029-8cdc29644425">

*Access keys* yang sudah terbuat disimpan untuk kita gunakan konfigurasi environment AWS-nya

 ### 1.4 Membuat Infrastruktur AWS menggunakan Terraform
 <img width="1440" alt="Screenshot 2023-10-07 at 14 07 03" src="https://github.com/calvinnr/devops18-dw-calvinnr/assets/101310300/0f7d3aa1-f99c-4a2f-a532-c9423e494a4a">

Pertama kita konfigurasi Access Keys yang sudah kita buat tadi agar Terraform memiliki akses untuk membuat Resources di AWS dengan menjalankan perintah:

```terraform
aws configure
```

Disini saya spesifikasi sebagai berikut:

> AWS Access Key ID: (access-key)
>
> AWS Secret Access Key: (secret-access-key)
>
> Default region name: ap-southeast-1 (Singapore)
> 
> Default output format: (blank)



 







