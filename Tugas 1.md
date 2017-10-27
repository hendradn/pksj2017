# Anggota Kelompok

1. 5114100031 ANDRE EXAUDI JEREMY RUMAPEA
2. 5114100043 JEFFRY NASRI FARUKI
3. 5114100073 HENDRA DARMAWAN

# Pendahuluan

Dalam laporan ini akan dilakukan uji penetrasi  terhadap server. Dalam praktiknya Kami menggunakan os ubuntu-14.04.5-server-i386 sebagai server dan dan os ubuntu-17.04-dekstop sepagai penyerang. tools yang kami pakai dalam uji coba adalah hydra dan ncrack. Dalam laporan ini akan dilakukan 2 kali uji coba penetrasi, dimana yang pertama virtual server hanya terinstall openssh . Yang kedua viertual server terinstall openssh dan fail2ban

# Dasar teori
## OS Ubuntu Server
Ubuntu server adalah ubuntu yang didesain untuk di install di server. Perbedaan mendasar, di Ubuntu Server tidak tersedia GUI. Jika anda menggunakan ubuntu server artinya anda harus bekerja dengan perintah perintah di layar hitam ayng sering disebut konsole. Jika anda datang dari windows, maka tampilan ubuntu server seperti DOS.Kami menggunakan os ubuntu server versi 14.04.5-server-i386

## OS Ubuntu Dekstop
Ubuntu adalah salah satu distribusi Linux yang berbasiskan pada Debian dan memiliki interface desktop. Proyek Ubuntu disponsori oleh Canonical Ltd (perusahaan milik Mark Shuttleworth). Kami menggunakan os ubuntu server versi 17.04-dekstop

## Tools Hydra
Hydra adalah cracker login paralel yang mendukung banyak protokol untuk menyerang. Ini sangat cepat dan fleksibel, dan modul baru mudah ditambahkan. Alat ini memungkinkan para periset dan konsultan keamanan untuk menunjukkan betapa mudahnya mendapatkan akses yang tidak sah ke sistem jarak jauh.

Ini mendukung: Cisco AAA, Cisco auth, Cisco memungkinkan, CVS, FTP, HTTP (S) -FORM-GET, HTTP (S) -FORM-POST, HTTP (S) -GET, HTTP (S) -HEAD, HTTP- Proxy, ICQ, IMAP, IRC, LDAP, MS-SQL, MySQL, NNTP, Oracle Listener, Oracle SID, PC-Anywhere, PC-NFS, POP3, PostgreSQL, RDP, Rexec, Rlogin, Rsh, SIP, SMB (NT) , SMTP, SMTP Enum, SNMP v1 + v2 + v3, SOCKS5, SSH (v1 dan v2), SSHKEY, Subversion, TeamSpeak (TS2), Telnet, VMware-Auth, VNC dan XMPP.


## Tools NCrack
Ncrack adalah alat cracking otentikasi jaringan berkecepatan tinggi. Ini dibangun untuk membantu perusahaan mengamankan jaringan mereka dengan secara proaktif menguji semua host dan perangkat jaringan mereka dengan kata kunci yang buruk. Profesional keamanan juga mengandalkan Ncrack saat mengaudit klien mereka. Ncrack dirancang menggunakan pendekatan modular, sintaks baris perintah yang mirip dengan Nmap dan mesin dinamis yang dapat menyesuaikan perilakunya berdasarkan umpan balik jaringan. Ini memungkinkan dilakukannya audit berskala besar yang cepat namun dapat diandalkan dari beberapa host.

Fitur Ncrack mencakup antarmuka yang sangat fleksibel yang memberi pengguna kontrol penuh atas operasi jaringan, memungkinkan serangan bruteforcing yang sangat canggih, template waktu untuk kemudahan penggunaan, interaksi runtime yang mirip dengan Nmap dan banyak lagi. Protokol yang didukung meliputi RDP, SSH, HTTP (S), SMB, POP3 (S), VNC, FTP, SIP, Redis, PostgreSQL, MySQL, dan Telnet.

# Ujipenetrasi 1
## LangkahinstalasiUbuntu server
1. Buka Oracle VM virtual Box Manager, Buat virtual mesin baru dengan mengklik ikon NEW pada toolbar dan isi option dengan :
name : Ubuntu Server
Type : Linux
Version : Ubuntu (64-bit)
Memory : 4 Gb

