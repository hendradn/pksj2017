# Anggota Kelompok

1. 5114100031 ANDRE EXAUDI JEREMY RUMAPEA
2. 5114100043 JEFFRY NASRI FARUKI
3. 5114100073 HENDRA DARMAWAN

# Pendahuluan

Dalam laporan ini akan dilakukan uji penetrasi  terhadap server. Dalam praktiknya Kami menggunakan os ubuntu-14.04.5-server-i386 sebagai server dan dan os ubuntu-17.04-dekstop sepagai penyerang. tools yang kami pakai dalam uji coba adalah hydra dan ncrack. Dalam laporan ini akan dilakukan 2 kali uji coba penetrasi, dimana yang pertama virtual server hanya terinstall openssh . Yang kedua viertual server terinstall openssh dan fail2ban

# Dasar teori

## OS Ubuntu Dekstop
Ubuntu adalah salah satu distribusi Linux yang berbasiskan pada Debian dan memiliki interface desktop. Proyek Ubuntu disponsori oleh Canonical Ltd (perusahaan milik Mark Shuttleworth). Kami menggunakan os ubuntu server versi 16.04-dekstop

## Tools Wordpress

WordPress adalah sebuah aplikasi sumber terbuka (open source) yang sangat populer digunakan sebagai mesin blog (blog engine). WordPress dibangun dengan bahasa pemrograman PHP dan basis data (database) MySQL. PHP dan MySQL, keduanya merupakan perangkat lunak sumber terbuka (open source software). Selain sebagai blog, WordPress juga mulai digunakan sebagai sebuah CMS (Content Management System) karena kemampuannya untuk dimodifikasi dan disesuaikan dengan kebutuhan penggunanya. WordPress adalah penerus resmi dari b2/cafelog yang dikembangkan oleh Michel Valdrighi. Nama WordPress diusulkan oleh Christine Selleck, teman Matt Mullenweg. WordPress saat ini menjadi platform content management system (CMS) bagi beberapa situs web ternama seperti CNN, Reuters, The New York Times, TechCrunch, dan lainnya .


## Plugin Video Player

Video player adalah plugin video WordPress yang memungkinkan Anda menambahkan video ke situs web dengan mudah. Ini memiliki kemungkinan untuk mengatur video menjadi daftar putar dan memilih tata letak pilihan untuk pemain

## Plugin League Manager

League manager adalah Plugin yangdirancang untuk mengelola liga olahraga dan menampilkannya di blog Anda.

## Tools SQLMap

Sqlmap adalah alat pengujian penetrasi open source yang mengotomatisasi proses mendeteksi dan mengeksploitasi kelemahan SQL injection dan mengambil alih dari database server. Muncul dengan mesin deteksi yang kuat, banyak fitur ceruk untuk penetrasi tester utama dan berbagai switch yang berlangsung dari database sidik jari, atas data mengambil dari database, untuk mengakses sistem file yang mendasari dan mengeksekusi perintah pada sistem operasi melalui out of-band koneksi.

## Tools WPScan

WPScan adalah scanner keamanan yang memeriksa keamanan WordPress menggunakan metode “black box”.WpScan ini ditulis dengan bahasa ruby.



# Uji penetrasi SQL Injection
## Langkah instalasi wordpress dan Vulnerable Plugin

1. Buka terminal
2. Install LAMP dengan cara mengetikkan perintah berikut :
```
sudo apt-get install apache2 mysql-server php7.0 php7.0-mysql libapache2-mod-php7.0 php7.0-cli php7.0-cgi php7.0-gd
```
3. Buat sebuah database di mysql yang digunakan sebagai database wordpress. dengan mengetikkan perintah berikut :
```
mysql -u root -p;
CREATE DATABASE wordpress;
GRANT ALL ON wordpress.* TO 'root'@'localhost' IDENTIFIED BY 'root';
FLUSH PRIVILEGES;
EXIT;
```
3. Unduh wordpress tarball di http://wordpress.org/latest.tar.gz
4. Ekstrak file ke direktori /var/www/html dengan mengetikkan perintah 
```
sudo tar -xvzf wordpress-4.8.3.tar.gz -C /var/www/html
```
5. Buka Browser dan ketikkan :

http://localhost/wordpress/wp-admin/install.php

