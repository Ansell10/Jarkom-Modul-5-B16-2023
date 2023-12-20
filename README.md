# Jarkom-Modul-5-B16-2023
Praktikum Jaringan Komputer Modul 5 Tahun 2023

# Kelompok B16
| Nama | NRP |Github |
|---------------------------|------------|--------|
|Ahmad Fauzan A | 5025211091 | https://github.com/fazghfr |
|Syomeron Ansell W | 5025211250 | https://github.com/Ansell10 |

## Konfig
### Aura
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.186.14.145
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.186.14.149
	netmask 255.255.255.252
```

### Heiter
```
auto eth0
iface eth0 inet static
	address 192.186.14.150
	netmask 255.255.255.252
	gateway 192.186.14.149

auto eth1
iface eth1 inet static
	address 192.186.8.1
	netmask 255.255.252.0

auto eth2
iface eth2 inet static
	address 192.186.0.1
	netmask 255.255.248.0
```

### Frieren
```
auto eth0
iface eth0 inet static
	address 192.186.14.146
	netmask 255.255.255.252
	gateway 192.186.14.145

auto eth1
iface eth1 inet static
	address 192.186.14.137
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.186.14.141
	netmask 255.255.255.252
```

### Himmel
```
auto eth0
iface eth0 inet static
	address 192.186.14.138
	netmask 255.255.255.252
	gateway 192.186.14.137

auto eth1
iface eth1 inet static
	address 192.186.14.1
	netmask 255.255.255.128

auto eth2
iface eth2 inet static
	address 192.186.12.1
	netmask 255.255.254.0
```

### Fern
```
auto eth0
iface eth0 inet static
	address 192.186.14.3
	netmask 255.255.255.128
	gateway 192.186.14.1

auto eth1
iface eth1 inet static
	address 192.186.14.133
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.186.14.129
	netmask 255.255.255.252
```

### Richter (DNS Server)
```
auto eth0
iface eth0 inet static
	address 192.186.14.134
	netmask 255.255.255.252
	gateway 192.186.14.133
```

### Revolte (DHCP Server)
```
auto eth0
iface eth0 inet static
	address 192.186.14.130
	netmask 255.255.255.252
	gateway 192.186.14.129
```

### Sein (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.186.8.2
	netmask 255.255.255.0
	gateway 192.186.8.1
```

### Stark (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.186.14.142
	netmask 255.255.255.252
	gateway 192.186.14.141
```

### SchwerMountain (64 Host)
```
auto eth0
iface eth0 inet dhcp
```

### LaubHills (255 Host)
```
auto eth0
iface eth0 inet dhcp
```

### TurkRegion (1022 Host)
```
auto eth0
iface eth0 inet dhcp
```

### GrobeForest (512 Host)
```
auto eth0
iface eth0 inet dhcp
```

## Routing
### Aura
```
route add -net 192.186.0.0 netmask 255.255.248.0 gw 192.186.14.150
route add -net 192.186.8.0 netmask 255.255.252.0 gw 192.186.14.150
route add -net 192.186.14.140 netmask 255.255.255.252 gw 192.186.14.146
route add -net 192.186.14.136 netmask 255.255.255.252 gw 192.186.14.146
route add -net 192.186.12.0 netmask 255.255.254.0 gw 192.186.14.146
route add -net 192.186.14.0 netmask 255.255.255.128 gw 192.186.14.146
route add -net 192.186.14.132 netmask 255.255.255.252 gw 192.186.14.146
route add -net 192.186.14.128 netmask 255.255.255.252 gw 192.186.14.146
```

### Heiter
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.186.14.149
```

### Frieren
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.186.14.145
route add -net 192.186.12.0 netmask 255.255.254.0 gw 192.186.14.138
route add -net 192.186.14.0 netmask 255.255.255.128 gw 192.186.14.138
route add -net 192.186.14.132 netmask 255.255.255.252 gw 192.186.14.138
route add -net 192.186.14.128 netmask 255.255.255.252 gw 192.186.14.138
```

### Himmel
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.186.14.137 
route add -net 192.186.14.132 netmask 255.255.255.252 gw 192.186.14.3
route add -net 192.186.14.128 netmask 255.255.255.252 gw 192.186.14.3
```

### Fern
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.186.14.1
```

## DHCP Server
```
echo nameserver 192.168.122.1 > /etc/resolv.conf

