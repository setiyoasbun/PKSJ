
#TUGAS 1 PKSJ 2016
##Pendahuluan
Laporan ini dibuat sebagai tugas 1 dari mata kuliah Peracangan Keamanan dan Sekuritas Jaringan. Pada laporan ini terdapat penjelasan-penjelasan dan hasil percobaan peneterasi SSH yang kami lakukan. 
Laporan ini disusun oleh :
Setiyo Adiwicaksono	:5113100020
Fajar Ade Putra			:5113100092
Anwar Rosyidi			:5113100180

### Uji coba yang dilakukan
####Uji penetrasi 1 :
Instal sebuah virtual OS dengan Ubuntu server
Instal SSH server dengan konfigurasi default
Instal satu lagi virtual OS dengan OS bebas, misalnya Kali Linux atau Ubuntu Desktop
Pastikan tools untuk SSH brute force attack sudah terinstal
Lakukan uji penetrasi 1: dengan THC-Hydra atau Ncrack dan catat hasil uji penetrasi

#### Uji penetrasi 2 :
nstal fail2ban pada Ubuntu server yang telah diinstal SSH servernya
Konfigurasilah SSH server agar tidak default lagi
Lakukan uji penetrasi 2 dengan tools yang sama dan catat hasilnya


##Dasar Teori
### OS yang digunakan
1. Ubuntu Server 14.04 : Ubuntu server adalah ubuntu yang didesain untuk di install di server. Perbedaan mendasar, di Ubuntu Server tidak tersedia GUI. Jika anda menggunakan ubuntu server artinya anda harus bekerja dengan perintah perintah di layar hitam ayng sering disebut konsole. Jika anda datang dari windows, maka tampilan ubuntu server seperti DOS.

2. Xubuntu :Xubuntu adalah sebuah distribusi Linux dan varian resmi yang berbasiskan Ubuntu yang menggunakan lingkungan desktop Xfce. Xubuntu ditujukan untuk pengguna yang menggunakan komputer dengan kinerja rendah atau mereka yang mencari lingkungan meja yang lebih efisien pada komputer dengan kinerja tinggi.


###Tools yang digunakan
1. Medusa : Medusa adalah suatu aplikasi untuk melakukan bruteforce attacking ke server. Bekerja dengan cara mencoba satu persatu user name dan password hingga username dan password pada server ditemukan, jika entri username dan password sesuai dengan yang ada di server.

2. SSH Server :SSH adalah akronim dari Secure Shell yang merupakan sebuah protokol jaringan yang memanfaatkan kriptografi untuk melakukan komunikasi data pada perangkat jaringan agar lebih aman. Dalam konsepnya penggunaan SSH ini harus di dukung oleh server maupun perangkat atau komputer klien yang melakukan pertukaran data. Keduanya harus memiliki SSH server dari sisi komputer server dan SSH klien untuk komputer penerima (klien).

3. Fail2ban : adalah package keamanan yang digunakan untuk mencegah serangan brute-force dan DDoS pada linux. Fail2ban bekerja dengan memonitor jumlah kegagalan login untuk selanjutnya memblok ip address dari login yang gagal tersebut.




