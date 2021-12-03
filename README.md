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
# iptables -A INPUT -s 10.151.36.0/24 -j DROP
```

### 2.) PC Arabasta tidak dapat diakses pada pukul 07.00 - 17.00

```
# iptables --policy OUTPUT DROP
```

### 3.) Server Water7 tidak diperbolehkan menerima koneksi HTTP 

```
# iptables -A INPUT -p tcp --dport 80 -j DROP
```

### 4.) Semua paket yang menuju PC Baratie akan diarahkan ke PC Mariejois (Forwarding)

```
# iptables -A FORWARD -s 10.151.36.0/24 -j ACCEPT
```

## Configh All

### Foosha

### Pucci

### Guanhao

### Baratie

### Mariejois

### Wano

### Enieslobby

### Loguetown

### Water7

### Arabasta

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