apt-get update
apt-get install isc-dhcp-server -y
dhcpd --version

service isc-dhcp-server start

echo '
INTERFACES="eth0"
' > /etc/default/isc-dhcp-server

echo '
option domain-name "example.org";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-style none;

subnet 192.186.14.128 netmask 255.255.255.252 {
    option routers 192.186.14.129;
}

subnet 192.186.14.132 netmask 255.255.255.252 {
}

subnet 192.186.14.136 netmask 255.255.255.252 {
    option routers 192.186.14.136;
}

subnet 192.186.14.140 netmask 255.255.255.252 {
}

subnet 192.186.14.144 netmask 255.255.255.252 {
    option routers 192.186.14.145;
}

subnet 192.186.14.148 netmask 255.255.255.252 {
    option routers 192.186.14.150;
}

subnet 192.186.12.0 netmask 255.255.254.0 {
    range 192.186.12.2 192.186.13.1;
    option routers 192.186.12.1;
    option broadcast-address 192.186.13.255;
    option domain-name-servers 192.186.14.134;
    default-lease-time 720;
    max-lease-time 5760;
}

subnet 192.186.14.0 netmask 255.255.255.128 {
    range 192.186.14.4 192.186.14.67;
    option routers 192.186.14.1;
    option broadcast-address 192.186.14.127;
    option domain-name-servers 192.186.14.134;
    default-lease-time 720;
    max-lease-time 5760;
}

subnet 192.186.0.0 netmask 255.255.248.0 {
    range 192.186.0.2 192.186.4.4;
    option routers 192.186.0.1;
    option broadcast-address 192.186.7.255;
    option domain-name-servers 192.186.14.134;
    default-lease-time 720;
    max-lease-time 5760;
}

subnet 192.186.8.0 netmask 255.255.252.0 {
    range 192.186.8.3 192.186.10.5;
    option routers 192.186.8.1;
    option broadcast-address 192.186.11.255;
    option domain-name-servers 192.186.14.134;
    default-lease-time 720;
    max-lease-time 5760;
}
' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

### Nomor 5
> Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

Untuk menjawab ini, perlu dilakukan konfigurasi firewall pada kedua webserver Sein dan Stark
```
iptables -A INPUT -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT

iptables -A INPUT -j REJECT
```

Hasil testing menggunakan nc dari client ke salah satu webserver :

