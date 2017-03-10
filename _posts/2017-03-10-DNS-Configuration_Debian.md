---
layout: post
title:  "DNS Configuration - Debian"
date:   2017-03-10 00:00:00 +0700
categories: debian
comments: false
---

### Instalasi
```
# apt-get install bind9
```

### File yang di konfigurasi
* /etc/bind/named.conf.local
* file forward
* file reverse

### Konfigurasi
- config /etc/bind/named.conf.local
```
# nano /etc/bind/named.conf.local
zone "maribelajar.id" {
        type master;
        file "/etc/bind/db.mari";
};
zone "10.10.10.in-addr.arpa" {
        type master;
        file "/etc/bind/db.10";
};
```
- file forward
```
# cp db.local db.mari
# nano /etc/bind/db.mari
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     maribelajar.id. root.maribelajar.id. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      maribelajar.id.
@       IN      A       10.10.10.150
www     IN      A       10.10.10.150
ftp     IN      A       10.10.10.150
mail    IN      A       10.10.10.150
```
- file reverse
```
# cp db.127 db.10
# nano /etc/bind/db.10
;
; BIND reverse data file for local loopback interface
;
$TTL    604800
@       IN      SOA     maribelajar.id. root.maribelajar.id. (
                              1         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      maribelajar.id.
150     IN      PTR     maribelajar.id.
```

### Kemudian Restart
```
# Service bind9 restart
```

# THE END