![Gambar 1](https://lh4.googleusercontent.com/otvECxc5tNlKsvXrDGEjs7sjfI_MFYzyJIBEX7Wnaxf6gGwMV9gx3OtAt2XtSvTYNw5eT_a43PCO968=w1366-h662)

2. Siapkan iso ubuntu server yang dapat didownload di : http://releases.ubuntu.com/14.04/ubuntu-14.04.5-desktop-amd64.iso

3. Pilih mesin virtual yang telah dibuat, dan klik start. Pilih iso ubuntu server.

![Gambar 2](https://lh5.googleusercontent.com/EOLLyZUQdAwDyesL9oq5RJHmDXDc0lDGWMcsCCjvGLiNe_Ncd527Q2X04BI9mxHRvnZtViv0OYngnh8=w1366-h662)

4. Pilih English

![Gambar 3](https://lh3.googleusercontent.com/0ZmA627PKfVY4CP_9VpC1OwVOKzOsTO3ZjjCDjWnP9qwENH2GBBNpgYqf-J4nOLquHGPdwtRwd84n4c=w1366-h662)

5. Pilih Install Ubuntu Server

![Gambar 4](https://lh3.googleusercontent.com/G_XQSEQ9i5hI9PUAmVhkRniUTFgzxLF71psEYRMyKjAGvqTnKpN4e3P5e3uwD_K-JEAS3hg4qRBhD3s=w1366-h662)

6. Pilih Bahasa English

![Gambar 5](https://lh4.googleusercontent.com/DwcFDDNBIhp5s0YNJyUQdN24tNei4mJnJAiinsuRy3oGkxx4ynorr8COqUi2oXQpssblrzvVRjG46Aw=w1366-h662-rw)

7. Pilih Lokasi other

![Gambar 6](https://lh5.googleusercontent.com/VN6kzpjfBQFqrGk_7z_BnIii6ELhCG-dC3rrrz_IRm6-TBbI8wQ3D0KqxclLemkQug7Cb1_ZCtcrY0E=w1366-h662-rw)

8. Pilih benua asia

![Gambar 7](https://lh4.googleusercontent.com/RpoQCSAj-OSSusGLS1bQifj3N82E9pdJUQNOILnvY4gNeCLhKgjb4Rc6mZCqnTTpR3rFKa_fG8RdU2g=w1366-h662-rw)

9. Pilih Indonesia

![Gambar 8](https://lh5.googleusercontent.com/NRTGZD_H6ada5ecl9rce7CQj3vbyIJwWud-g-VX4y0Y0cjOEEFub3DEkNfVvg0eu3ijo-BnmV02n7ds=w1366-h662-rw)

9. Isi option - option yang lain
10. Tunggu instalasi 

![Gambar 9](https://lh4.googleusercontent.com/LwvryCx0YeDdTPZQ6be4JuCIT_9BtEgBQEQxlOB3CIBD8yNt7Y4bMEPwLy5EtQaGe78qZePj6Hqnmnk=w1366-h662-rw)

11. Isi Hostname, full name, username,password

![Gambar 10](https://lh5.googleusercontent.com/ZhAhoo-d6qDoFcSJX3uM4-XOfHBSvSGGPjla0TQ5PC3i1JwHLve9Y5ytBIpIOZSR4lhiKlxegO0VqwE=w1366-h662-rw)

12. Jika muncul beberapa option, seperti partition, gunakan setting default
13. Akan muncul settingan proxy

![Gambar 11](https://lh5.googleusercontent.com/W_Q91ovsDMWvXgw8FaIVEWhTmFrMxtK14gOv3MEkQ_UHIrFabJPOTuIRMyUpae_5BFwpVPEDBk49RHo=w1366-h662)

14. Instalasi sealesai

![Gambar 12](https://lh3.googleusercontent.com/kKK3KW4IZXdg32YIt-xXbPGbOWyGfUI_MjaVnUHf_BFU4PQr_Y4Z30m86jkSzLvl7_6WMX-byvSm4ns=w1366-h662-rw)

## Langkah instalasi OS untuk penetrasi
1. Siapkan Virtualbox dan file .iso yang akan kita gunakan, disini kami menggunakan Ubuntu Desktop versi 17.04
2. Install Virtualbox kemudian buat new, kemudian isikan nama dan OS yang akan diintall pada virtualbox
![Gambar 14](https://lh6.googleusercontent.com/lpcqCZ7qs-jnVQZq9_w3qkZhzVM6hp1XoaHx--DtacDpETBArLz_Yw0_fawgwod0ldu2AZcKIM3eM6w=w1366-h662)
3. Masukkan jumlah ram yang akan digunakan pada OS virtual, kemudian lanjutkan proses instalasi secara default
4. Start OS virtual yang tadi telah kita buat, kemudian pilih file iso yang telah kita download
![Gambar 15](https://lh4.googleusercontent.com/4OQpDznPQNUxbORMHQvcXdrrujMjxNo4Bfujou6Abz-aulisRcXNWIPJXwI6lLBYOIAyZ0WfddgHSNo=w1366-h613-rw)
5. Kemudian lakukan penginstalan ubuntu dengan memilih Install Ubuntu, lanjutkan proses penginstalan sama dengan cara penginstalan ubuntu server
![Gambar 16](https://lh6.googleusercontent.com/Vjcm_ELQDUernm4hl1epFmRhVC1-5Jl1e7vM8C85Jeklke8qnY_C3JTrDbwWYvlFnc1iIw2PtZ8_X2s=w1366-h613-rw)
6. Restart Ubuntu
## Langkah instalasi SSH server
1. Login ke ubuntu server
2. Ketikkan perinta sudo apt-get install openssh-server
![Gambar 13](https://lh5.googleusercontent.com/ZtAsqYWdIwFnRhcGBFAXSzLT71GQqBLvLJXHcqnVcoNihDBRyxDgZZr0TF3l7JUf86GjYxA_DdaZa0w=w1366-h662-rw)
## Langkah uji penetrasi dengan SSH brute force tools
LANGKAH-LANGKAH UJI PENETRASI
1. Setting virtual network ubuntu server dan ubuntu dekstop ke host only, dan pastikan promiscuous mode allow all
![Gambar 1](https://lh4.googleusercontent.com/Z4MH4Cs85bQsLi80n2L30h7Xjwu8TLOGhj9HeyJLXIriK65vCg_d09dqlj4N-g3jo5Y4qcmvzo6vDtA=w1366-h613)

2. Install openssh-server di ubuntu server dengan mengetikkan perintah :
sudo apt-get install openssh-server

3. Install hydra di ubuntu server dengan mengetikkan perintah :
sudo apt-get install hydra hydra-gtk 

4. Install ncrack di ubuntu server dengan mendownload file tarnya di https://nmap.org/ncrack/dist/ncrack-0.5.tar.gz 

5. Install dependensi libssl-dev agar ncrack bisa diinstall dengan mengetikkan perintah :
sudo apt-get install libssl-dev

6. Jalankan perintah :
tar -xzf ncrack-0.5.tar.gz
cd ncrack-0.5
./configure
make
su root
make install

7. Tes koneksi ssh dengan cara remote ubuntu server lewat ubuntu dekstop dengan mengetikkan perintah : 
ssh (username_ubuntu server)@(ip_ubuntu server)
![Gambar 2](https://lh3.googleusercontent.com/w8XeoNsOV1JJxs9vRcOBcfwhlk57VORYWiDJb7abw0Am-BZWu_c0RQDA3e2gvM429imbh3rqVP5ZlMM=w1366-h613-rw)

8. Buka hydra-gtk
* isi ip server pada kolom single target di tab target
* isi protocol ke ssh
* Centang show attempt
![Gambar 3](https://lh6.googleusercontent.com/W3jIgGj9oaekKk3UbOEodUuhik8FRauy_LfTDwqtujp8SnVgcKtwa8lomG8sSCnyfNWjai77Mx9-KSc=w1366-h613)

* Pada tab passwords, kolom username dan password dapat diisi 1 kata atau beberapa kata yang terbungkus dalam file teks
* Pada tab password metode penyerangan dapat dilakukan dengan list files atau generate otomatis
![Gambar 5](https://lh3.googleusercontent.com/QQmmpw57drgITkq9IUmeqU-yi2G9M38k4VNhxu4xFNlA_B-pBEKQzCOozAdmVdPa6YTQLexSOfqj5GQ=w1366-h613-rw)
* Untuk memulai, buka tab start dan klik tombol start
* Jika ketemu akan muncul seperti tampilan dibawah
![Gambar 4](https://lh6.googleusercontent.com/GbBGNwECXp9daIRTfgvK7JCkE8c6szXd5MG3WD6r0sX5Y7WdCPRwfSY_2gQE2f9hWAp_feyeBlTKhu4=w1366-h613)

9. Untuk ncrack, ketikkan perintah berikut di terminal :
ncrack -p 22 --user {username ubuntu server} -P (LISt password.txt) (IP ubuntu server) 
![Gambar 6](https://lh5.googleusercontent.com/VTYKJ7EsggRSEXY9qN-84KJ1AO8g3qJFujPAND0jX8589PwEPHcbdCTEIq_V4kBELJbfL13TlvdKYmM=w1366-h613-rw)

* Jika berhasil, tampilan akan seperti berikut :
![Gambar 7](https://lh5.googleusercontent.com/g98EX0OAXe0LVwrPws1CMvwgtSY4xMBYh_IG0oNcvQkcpPKFOPyLGx2F1Cbbw44hrHTx7fK9F83h-hg=w1366-h613)

# Ujipenetrasi 2
## Langkah uji penetrasi dengan SSH brute force tools
1. Install fail2ban dengan command sudo apt-get install fail2ban
2. Copy file fail2ban.conf menjadi fail2ban.local dengan command cp /etc/failban/failban2.conf /etc/failban/fail2ban.local
3. Copy file jail.conf menjadi jail.local dengan command cp /etc/failban/jail.conf /etc/failban/jail.local
4. Ubah bantime, findtime, dan maxretry pada jail.local sesuai dengan keinginan admin
(bantime=jumlah waktu(detik) yang digunakan untuk menge-ban host/IP jika telah melebihi jumlah akses(maxretry) selama waktu yang dibatasi(findtime),
findtime=jumlah waktu(detik) maksimal yang ditentukan apabila host/IP melakukan sejumlah akses(maxretry),
maxretry=jumlah akses yang diberikan kepada suatu host/IP apabila melebihi maxretry dalam suatu waktu(findtime) maka host/IP akan di ban sementara(bantime))
![Gambar 8](https://lh5.googleusercontent.com/q3fS8aLGQx9woujhNQtbYRk3pvVDjTrB3pZkySjXpf9Zofy9kYa7Q9oad2Y5bploB1ZAia7iuePyABo=w1366-h613-rw)
5. Jalankan perintah fail2ban-client start pada terminal untuk memulai fail2ban
6. Lakukan penetrasi menggunakan hydra, pada password list, password user kami ada pada try 77, tetapi hydra tidak memberikan status berhasil dan tetap melakukan attempt,
![Gambar 9](https://lh4.googleusercontent.com/oDba0p90J50YrrnGiLoUTtI5hQmBrTPT1xajyw7IiZOQfYIn_RBAIXo2hUbo5ZJTy2MlxgGqPvEvDmE=w1366-h613-rw)
7. Jalankan perintah fail2ban-client status (nama jail) untuk mengecek status jail, akan menampilkan jumlah host/IP yang sedang di ban dan IP dari host tersebut
![Gambar 10](https://lh6.googleusercontent.com/DY0P4ul0EBSSVKHJJKUxrxrLS-3rT2y6upP9xkFBBIUy9wICTLDXQCGXO1qoHT-6WiVs-toZ3NTqDiI=w1366-h613)

Tambahan
1. Kami mencoba untuk merubah urutan password pada password list untuk melihat apakah fail2ban bekerja
2. Password kami pindah pada urutan 7
3. Hydra berhasil melakukan attack apabila attempt yang dilakukan kurang dari maxretry
![Gambar 11](https://lh3.googleusercontent.com/4u_Ul6T_XryIy0coklEcc3zrwB0j5U9Pp4fWwoD2va4enX5FywbZfLhcgMumfq4SyifZf2IDz9u-6YA=w1366-h613-rw)

# Refrensi
  * http://www.candra.web.id/mengenal-ubuntu-server/
  * https://balajarlinux.wordpress.com/2008/02/04/pengenalan-apa-itu-ubuntu-serta-sejarah/
  * https://tools.kali.org/password-attacks/hydra
  * https://nmap.org/ncrack/
  
