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

## Subneting

**Penjelasan**
Untuk melakukan subneting pada praktikum 5 ini kita menggunakan metode VLSM 
Berikut adalah topologi pengelompokan subnet :

(ss)


Setelah kita membuat pengelompokan subnet selanjutnya kita buat tabel pengelompokan subnet : 

(ss)

berikut adalah tree hasil perhitungan menggunaakan metode VLSM 

(ss)

Setelah melakukan perhitungan dan membuat tree maka didapatkan hasil ip yaittu sebagai berikut : 

(ss)

## Routing 
sebelum kita melakukan routing kia melakukan IP configuration dulu di gns3 yang telah kita buat berikut adalah configurasinya : 

Revolte :
``
auto eth0
iface eth0 inet static
address 192.206.0.2
netmask 255.255.255.252
gateway 192.206.0.1
``

Ritcher : 

``
auto eth0
iface eth0 inet static
address 192.206.0.6
netmask 255.255.255.252
gateway 192.206.0.5
``

Stark :
``
auto eth0
iface eth0 inet static
address 192.206.0.18
netmask 255.255.255.252
gateway 192.206.0.17
``

Sein : 
``
auto eth0
iface eth0 inet static
address 192.206.4.2
netmask 255.255.252.0
gateway 192.206.4.1
``

TurkRegion : 
``
auto eth0
iface eth0 inet dhcp
address 192.206.8.2
netmask 255.255.248.0
gateway 192.206.8.1
``

GrobeForest : 
``
auto eth0
iface eth0 inet dhcp
address 192.206.4.3
netmask 255.255.252.0
gateway 192.206.4.1
``

SchwerMotain : 

``
auto eth0
iface eth0 inet dhcp
address 192.206.0.131
netmask 255.255.255.128
gateway 192.206.0.129
``

LaubHills: 
``
auto eth0
iface eth0 inet dhcp
address 192.206.2.2
netmask 255.255.254.0
gateway 192.206.2.1
``

Aura : 
``
auto lo
iface lo inet loopback
auto eth0
iface eth0 inet dhcp
auto eth1
iface eth1 inet static
address 192.206.0.25
netmask 255.255.255.252
auto eth2
iface eth2 inet static
address 192.206.0.21
netmask 255.255.255.252
``

Heiter : 
``
auto lo
iface lo inet loopback
auto eth0
iface eth0 inet static
address 192.206.0.26
netmask 255.255.255.252
gateway 192.206.0.25
auto eth1
iface eth1 inet static
address 192.206.8.1
netmask 255.255.248.0
auto eth2
iface eth2 inet static
address 192.206.4.1
netmask 255.255.252.0
``

Frieren 
``
auto lo
iface lo inet loopback
auto eth0
iface eth0 inet static
address 192.206.0.22
netmask 255.255.255.252
gateway 192.206.0.21
auto eth1
iface eth1 inet static
address 192.206.0.17
netmask 255.255.255.252
auto eth2
iface eth2 inet static
address 192.206.0.13
netmask 255.255.255.252
``

Himmel : 
``
auto lo
iface lo inet loopback
auto eth0
iface eth0 inet static
address 192.206.0.14
netmask 255.255.255.252
gateway 192.206.0.13
auto eth1
iface eth1 inet static
address 192.206.2.1
netmask 255.255.254.0
auto eth2
iface eth2 inet static
address 192.206.0.129
netmask 255.255.255.128
``

Fern : 
``
auto lo
iface lo inet loopback
auto eth2
iface eth2 inet static
address 192.206.0.1
netmask 255.255.255.252
gateway 192.206.0.129
auto eth1
iface eth1 inet static
address 192.206.0.5
netmask 255.255.255.252
auto eth0
iface eth0 inet static
address 192.206.0.130
netmask 255.255.255.128
``

Setelah menentukan Ip kita lakukan touting di setiap Router yang ada, berikut adalah code untuk setiap routernya :

