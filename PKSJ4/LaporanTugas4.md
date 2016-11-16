# Laporan Tugas 4 PKSJ
## Pendahuluan
Laporan ini dibuat sebagai tugas 4 dari mata kuliah Perancangan Keamanan dan Sekuritas Jaringan (PKSJ). Pada laporan ini terdapat penjelasan-penjelasan dasar teori dan hasil percobaan mengamati serangan DDOS menggunakan tools snort. Laporan ini 
disusun oleh :
- Setiyo Adiwicaksono : 5113100020
- Fajar Ade Putra : 5113100092
- Anwar Rosyidi : 5113100180

## Dasar Teori

### OS yang digunakan 
1. Ubuntu Server 14.04 : Ubuntu server adalah ubuntu yang didesain untuk di install di server. Perbedaan mendasar, di Ubuntu Server tidak tersedia GUI. Jika anda menggunakan ubuntu server artinya anda harus bekerja dengan perintah perintah di layar hitam ayng sering disebut konsole. Jika anda datang dari windows, maka tampilan ubuntu server seperti DOS.

### Tools yang digunakan
1. Snort 2.9.8 : Snort adalah sebuah software ringkas yang sangat berguna untuk mengamati aktivitasdalam suatu jaringan komputer. Snort dapat digunakan sebagai suatu Network IntrusionDetection System (NIDS) yang berskala ringan (lightweight), dan software inimenggunakan sistem peraturan-peraturan (rules system) yang relatif mudah dipelajariuntuk melakukan deteksi dan pencatatan (logging) terhadap berbagai macam seranganterhadap jaringan komputer. 
2. Idswakeup : idswakeup adalah sebuah aplikasi untuk sistem pendeteksian intrutions/ penyusup

## Langkah Pengerjaan

### Instalasi snort
1. Install library yang dibutuhkan snort yaitu : liblzma-dev, opensslm libssl-dev dengan cara
```
sudo apt-get install -y zlib1g-dev liblzma-dev openssl libssl-dev
```
2. Setelah menginstall library diatas, maka kita siap untuk install Snort
```
cd ~/snort_src
wget https://snort.org/downloads/snort/snort-2.9.8.0.tar.gz
tar -xvzf snort-2.9.8.0.tar.gz
cd snort-2.9.8.0
./configure --enable-sourcefire
make
sudo make install
```
3. Jika mengalami kesulitan maka bisa dibantu dengan melihat semua list compile-time	
```
n ./configure --help
```
4. Jalankan perintah berikut untuk memperbaharui shared library	
```
sudo ldconfig
```
5. Tempatkan snort binary di usr/sbin:
```
sudo ln -s /usr/local/bin/snort /usr/sbin/snort
```
6. Untuk melihat snortnya udah keinstall jalankan perintah berikut
```
snort -V
```

###Konfigurasi Snort
- Buat directory yang dibutuhkan oleh snort dan atur privilleged dari folder yang dibuat

```
# Create the snort user and group:
sudo groupadd snort
sudo useradd snort -r -s /sbin/nologin -c SNORT_IDS -g snort

# Create the Snort directories:
sudo mkdir /etc/snort
sudo mkdir /etc/snort/rules
sudo mkdir /etc/snort/rules/iplists
sudo mkdir /etc/snort/preproc_rules
sudo mkdir /usr/local/lib/snort_dynamicrules
sudo mkdir /etc/snort/so_rules

# Create some files that stores rules and ip lists
sudo touch /etc/snort/rules/iplists/black_list.rules
sudo touch /etc/snort/rules/iplists/white_list.rules
sudo touch /etc/snort/rules/local.rules
sudo touch /etc/snort/sid-msg.map
# Create our logging directories:
sudo mkdir /var/log/snort
sudo mkdir /var/log/snort/archived_logs

# Adjust permissions:
sudo chmod -R 5775 /etc/snort
sudo chmod -R 5775 /var/log/snort
sudo chmod -R 5775 /var/log/snort/archived_logs
sudo chmod -R 5775 /etc/snort/so_rules
sudo chmod -R 5775 /usr/local/lib/snort_dynamicrules
```
- Ubah ownership dari file yang telah kita buat sebelumnya
```
# Change Ownership on folders:
sudo chown -R snort:snort /etc/snort
sudo chown -R snort:snort /var/log/snort
sudo chown -R snort:snort /usr/local/lib/snort_dynamicrules
```
- Salin snort configuration file ke dalam folder snort
```
cd ~/snort_src/snort-2.9.8.0/etc/
sudo cp *.conf* /etc/snort
sudo cp *.map /etc/snort
sudo cp *.dtd /etc/snort
cd ~/snort_src/snort-2.9.8.0/src/dynamic-preprocessors/build/usr/local/lib/snort_dynamicpreprocessor/
sudo cp * /usr/local/lib/snort_dynamicpreprocessor/
```
- comment semua ruleset yang terdapat pada file snort.conf
```
sudo sed -i "s/include \$RULE\_PATH/#include \$RULE\_PATH/" /etc/snort/snort.conf
```
- pada line 45 di file snort.conf setting ipvar sesuai dengan ip internal network
```
ipvar HOME_NET 10.0.0.0/24
```
- pada line 104 di file snort.conf copy kode berikut
```
var RULE_PATH /etc/snort/rules
var SO_RULE_PATH /etc/snort/so_rules
var PREPROC_RULE_PATH /etc/snort/preproc_rules
var WHITE_LIST_PATH /etc/snort/rules/iplists
var BLACK_LIST_PATH /etc/snort/rules/iplists
```
- pada line 545 di snort.conf uncomment line tersebut
```
include $RULE_PATH/local.rules
```
- lakukan perintah
```
sudo snort -T -c /etc/snort/snort.conf -i eth0
```
- untuk uji coba configurasi yang telah kita lakukan jalankan perintah
```
user@snortserver:~$ sudo snort -T -i eth0 -c /etc/snort/snort.conf
(...)
Snort successfully validated the configuration!
Snort exiting
user@snortserver:~$
```