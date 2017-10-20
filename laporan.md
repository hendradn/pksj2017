# Pendahuluan
# Dasarteori
## OS
Kami menggunakan os ubuntu-14.04.5-server-i386 sebagai server dan os ubuntu-17.04-dekstop
## TOOLS
# Ujipenetrasi1
## LangkahinstalasiUbuntu server
1. Buka Oracle VM virtual Box Manager, Buat virtual mesin baru dengan mengklik ikon NEW pada toolbar dan isi option dengan :
name : Ubuntu Server
Type : Linux
Version : Ubuntu (64-bit)
Memory : 4 Gb

{Gambar 1}

2. Siapkan iso ubuntu server yang dapat didownload di : http://kartolo.sby.datautama.net.id/ubuntu-cd/17.10/ubuntu-17.10-server-amd64.iso

3. Pilih mesin viortual yang telah dibuat, dan klik start. Pilih iso ubuntu server.
{GAMBAR 2}

4. Pilih English
{GAMBAR 3}
5. Pilih Install Ubuntu Server
{GAMBAR 4}
6. Pilih Bahasa English
{GAMBAR 5}
7. Pilih Lokasi other
{Gambar 6}
8. Pilih benua asia
{Gambar 7}
9. Pilih Indonesia
{Gambar 8}
9. Isi option - option yang lain
10. Tunggu instalasi 
{Gambar 9}
11. Isi Hostname, full name, username,password
TEST
{Gambar 10}
12. Jika muncul beberapa option, seperti partition, gunakan setting default
13. Akan muncul settingan proxy
{Gambar 11}
14. Akan muncul tawaran install software , piloih opensshserver
15. Instalasi sealesai
{Gambar 12}
## Langkah instalasi OS untukpenetrasi
## Langkah instalasi SSH server
1. Login ke ubuntu server
2. Ketikkan perinta sudo apt-get install openssh-server
{Gambar 13}
## Langkah uji penetrasi dengan SSH brute force tools