6. Ikuti langkah-langkahnya
![alt text](https://github.com/hendradn/pksj2017/blob/master/Tugas%202/Screenshoot/1-instalasi.PNG)
![alt text](https://github.com/hendradn/pksj2017/blob/master/Tugas%202/Screenshoot/2-instalasi.PNG)
![alt text](https://github.com/hendradn/pksj2017/blob/master/Tugas%202/Screenshoot/3-instalasi.PNG)

7. Akan diminta unutk membuat file wp-config.php.Buat wp-config.php di /var/www/html

8. Ikuti langkah-langkah selanjutnya hingga selesai :
![alt text](https://github.com/hendradn/pksj2017/blob/master/Tugas%202/Screenshoot/4-instalasi.PNG)
![alt text](https://github.com/hendradn/pksj2017/blob/master/Tugas%202/Screenshoot/5-instalasi.PNG)

9. Log in ke akun wordpress
![alt text](https://github.com/hendradn/pksj2017/blob/master/Tugas%202/Screenshoot/6-instalasi.PNG)

10. Buka menu plugin dan klik tombol add new
![alt text](https://github.com/hendradn/pksj2017/blob/master/Tugas%202/Screenshoot/7-instalasi.PNG)

11. Ketikkan video player dan league manager di kotak pencarian dan klik install untuk masing-masing
![alt text](https://github.com/hendradn/pksj2017/blob/master/Tugas%202/Screenshoot/8-instalasi.PNG)
![alt text](https://github.com/hendradn/pksj2017/blob/master/Tugas%202/Screenshoot/9-instalasi.PNG)

12. Jika muncul error terkait FTP tambahkan baris berikut di wp-config.php :
```
define('FSMETHOD', 'direct');
```
13. Jika muncul error terkait PERMISION , ketikkan perintah berikut di terminal :
```
sudo chown -R www-data:www-data  /var/www/html/wordpress
find sudo /var/www/html -type d -exec chmod 755 {} \;
find sudo /var/www/html -type f -exec chmod 644 {} \;
```
14. Jika plugin berhasil terinstall, tampilan akan menjadi seperti berikut :
![alt text](https://github.com/hendradn/pksj2017/blob/master/Tugas%202/Screenshoot/11-instalasi.PNG)

### Instalasi WPScan

1. Install git terlebih dahulu dengan perintah
```
sudo apt-get install git
```
2. Install prerequisites
```
sudo apt-get install libcurl4-openssl-dev libxml2 libxml2-dev libxslt1-dev ruby-dev build-essential libgmp-dev zlib1g-dev
```
3. Clone git main branch dari WPScan, kemudian masuk ke folder WPScan, dan masukkan perintah sebagai berikut(line 3)
```
git clone https://github.com/wpscanteam/wpscan.git
cd wpscan
sudo gem install bundler && bundle install --without test development
```
### Instalasi sqlmap

1. Lakukan git clone dari repository sqlmap dan masuk ke folder sqlmap dengan perintah sebagai berikut
```
https://github.com/sqlmapproject/sqlmap.git
cd sqlmap
```
2. Jalankan sqlmap dengan menggunakan python
```
python sqlmap.py
```

## Langkah Penetrasi SQL Injection

1. Lakukan perintah ini untuk melakukan pull terbaru dari git WPScan dan update database
```
git pull
ruby wpscan.rb --update
```
2. Lakukan pengecekan plugin vulnerabilities plugin dari wordpress dengan perintah dibawah ini
```
ruby wpscan.rb --url http://yourwebsite.com --enumerate vp
```
Karena menggunakan localhost ganti http://yourwebsite.com dengan localhost/wordpress

3. Berikut adalah hasil dari pengecekan tersebut
![alt text](https://github.com/hendradn/pksj2017/blob/master/Tugas%202/Screenshoot/10-instalasi.PNG)

4.

# Kesimpulan dan Saran
## Defense

## Countermeasure


# Refrensi
  * https://id.wikipedia.org/wiki/WordPress
  * https://ourgeeks.blogspot.co.id/2016/01/apa-itu-sqlmap.html
  * https://rixzaldi.wordpress.com/2017/01/03/mencari-kelemahan-wordpress-site-dengan-wpscan/
  * https://id.wordpress.org/plugins/player/
  * https://wordpress.org/plugins/leaguemanager/
  
