# cilog
Aplikasi PHP untuk membantu membuka log situs http apa yang dibuka oleh client mikrotik router yang ada di database linux Ubuntu.

Demo : Video demo : https://drive.google.com/.../1RlYc2wNPggJGAwPbTeulHC.../view

Konfigurasi di Mikrotik dan Linux Ubuntu
----------------------------------------

Dikondisikan sebelumnya sudah membuat NAT di Mikrotik. 

Di Winbox

IP -> Firewall -> NAT -> +

General
-------
Chain: dstnat

Protocol: 6(TCP)

Dst. Port: 80

Action
------

Action: redirect

To Ports: 8080

OK


Setelah di atas selesai maka aktifkan proxy
-------------------------------------------

IP -> Web Proxy

General
-------
Enabled dicentang 

OK

Mengaktifkan LOG agar bisa dikirimkan ke linux ubuntu
-----------------------------------------------------


Log Action
---------- 
System -> Logging -> Actions -> +

Name: Action1

Type: remote

Remote Address: ip addresss linux ubuntu (Posisi server berada di dalam satu jaringan dengan client)

OK

Log Rule
--------

System -> Logging -> Rules -> +

Rules
----- 

Topics: Web-proxy (arah panah ke bawah di klik) lalu !Debug
        
Prefix dikosongkan

Action: Action1

OK

Khusus Hotspot jika client ip address-nya ingin dibuat static
-------------------------------------------------------------

Dikondisikan sudah dibuat hotspot beserta user-nya, maka ikuti langkah di bawah ini.

IP -> Hotspot -> Users

Pilih user yang akan dibuat static ip-nya agar bisa mudah diketahui siapa pengguna suatu IP di log.

Hotspot User
------------

General
------- 

Address: Ip address yang ingin digunakan saat login

OK

Keterangan : Saat user tersambung nanti akan terdeteksi ip dari bawaan DHCP Server, tapi saat client browsing nanti IP static yang diset itu yang tercatat.

Installasi dan konfigurasi untuk mendukung disimpannya log pada database mysql
------------------------------------------------------------------------------


Ubuntu 16.04.4 LTS
------------------

Installasi :

apt-get install apache2

apt-get install php

apt-get install mysql-server

apt-get install phpmyadmin

apt-get install rsyslog

apt-get install rsyslog-mysql

nano /etc/rsyslog.conf

Hilangkan tanda # pada module(load="imudp")

Hilangkan tanda # pada input(type="imudp" port="514")

Hilangkan tanda # pada modul(load="imtcp")

Hilangkan tanda # pada input(type-"imtcp" port="514")

Tambahkan agar masuk di /var/log/mikrotik.log: 

:fromhost-ip,isequal,"ipgatewaymikrotik" /var/log/mikrotik.log

Memasukkan cilog ke web server
------------------------------

cd /var/www/html

git clone https://github.com/kurniawandata/cilog.git

cd /var/www/html/cilog

nano mikrolog.php

Ganti username dan password database, sesuaikan dengan username dan password database yang anda gunakan lalu simpan.

Mengakses Cilog
---------------

Langsung buka alamat http://(ipaddressweb)/cilog


LICENSI
------- 

GNU General Public License 


Program cilog dan tutorial ini dibuat oleh :
--------------------------------------------

Kurniawan. trainingxcode@gmail.com. 

xcode.or.id


Donasi :
--------
Jika ingin donasi untuk Kurniawan

![alt text](http://xcodeserver.my.id/gofood.png)

![alt text](http://xcodeserver.my.id/gopay.png)
