---
layout: post
title:  "RAID Configuration - Debian"
date:   2017-03-09 00:00:00 +0700
categories: debian
comments: true
---

# RAID Configuration

### Instalasi
```
# apt-get install mdadm
```
#### Cek hardisk
```
# fdisk -l
```
#### Config raid
```
# mdadm –create –verbose /dev/md0 –level=5 –raid-device=3 /dev/sdb /dev/sdc /dev/sdd
```
NB. level RAID bisa disesuaikan, jika ingin membuat RAID 5 atau 0, tinggal anda ubah level menjadi 5 atau 0

* Untuk cek proses
```
# cat /proc/mdstat
```
* Agar RAID di kenali oleh sistem gunakan perintah
```
# mdadm –detail –scan –verbose
# mdadm –detail –scan –verbose > /etc/mdadm/mdadm.conf
```
* Sampai tahap ini, RAID sudah selesai dibuat atau di konfigurasi. Selanjutnya adalah memformat dan me-mount RAID agar on pada saat startup
```
# mkfs.ext4 /dev/md0
# mkdir /data
# nano /etc/fstab
/dev/md0	/data	ext4	defaults	0	0
```



## THE END
