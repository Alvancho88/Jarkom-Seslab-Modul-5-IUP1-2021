# Jarkom-Modul-5-IUP1-2021

## Seslab

#### Syntax

##### Syntax tersebut akan men DROP semua paket keluar (OUTPUT) yang menuju ke 10.151.36.5

```
iptables -A OUTPUT -d 10.151.36.5 -j DROP
```

##### Syntax tersebut akan meng ACCEPT semua paket keluar yang melewati yang berasal dari subnet 10.151.36.0/24


```
iptables -A FORWARD -s 10.151.36.0/24 -j ACCEPT
```

##### Arahkan ke jaringan lain

```
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to-destination 10.151.73.98:80
```

##### Mengubah alamat asal

```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```


##### Menyimpan Rules IPTables

```
# sudo /sbin/iptables-save
```

##### Menghapus semua Rules pada IPTables

```
# iptables -F
```

#### Melihat semua Rules pada IPTables

```
# iptables -L
```

## Soal

### 1.) PC Baratie tidak diizinkan mengakses server Water7

```
# iptables -A INPUT -s 10.38.1.1 -j DROP
```

a Ping Baratie ke Water 7

b Ping node lain ke Water 7

### 2.) PC Arabasta tidak dapat diakses pada pukul 07.00 - 17.00

Drop semua koneksi ke
```
# iptables --policy OUTPUT DROP
```

Referensi Waktu
```
iptables -A INPUT -p tcp -m time --timestart 02:00 --timestop 03:00 -j DROP
```

Versi 1
```
iptables -A INPUT -m time --timestart 07:00 --timestop 17:00 -j DROP
```

Cek Date
```
date
```

Ganti Date dan cek bila ping otomatis stop dan lanjut
```
date -s "12:00"
date -s "17:00"
```

Versi 2
```
iptables -A FORWARD -s IPGuanhao -m time --timestart 07:00 --timestop 17:00 -j DROP
```

### 3.) Server Water7 tidak diperbolehkan menerima koneksi HTTP 

```
# iptables -A INPUT -p tcp --dport 80 -j DROP
```

cek commands
```
nmap
```

Di note selain Water 7
```
nmap IPWater7
nmap 10.38.1.30
```

