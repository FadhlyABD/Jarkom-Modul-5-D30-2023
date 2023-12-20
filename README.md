# Jarkom-Modul-5-D30-2023

## Group Member    :
| Nama                              | NRP        |
|-----------------------------------|------------|
|Abdullah Yasykur Bifadhlil Midror  |5025211035  |
|Muhammad Ahyun Irsyada             |5025211251  |

Berikut adalah demo laporan untuk praktikum modul 5

## Topologi
Topologi yang digunakan untuk praktikum modul 5 adalah sebagai berikut.
| <p align="center"> Topologi </p> |
| -------------------------------------------- |
| <img src="https://github.com/FadhlyABD/Jarkom-Modul-5-D30-2023/blob/main/Images/topo5.jpg" width = "400"/> |

## Nomor 4
Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

**Penyelesaian**
  - Sein & Stark (Web Server)
```bash
iptables -A INPUT -p tcp --dport 22 -s 192.206.4.0/22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```

**Hasil**

https://github.com/thoriqagfi/Jarkom-Modul-5-B08-2023/assets/92865110/9b49c79a-005d-4c91-a52d-65bd64e8c03c

## Nomor 5
Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

**Penyelesaian**
  - Sein & Stark (Web Server)
```bash
# Izinkan akses ke Web Server pada senin-jumat pukul 08:00-16:00
iptables -A INPUT -p tcp --dport 80 -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
```

**Hasil**

https://github.com/thoriqagfi/Jarkom-Modul-5-B08-2023/assets/92865110/bed858f6-755b-40a9-9b5f-277ff3ae39e5

## Nomor 6
Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

**Penyelesaian**
  - Konfigurasi Sein & Stark (Web Server)
```bash
# Larangan Akses pada hari Senin-Kamis jam 12:00 - 13:00
iptables -A INPUT -p tcp --dport 80 -m time --timestart 12:00 --timestop 13:00 --weekdays Mon,Tue,Wed,Thu -j DROP

# Larangan akses pada hari jumat pada 11:00 - 13:00
iptables -A INPUT -p tcp --dport 80 -m time --timestart 11:00 --timestop 13:00 --weekdays Fri -j DROP
```

**Hasil**

https://github.com/thoriqagfi/Jarkom-Modul-5-B08-2023/assets/92865110/0e6f4bbb-79fb-4aae-bcb7-6623412b5be6

## Nomor 7
Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

**Penyelesaian**
  - Sein
```bash
# Soal 7
iptables -A PREROUTING -t nat -p tcp -d 192.206.4.2 --dport 80 -m statistics --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.206.4.2:80

iptables -A PREROUTING -t nat -p tcp -d 192.206.4.2 --dport 80 -j DNAT --to-destination 192.206.0.14:80
```

  - Stark
```bash
# Soal 7
iptables -A PREROUTING -t nat -p tcp -d 192.206.0.4 --dport 443 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.206.4.2:443

iptables -A PREROUTING -t nat tcp -d 192.206.0.4 --dport 443 -j DNAT --to-destination 192.206.0.14:443
```

## Nomor 8
Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

**Penyelesaian**
  - Sein
```bash
### apabila ingin meng-drop TCP 
iptables -A INPUT -p tcp -s 192.206.0.2 --dport 80 -m time --datestart 2023-10-19T00:00 --datestop 2024-02-15T00:00 -j DROP

### namun ingin drop semua, bisa digunakan :
iptables -A INPUT -s 192.206.0.2 -m time --datestart 2023-10-19T00:00 --datestop 2024-02-15T00:00 -j DROP

```

<img width="632" alt="Screenshot 2023-12-16 at 01 27 30" src="https://github.com/thoriqagfi/Jarkom-Modul-5-B08-2023/assets/86884506/a9daface-4509-48d8-b2aa-5a89e1dc67b8">

## Nomor 9
Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir  alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit. (clue: test dengan nmap)

**Penyelesaian**
  - Sein
```bash
# Soal No 9
iptables -A INPUT -p tcp --syn -m recent --name portscan --set
iptables -A INPUT -p tcp --syn -m recent --name portscan --rcheck --seconds 600 --hitcount  20  -j  DROP
```

  - Stark
```bash
# Soal No 9
iptables -N PORTSCAN
iptables -A PORTSCAN -m recent --set --name portscan
iptables -A PORTSCAN -m recent --update --seconds 600 --hitcount 20 --name portscan -j LOG --log-prefix "Portscan Detected: " --log-level 4
iptables -A PORTSCAN -m recent --update --seconds 600 --hitcount 20 --name portscan -j DROP
iptables -A INPUT -p tcp --tcp-flags SYN,ACK,FIN,RST RST -m limit --limit 2/s -j ACCEPT
iptables -A INPUT -p tcp --tcp-flags SYN,ACK,FIN,RST RST -j PORTSCAN
```

## Nomor 10
Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level.

**Penyelesaian**
logging dapat ditambahkan dengan syntax iptables berikut yang dijalankan di semua node server dan router

```bash
iptables -A INPUT -j LOG --log-level debug --log-prefix "Dropped Packet: " -m limit --limit 1/second --limit-burst 10
```
<img width="1274" alt="Screenshot 2023-12-16 at 01 41 57" src="https://github.com/thoriqagfi/Jarkom-Modul-5-B08-2023/assets/86884506/e553caa1-af9b-4e86-b26f-70cae46fa30e">

dapat dilihat, pada server sein, telah ditambahkan rules tentang log dengan prefix "paket didrop:"
