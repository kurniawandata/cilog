# cilog
Program untuk membantu membuka log apa yang dibuka oleh client mikrotik router di database linux.

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

IP -> Web Proxy

General
-------
Enabled dicentang 

OK

System -> Logging -> Actions -> +

Log Action
---------- 

Name: Action1

Type: remote

Remote Address: ip addresss linux ubuntu

OK

System -> Logging -> Rules -> +

Rules
----- 

Topics: Web-proxy (arah panah ke bawah di klik)

        !Debug
        
Prefix dikosongkan

Action: Action1

OK

Ubuntu 16.04.4 LTS
------------------

Installasi :

apt-get install apache2

apt-get install phpmyadmin

apt-get install mysql-server

apt-get install rsyslog

apt-get install rsyslog-mysql

nano /etc/rsyslog.conf

Hilangkan tanda # pada module(load="imudp")

Hilangkan tanda # pada input(type="imudp" port="514")

Hilangkan tanda # pada modul(load="imtcp")

Hilangkan tanda # pada input(type-"imtcp" port="514")

Tambahkan : :fromhost-ip,isequal,"ipgatewaymikrotik" /var/log/mikrotik.log

Kurniawan

Kurniawanajazenfone@gmail.com

xcode.or.id