Fern : 
``
echo nameserver 192.168.122.1 > /etc/resolv.conf
route add -net 192.206.0.0 netmask 255.255.255.252 gw 192.206.0.1
route add -net 192.206.0.4 netmask 255.255.255.252 gw 192.206.0.5
``

Himmel : 
`` 
echo nameserver 192.168.122.1 > /etc/resolv.conf
route add -net 192.206.2.0 netmask 255.255.254.0 gw 192.206.2.1
route add -net 192.206.0.128 netmask 255.255.255.128 gw 192.206.0.129
route add -net 192.206.0.0 netmask 255.255.255.252 gw 192.206.0.130
route add -net 192.206.0.4 netmask 255.255.255.252 gw 192.206.0.130
``

Frieren : 
``
echo nameserver 192.168.122.1 > /etc/resolv.conf
route add -net 192.206.0.16 netmask 255.255.255.252 gw 192.206.0.17
route add -net 192.206.0.12netmask 255.255.255.252 gw 192.206.0.14
route add -net 192.206.2.0 netmask 255.255.254.0 gw 192.206.0.14
route add -net 192.206.0.128 netmask 255.255.255.128 gw 192.206.0.14
route add -net 192.206.0.0 netmask 255.255.255.252 gw 192.206.0.14
route add -net 192.206.0.4 netmask 255.255.255.252 gw 192.206.0.14
``

Heiter 
``
echo nameserver 192.168.122.1 > /etc/resolv.conf
route add -net 192.206.4.0  netmask 255.255.252.0 gw 192.206.4.1
route add -net 192.206.8.0  netmask 255.255.248.0  gw 192.206.8.1
``

Aura 
``
# Heiter
route add -net 192.206.4.0  netmask 255.255.252.0 gw 192.206.0.26
route add -net 192.206.8.0  netmask 255.255.248.0  gw 192.206.0.26
route add -net 192.206.0.24  netmask 255.255.255.252 gw 192.206.0.26
# Frieren
route add -net 192.206.0.20 netmask 255.255.255.252 gw 192.206.0.22
route add -net 192.206.0.16 netmask 255.255.255.252 gw 192.206.0.22
route add -net 192.206.0.12netmask 255.255.255.252 gw 192.206.0.22
route add -net 192.206.2.0 netmask 255.255.254.0 gw 192.206.0.22
route add -net 192.206.0.128 netmask 255.255.255.128 gw 192.206.0.22
route add -net 192.206.0.0 netmask 255.255.255.252 gw 192.206.0.22
``

### Soal 1

**Soal**
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

**Penjelasan**
Untuk membuat konfigurasi Aura menggunakan iptable,tetapi tidak ingin menggunakan MASQUERADE yaitu dengan menggunakan query berikut : 

``
ETH0_IP=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')

iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $ETH0_IP
``

query `ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}`  berfungsi untuk mereturn IP eth0 Aura 

Selanjutnya, untuk menyambungkan ke nat, maka kita masukkan ke NAT Table dengan POSTROUTING chain : `iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $ETH0_IP`

### No 2
**Soal**
Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

**penjelasan**
pertama tama kita install netcat di router `Aura` terlebih dahulu dengan 
``
apt-get update
apt-get install netcat -y
``
Lalu untuk menolak suma koneksi TCP kecuali port 8080 bisa menggunakan query berikut : 

``
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
iptables -A INPUT -p tcp -j DROP
``

lalu untuk menolak semua koneksi di udp bisa menggunakan query berikut : 
``
iptables -A INPUT -p udp -j DROP
``

### No 3
**Soal**

Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

**Penjelasan**

lakukan perintah berikut di Revolte & Richter DHCP server & DNS Server

``
#Allow established and related connections
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
#Limit ICMP connections to 3 per second
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
``
- `--connlimit-above 3` adalah parameter menentukan batas koneksi yang terhubung
- `--connlimit-mask 0` adalah parameter menentukan mask

### No 4
**Soal**
Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

**Penjelasan**
Lakukan perintah berikut di Sein & Stark (Web Server)

``
iptables -A INPUT -p tcp --dport 22 -s 192.182.4.0/22 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
``
