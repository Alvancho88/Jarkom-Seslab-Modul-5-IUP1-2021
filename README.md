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

## Soal

### 1.) PC Baratie tidak diizinkan mengakses server Water7

```

```

### 2.) PC Arabasta tidak dapat diakses pada pukul 07.00 - 17.00

```

```

### 3.) Server Water7 tidak diperbolehkan menerima koneksi HTTP 

```
# iptables -A INPUT -p tcp --dport 80 -j DROP
```

### 4.) Semua paket yang menuju PC Baratie akan diarahkan ke PC Mariejois (Forwarding)

```
# iptables -A FORWARD -s 10.151.36.0/24 -j ACCEPT
```


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
