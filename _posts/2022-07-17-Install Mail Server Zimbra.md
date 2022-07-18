---
title: "Instalasi Mail Server di Ubuntu using Zimbra"
date: 2022-07-17
category: Application
---
						Bismillahirrahmanirahim
						 Assalamualaikum Wr.Wb

Instalasi ini dilakukan pada konfigurasi berikut ini, apabila ada perbedaan versi silahkan di UP.


| System        |   VirtualGuest/Os     | IP/Host     |
| ------------- | --------------------- |------------- |
| Proxmox 7.1.2 |Container/Ubuntu 20.04  | Static~IPV6|

Pertama" siapkan domain untuk dipakai sebagai domain email, disini saya pake domain pribadi

setelah itu set DNS Record A(ipv4) dan AAAA(ipv6) ke IP Server 

lalu jangan lupa set MX Record ke domain A/AAAA Record dengan konfigurasi seperti berikut :

Type : MX
Name : mail
Priority : 10
Value : "isikan dengan domain A/AAAA Record"
TTL : 1Hour

Simpan

Jika sudah pastikan MX Record berhasil dideteksi dengan menginputkan pengecekan di web https://mxtoolbox.com .

masukkan alamat MX Record dan cek hasilnya
<img width="1338" alt="Screen Shot 2022-07-17 at 21 00 41" src="https://user-images.githubusercontent.com/22628150/179401883-0aba6939-39bf-49ce-beee-26e86661483b.png">
Jika muncul seperti diatas berarti pointing MX ke domain belum berhasil
Jika konfigurasi benar maka tampilan akan seperti ini
<img width="1338" alt="image" src="https://user-images.githubusercontent.com/22628150/179402135-85d5d892-9921-4a36-9aea-bfe2ecc8db24.png">
Jika sudah maka setting Domain sudah selesai, selanjutnya masuk ke instalasi Zimbra

Masuk ke Ubuntu

# apt-get update
# apt-get upgrade

# ls -la

<img width="467" alt="image" src="https://user-images.githubusercontent.com/22628150/179402663-a3ce8c1e-cc7a-4120-a11e-7e0cdf8ef20c.png">

Ini buat install versi zimbra versi terbaru 9.0.0

# wget https://files.zimbra.com/downloads/9.0.0_GA/zcs-NETWORK-9.0.0_GA_4178.UBUNTU20_64.20211112031526.tgz
# tar zxvf zcs-NETWORK-9.0.0_GA_4178.UBUNTU20_64.20211112031526.tgz

>> Untuk versi yg sbelumnya pake ini :
# wget https://files.zimbra.com/downloads/8.8.15_GA/zcs-8.8.15_GA_4179.UBUNTU20_64.20211118033954.tgz
# tar zxvf zcs-8.8.15_GA_4179.UBUNTU20_64.20211118033954.tgz

# ls -la
<img width="937" alt="image" src="https://user-images.githubusercontent.com/22628150/179404561-b461b471-ecf7-4908-b0a0-3d73d5fd3e15.png">
Maka tampian terbaru seperti diatas

lanjut

# mv zcs-NETWORK-9.0.0_GA_4178.UBUNTU20_64.20211112031526 zcs
# cd zcs
<img width="600" alt="image" src="https://user-images.githubusercontent.com/22628150/179404688-0cf25851-50d4-4c71-82dd-2f03ed5820ab.png">
~/zcs# ./install.sh 
Ketik Y
Ketik Y
Ketik Y
Jika keluar seperti dibawah
<img width="937" alt="image" src="https://user-images.githubusercontent.com/22628150/179404905-d30a25bf-b17e-476f-87ed-f2fd0f6dfa0c.png">
Eror padad gnupg maka kita install dulu gnupg

# apt-get update && apt-get install -y gnupg

Jika sudah ulangi
~/zcs# ./install.sh

Jika muncul eror seperti ini
<img width="446" alt="image" src="https://user-images.githubusercontent.com/22628150/179405513-efb12c15-f59e-4300-bb53-7e57662d62bb.png">
coba jalankan

# apt-get purge postfix

Jika sudah coba ulangi
~/zcs# ./install.sh
Ketik Y jika ada commnd keluar (20X kalo gasalah)
Ada eror masalah domain , pas reboot eror connect LDAP caranya 
~/zcs# ./install.sh -u

Lalu install lagi
~/zcs# ./install.sh -u
Ketik Y jika ada commnd keluar (20X kalo gasalah)
Ketik sudah muncul DNS Error resolving .....
isikan dengan nameserver dari domain yang dibeli
biasanya ns.......com

jika sudah akan muncul Re-enter Hostname isikan dengan nameserver tadi
jika lancar akan muncul seperti dibawah
<img width="422" alt="Screen Shot 2022-07-17 at 23 14 37" src="https://user-images.githubusercontent.com/22628150/179410960-dbf77b93-7f9f-4c0d-ab08-3a28398aaf30.png">
lalu tekan 7
lalu tekan 4
Masukkan Password :
tekan r
tekan a untuk apply

Step pake versi 8.xx

Change hostname [yes] : yes
Please enter the logical hostname for this host [xxxx:nameservermu.com] nameservermu.com

Change domain name? [Yes] yes
Create domain: [nameservermu.com] domainmu.com
lalu tekan 7
lalu tekan 4
Masukkan Password :
tekan r
tekan a untuk apply
ketik yes
klik enter
ketik yes

melanjutkan setup yg tertunda 