Starting Nmap 7.01 ( https://nmap.org ) at 2021-05-12 17:09 UTC
Nmap scan report for 10.38.1.30
Host is up (0.00028s latency).
Not shown: 999 closed ports
PORT   STATE    SERVICE
80/tcp filtered http

### 4.) Semua paket yang menuju PC Baratie akan diarahkan ke PC Mariejois (Forwarding)

```
iptables -t nat -A PREROUTING -d 10.38.1.2 -j DNAT --to-destination 10.38.1.6
```

tcpdumb di Baratie dan Mariejois
```
tcpdumb
```

Dari Foosha ping ke Baratie dan Mariejois

## VLSM

14 host

10.38.0.1/28

10.38.0.0/29 --- 10.38.0.6/29

10.38.0.0

## Config ETH All

### Foosha
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.38.1.13
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 10.38.1.17
netmask 255.255.255.252
  
auto eth3
iface eth3 inet static
	address 10.38.1.21
	netmask 255.255.255.252
```

### Pucci
```
auto eth0
iface eth0 inet static
	address 10.38.1.14
	netmask 255.255.255.252
  
auto eth1
iface eth1 inet static
	address 10.38.1.1
	netmask 255.255.255.252
  
auto eth2
iface eth2 inet static
  address 10.38.1.5
  netmask 255.255.255.252


auto eth3
iface eth3 inet static
  address 10.38.1.9
  netmask 255.255.255.252
```

### Guanhao
```
auto eth0
iface eth0 inet static
	address 10.38.1.18
	netmask 255.255.255.252
  
auto eth1
iface eth1 inet static
	address 10.38.1.25
	netmask 255.255.255.252
  
auto eth2
iface eth2 inet static
  address 10.38.1.29
  netmask 255.255.255.252


auto eth3
iface eth3 inet static
  address 10.38.1.33
  netmask 255.255.255.252
```

### Baratie
```
auto eth0
iface eth0 inet static
	address 10.38.1.2
	netmask 255.255.255.252
	gateway 10.38.1.1
```

### Mariejois
```
auto eth0
iface eth0 inet static
	address 10.38.1.6
	netmask 255.255.255.252
	gateway 10.38.1.5
```

### Wano
```
auto eth0
iface eth0 inet static
	address 10.38.1.10
	netmask 255.255.255.252
	gateway 10.38.1.9
```

### Enieslobby
```
auto eth0
iface eth0 inet static
	address 10.38.3.2
	netmask 255.255.255.0
	gateway 10.38.3.1
```

### Arabasta
```
auto eth0
iface eth0 inet static
	address 10.38.1.26
	netmask 255.255.255.252
	gateway 10.38.1.25
```

### Water7
```
auto eth0
iface eth0 inet static
	address 10.38.1.30
	netmask 255.255.255.252
	gateway 10.38.1.29
```

### Loguetown
```
auto eth0
iface eth0 inet static
	address 10.38.1.34
	netmask 255.255.255.252
	gateway 10.38.1.33
```

## Routing

### Foosha
```
# !/bin/sh

route add -net 10.38.1.0 netmask 255.255.255.252 gw 10.38.1.14
route add -net 10.38.1.4 netmask 255.255.255.252 gw 10.38.1.14
route add -net 10.38.1.8 netmask 255.255.255.252 gw 10.38.1.14

route add -net 10.38.1.24 netmask 255.255.255.252 gw 10.38.1.18
route add -net 10.38.1.28 netmask 255.255.255.252 gw 10.38.1.18
route add -net 10.38.1.32 netmask 255.255.255.252 gw 10.38.1.18

```

### Guanhao
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.38.1.17
atau
route add -net 0.0.0.0/0  gw 10.38.1.17
```

### Pucci
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.38.1.13
```

## Config normal

### nano ./.bashrc
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.38.0.0/16
/root/config.sh
echo "nameserver 10.38.122.1" > /etc/resolv.conf
```

### Terminal
```
chmod +x config.sh
```

## References

https://www.thegeekstuff.com/2011/06/iptables-rules-examples/

https://opensource.com/article/18/10/iptables-tips-and-tricks

Regulate by Time

Scenario: The backlash from the company's employees over denying access to Facebook access causes the CEO to relent a little (that and his administrative assistant's reminding him that she keeps HIS Facebook page up-to-date). The CEO decides to allow access to Facebook.com only at lunchtime (12PM to 1PM). Assuming the default policy is DROP, use iptables' time features to open up access.

```
iptables –A OUTPUT -p tcp -m multiport --dport http,https -i eth0 -o eth1 -m time --timestart 12:00 --timestart 12:00 –timestop 13:00 –d
31.13.64.0/18  -j ACCEPT
```

This command sets the policy to allow (-j ACCEPT) http and https (-m multiport --dport http,https) between noon (--timestart 12:00) and 13PM (--timestop 13:00) to Facebook.com (–d 31.13.64.0/18).

Regulate by time—Take 2

Scenario: During planned downtime for system maintenance, you need to deny all TCP and UDP traffic between the hours of 2AM and 3AM so maintenance tasks won't be disrupted by incoming traffic. This will take two iptables rules:

```
iptables -A INPUT -p tcp -m time --timestart 02:00 --timestop 03:00 -j DROP
iptables -A INPUT -p udp -m time --timestart 02:00 --timestop 03:00 -j DROP
```

With these rules, TCP and UDP traffic (-p tcp and -p udp ) are denied (-j DROP) between the hours of 2AM (--timestart 02:00) and 3AM (--timestop 03:00) on input (-A INPUT).
