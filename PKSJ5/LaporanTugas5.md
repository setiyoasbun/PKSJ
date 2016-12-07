# Laporan Tugas 5 PKSJ
## Pendahuluan
Laporan ini dibuat sebagai tugas 5 dari mata kuliah Perancangan Keamanan dan Sekuritas Jaringan (PKSJ). Pada laporan ini terdapat penjelasan-penjelasan dasar teori dan hasil percobaan mengamati serangan Metasploit terhadap Metasploitable. Laporan ini 
disusun oleh :
- Setiyo Adiwicaksono : 5113100020
- Fajar Ade Putra : 5113100092
- Anwar Rosyidi : 5113100180

## Dasar Teori
### OS yang digunakan
1. Ubuntu Desktop 14.04 : Ubuntu Desktop 14.04 adalah ubuntu yang didesain untuk di install pada PC Desktop. Ubuntu ini menggunakan GUI dengan dasaran GNOME. OS ini yang nantinya akan diinstal Metasploit untuk melakukan penetrasi

### Tools yang digunakan
1. Metasploit : Adalah sebuah aplikasi yang mampu melakukan hacking pada sebuah sistem yang digunakan untuk keperluan testing produk. Metasploit menyediakan layanan yang sangat memudahkan pengguna untuk melakukan penetration testing

## Langkah Pengerjaan
### Instalasi Metasploit
1. Pertama kita install dulu dependensi yang dibutuhkan metasploit dengan menjalankan pada terminal perintah berikut
```
sudo apt-get install build-essential libreadline-dev libssl-dev libpq5 libpq-dev libreadline5 libsqlite3-dev libpcap-dev openjdk-7-jre git-core autoconf postgresql pgadmin3 curl zlib1g-dev libxml2-dev libxslt1-dev vncviewer libyaml-dev curl zlib1g-dev
```

2. Setelah instalasi dependensi selesai, mlai kita install untuk Metasploit Frameworknya dengan memasukkan perintah pada terminal. Pertama, masuk ke folder "opt"
```
cd /opt
```
Lalu clone repository metasploit framework
```
sudo git clone https://github.com/rapid7/metasploit-framework.git
```
Setelah itu mulai instalasi metasploit framework
```
sudo chown -R `whoami` /opt/metasploit-framework &
cd metasploit-framework &
gem install bundler &
bundle install
```
Setelah metasploit terinstall dengan baik, setting environment agar bisa menjalankan metasploit tanpa harus masuk ke folder nya dengan cara
```
sudo bash -c 'for MSF in $(ls msf*); do ln -s /opt/metasploit-framework/$MSF /usr/local/bin/$MSF;done' 
```

3. Setelah metasploit framework terinstall dengan baik, kita akan menginstal Armitage, GUI untuk metasploitnya. Untuk install GUI, jalankan perintah dibawah.
Pertama, download dulu file armitagenya
```
curl -# -o /tmp/armitage.tgz http://www.fastandeasyhacking.com/download/armitage-latest.tgz
```
Lalu Ekstrak file hasil downloadnya
```
sudo tar -xvzf /tmp/armitage.tgz -C /opt
```
Lalu jalankan perintah dibawah untuk instalasinya
```
sudo ln -s /opt/armitage/armitage /usr/local/bin/armitage &
sudo ln -s /opt/armitage/teamserver /usr/local/bin/teamserver &
sudo sh -c "echo java -jar /opt/armitage/armitage.jar \$\* > /opt/armitage/armitage" &
sudo perl -pi -e 's/armitage.jar/\/opt\/armitage\/armitage.jar/g' /opt/armitage/teamserver
```