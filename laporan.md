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

![Gambar 1](https://lh4.googleusercontent.com/otvECxc5tNlKsvXrDGEjs7sjfI_MFYzyJIBEX7Wnaxf6gGwMV9gx3OtAt2XtSvTYNw5eT_a43PCO968=w1366-h662)

2. Siapkan iso ubuntu server yang dapat didownload di : http://kartolo.sby.datautama.net.id/ubuntu-cd/17.10/ubuntu-17.10-server-amd64.iso

3. Pilih mesin viortual yang telah dibuat, dan klik start. Pilih iso ubuntu server.
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
14. Akan muncul tawaran install software , piloih opensshserver
15. Instalasi sealesai
![Gambar 12](https://lh3.googleusercontent.com/kKK3KW4IZXdg32YIt-xXbPGbOWyGfUI_MjaVnUHf_BFU4PQr_Y4Z30m86jkSzLvl7_6WMX-byvSm4ns=w1366-h662-rw)
## Langkah instalasi OS untuk penetrasi
1) Siapkan Virtualbox dan file .iso yang akan kita gunakan, disini kami menggunakan Ubuntu Desktop versi 17.04
2) Install Virtualbox kemudian buat new, kemudian isikan nama dan OS yang akan diintall pada virtualbox
![Gambar 14](https://lh6.googleusercontent.com/lpcqCZ7qs-jnVQZq9_w3qkZhzVM6hp1XoaHx--DtacDpETBArLz_Yw0_fawgwod0ldu2AZcKIM3eM6w=w1366-h662)
3) Masukkan jumlah ram yang akan digunakan pada OS virtual, kemudian lanjutkan proses instalasi secara default
4) Start OS virtual yang tadi telah kita buat, kemudian pilih file iso yang telah kita download
![Gambar 15](https://lh4.googleusercontent.com/4OQpDznPQNUxbORMHQvcXdrrujMjxNo4Bfujou6Abz-aulisRcXNWIPJXwI6lLBYOIAyZ0WfddgHSNo=w1366-h613-rw)
5) Kemudian lakukan penginstalan ubuntu dengan memilih Install Ubuntu, lanjutkan proses penginstalan sama dengan cara penginstalan ubuntu server
![Gambar 16](https://lh6.googleusercontent.com/Vjcm_ELQDUernm4hl1epFmRhVC1-5Jl1e7vM8C85Jeklke8qnY_C3JTrDbwWYvlFnc1iIw2PtZ8_X2s=w1366-h613-rw)
6) Restart Ubuntu
## Langkah instalasi SSH server
1. Login ke ubuntu server
2. Ketikkan perinta sudo apt-get install openssh-server
![Gambar 13](https://lh5.googleusercontent.com/ZtAsqYWdIwFnRhcGBFAXSzLT71GQqBLvLJXHcqnVcoNihDBRyxDgZZr0TF3l7JUf86GjYxA_DdaZa0w=w1366-h662-rw)
## Langkah uji penetrasi dengan SSH brute force tools