![image](https://github.com/Ansell10/Jarkom-Modul-5-B16-2023/assets/96367502/55bf494d-79d6-43ea-bd82-47c4fdb21875)

![image](https://github.com/Ansell10/Jarkom-Modul-5-B16-2023/assets/96367502/5879db3b-4f94-4f3b-ae91-f15d801b5137)

Disimpulkan bahwa ketika set date menjadi diluar jam kerja, maka koneksi akan ditolak. Jika masuk pada interval jam tersebut, maka koneksi diterima

### Nomor 6
> Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

Untuk penyelesaiannya, dapat melengkapi rules yang sudah ada, dengan menambahkan rules tambahan tersebut menjadi prioritas. Sehingga konfig akan menjadi :
```
# Batasi akses pada Senin - Kamis dari pukul 12:00 hingga 13:00
iptables -A INPUT -m time --timestart 12:00 --timestop 13:00 --weekdays Mon,Tue,Wed,Thu -j REJECT

# Batasi akses pada Jumat dari pukul 11:00 hingga 13:00
iptables -A INPUT -m time --timestart 11:00 --timestop 13:00 --weekdays Fri -j REJECT

# Izinkan akses pada Senin - Jumat dari pukul 08:00 hingga 16:00
iptables -A INPUT -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT

# Tolak akses pada waktu lainnya
iptables -A INPUT -j REJECT
```

Hasil : 

![image](https://github.com/Ansell10/Jarkom-Modul-5-B16-2023/assets/96367502/57fb6317-3a91-44dc-b7c6-c1eaac08dec9)



### Nomor 7
> Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

Untuk nomor 7 kelompok kami belum bisa menyelesaikannya. Namun secara umum, untuk permasalahan ini dapat diselesaikan menggunakan load balancing dari apache2 ataupun webserver untuk mengalihkan traffic secara bergantian (round robin). Kemudian implementasikan pula rules pada firewall untuk preroutingnya.


### Nomor 8
> Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

Untuk menyelesaikannya, berikan rules firewall berikut : 

[Dengan informasi bahwa subnet dimana revolte berada adalah 192.186.14.128/30]
```
# reject subnet 192.186.14.128
iptables -A INPUT -p tcp -s 192.186.14.128/30 -m time --datestart 2023-12-10 --datestop 2024-02-15 -j DROP

# Batasi akses pada Senin - Kamis dari pukul 12:00 hingga 13:00
iptables -A INPUT -m time --timestart 12:00 --timestop 13:00 --weekdays Mon,Tue,Wed,Thu -j REJECT

# Batasi akses pada Jumat dari pukul 11:00 hingga 13:00
iptables -A INPUT -m time --timestart 11:00 --timestop 13:00 --weekdays Fri -j REJECT

# Izinkan akses pada Senin - Jumat dari pukul 08:00 hingga 16:00
iptables -A INPUT -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT

# Tolak akses pada waktu lainnya
iptables -A INPUT -j REJECT
```

Hasil : 

![image](https://github.com/Ansell10/Jarkom-Modul-5-B16-2023/assets/96367502/ca5fc5a1-e521-4d12-964a-5d016bf94505)

![image](https://github.com/Ansell10/Jarkom-Modul-5-B16-2023/assets/96367502/d5f56807-ea9e-4fea-847f-b35488d13697)


![image](https://github.com/Ansell10/Jarkom-Modul-5-B16-2023/assets/96367502/86d896d4-499c-4d4c-b7b4-3a9a1e40c0a4)


![image](https://github.com/Ansell10/Jarkom-Modul-5-B16-2023/assets/96367502/ae9131c9-4666-4f45-9190-61912000e57e)


### Nomor 9
> Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir  alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit.

```
# Membuat chain khusus untuk menangani port scanning
iptables -N PORTSCAN

# Aturan drop jika terdapat lebih dari 20 scan port dalam 10 menit
iptables -A PORTSCAN -m recent --name portscan --update --seconds 600 --hitcount 20 -j DROP

# Aturan untuk mengaktifkan tracking pada alamat IP yang melakukan scanning port
iptables -A PORTSCAN -m recent --name portscan --set -j ACCEPT

# Mengizinkan paket yang tidak terkait dengan port scanning
iptables -A PORTSCAN -j ACCEPT

# Mengintegrasikan chain PORTSCAN ke dalam chain INPUT
iptables -I INPUT -j PORTSCAN
```

hasil : 

![image](https://github.com/Ansell10/Jarkom-Modul-5-B16-2023/assets/96367502/53b5786f-431b-4b84-8bdd-028dfc7c082e)

Dari hasil di atas, terlihat bahwa laubhills melakukan ping ke ip sein sebanyak 25 paket. Namun hanya 20 yang berhasil dan sisanya loss. Ini dikarenakan 20 paket tersebut dikirim pada kurun waktu 10 menit pertama, sehingga server mendeteksi adanya spam (sesuai definisi pada rules firewall yang dibuat). Maka semua paket yang berasal dari host laubhills akan di drop, yang mengakibatkan paket loss.

### Nomor 10
> Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level.

```
# Membuat chain khusus untuk menangani port scanning
iptables -N PORTSCAN

# Aturan untuk log dan drop jika terdapat lebih dari 20 scan port dalam 10 menit
iptables -A PORTSCAN -m recent --name portscan --update --seconds 600 --hitcount 20 -j LOG --log-prefix "PORTSCAN-DROP: " --log-level warning --log-ip-options --log-tcp-options --log-uid
iptables -A PORTSCAN -m recent --name portscan --update --seconds 600 --hitcount 20 -j DROP

# Aturan untuk mengaktifkan tracking pada alamat IP yang melakukan scanning port
iptables -A PORTSCAN -m recent --name portscan --set -j ACCEPT

# Mengizinkan paket yang tidak terkait dengan port scanning
iptables -A PORTSCAN -j ACCEPT

# Mengintegrasikan chain PORTSCAN ke dalam chain INPUT
iptables -I INPUT -j PORTSCAN
```

Hasil : 
![image](https://github.com/Ansell10/Jarkom-Modul-5-B16-2023/assets/96367502/8ece7527-d9dc-4a28-8ff1-b57d261c3146)


Dari hasil, terlihat bahwa rules firewall LOG sudah berjalan, namun kami belum bisa meng-invoke file log yang diperintahkan, walaupun sudah kami konfigurasi pada service syslog pada webserver.
