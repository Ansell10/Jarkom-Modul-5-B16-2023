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

