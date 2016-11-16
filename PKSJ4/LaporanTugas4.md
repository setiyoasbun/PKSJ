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
2. 
