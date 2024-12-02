# Jarkom-Modul-5-IT13-2024

## Anggota Kelompok IT 13

| Nama Lengkap          | NRP        |
| --------------------- | ---------- |
| Muhammad Dzaky Ahnaf  | 5027231039 |
| Muhammad Nafi Firdaus | 5027231045 |

## Misi 1 
## Topologi

![image](https://github.com/user-attachments/assets/64ae068b-ce3b-4d44-9890-e42f7d4b2056)

## Definisi
### VLSM 
VLSM (Variable Length Subnet Mask) adalah metode subnetting dalam jaringan komputer yang memungkinkan penggunaan subnet mask dengan panjang yang berbeda-beda untuk setiap subnet dalam suatu jaringan IP. VLSM dikenal sebagai metode subnetting yang efisien karena memaksimalkan alokasi alamat IP berdasarkan kebutuhan jumlah host dalam tiap subnet.

## Tabel Routing 
| Nama Subnet          | Rute       | Jumlah IP       | Netmask      | 
| -- | ---------- | ---------- | ---------- |
| A1  | NewEridu -> LuminaSquare | 2 | /30 | 
| A2 | NewEridu -> LuminaSquare -> PubSec -> Policeboo -> PubSec -> Jane | 231 | /24 | 
| A3  |NewEridu -> LuminaSquare -> Ofc.Mewmew -> HIA -> Ofc.Mewmew -> BalletTwins | 3 | /29 | 
| A4 | NewEridu -> LuminaSquare -> Ofc.Mewmew -> BalletTwins -> Victoria -> Lycaon -> Victoria -> Ellen | 121 | /25 | 
| A5  | NewEridu -> SixStreet | 2 | /30 | 
| A6 | NewEridu -> SixStreet -> RandomPlay -> HDD -> RandomPlay -> Fairy | 3 | /29 | 
| A7  | NewEridu -> SixStreet -> Metro -> ScootOutpost -> Metro -> OuterRing | 3 | /29 | 
| A8 | NewEridu -> SixStreet -> Metro -> OuterRing -> SoC -> Caesar -> SoC -> Burnice | 56 | /26 | 
| A9  |NewEridu -> SixStreet -> Metro -> ScootOutpost -> HollowZero | 2 | /30 | 
| Total |  | 423 | /23 | 

## Pembagian IP 
| Subnet | Network ID        | Netmask           | Broadcast      | Range IP                       |
|--------|-------------------|-------------------|----------------|--------------------------------|
| A1     | 10.70.1.216	   | 255.255.255.252  | 10.70.1.219    | 10.70.1.217 - 10.70.1.218     |
| A2     | 10.70.0.0 | 255.255.255.0   | 10.70.0.255	    | 10.70.0.1 - 10.70.0.254     |
| A3     | 10.70.1.192     | 255.255.255.248     | 10.70.1.199   | 10.70.1.193 - 10.70.1.198      |
| A4     | 10.70.1.0   | 255.255.255.128	   | 10.70.1.127    | 10.70.1.1 - 10.70.1.126     |
| A5     | 10.70.1.220	  |255.255.255.252   | 10.70.1.223  | 10.70.1.221 - 10.70.1.222   |
| A6     | 10.70.1.200  | 255.255.255.248   | 10.70.1.207    | 10.70.1.201 - 10.70.1.206     |
| A7     | 10.70.1.208  | 255.255.255.248     | 10.70.1.215   | 10.70.1.209 - 10.70.1.214     |
| A8     | 10.70.1.128	   | 255.255.255.192   | 10.70.1.191    | 10.70.1.129 - 10.70.1.190     |
| A9     | 10.70.1.224	   | 255.255.255.252   | 10.70.1.227   | 10.70.1.225 - 10.70.1.226    |

## Subnetting 
### NewEridu (Router) = A1 & A5 
```
#NAT
auto eth0
iface eth0 inet dhcp
#A1
auto eth1
iface eth1 inet static
	address 10.70.1.217
	netmask 255.255.255.252
#A5
auto eth2
iface eth2 inet static
	address 10.70.1.221
	netmask 255.255.255.252
```
### LuminaSquare (Router) = A1, A2, A3
```
#A1
auto eth0
iface eth0 inet static
	address 10.70.1.218
	netmask 255.255.255.252
	gateway 10.70.1.217
#A2
auto eth1
iface eth1 inet static
	address 10.70.0.1
	netmask 255.255.255.0
#A3
auto eth2
iface eth2 inet static
	address 10.70.1.193
	netmask 255.255.255.248
```
### Jane (Client) = A2, Host berjumlah 200
```
auto eth0
iface eth0 inet dhcp
```
### PoliceBoo (Client) = A2, Host berjumlah 30
```
auto eth0
iface eth0 inet dhcp
```
### Hia (Webserver) = A3 
```
#A3
auto eth0
iface eth0 inet static
	address 10.70.1.195
	netmask 255.255.255.248
  	gateway 10.70.1.193
```
### BalletTwins (Router) = A3 & A4 
```
#A3
auto eth0
iface eth0 inet static
	address 10.70.1.194
	netmask 255.255.255.248
  	gateway 10.70.1.193
#A4
auto eth1
iface eth1 inet static
  	address 10.70.1.1
	netmask 255.255.255.128
```
### Ellen (Client) = A4, Berjumlah 100 host 
```
auto eth0
iface eth0 inet dhcp
```
### Lycaon (Client) = A4, Berjumlah 20 host
```
auto eth0
iface eth0 inet dhcp
```
### SixStreet (Router) = A5,A6,A7 
```
#A5
auto eth0
iface eth0 inet static
	address 10.70.1.222
	netmask 255.255.255.252
	gateway 10.70.1.221
#A6
auto eth1
iface eth1 inet static
	address 10.70.1.201
	netmask 255.255.255.248
#A7
auto eth2
iface eth2 inet static
	address 10.70.1.209
	netmask 255.255.255.248
```
### Fairy (DHCP) = A6 
```
#A6
auto eth0
iface eth0 inet static
	address 10.70.1.202
	netmask 255.255.255.248
	gateway 10.70.1.201
```
### HDD (DNS) = A6 
```
#A6
auto eth0
iface eth0 inet static
	address 10.70.1.203
	netmask 255.255.255.248
	gateway 10.70.1.201
```
### OuterRing (Router) = A7 & A8 
```
#A7
auto eth0
iface eth0 inet static
	address 10.70.1.210
	netmask 255.255.255.248
	gateway 10.70.1.209
#A8
auto eth1
iface eth1 inet static
	address 10.70.1.129
	netmask 255.255.255.192
```
### Caesar (Client) = A8, 50 Host 
```
auto eth0
iface eth0 inet dhcp
```
### Burnice (Client) = A8, 5 Host 
```
auto eth0
iface eth0 inet dhcp
```
### ScootOutpost (Router) = A7 & A9 
```
#A7
auto eth0
iface eth0 inet static
	address 10.70.1.211
	netmask 255.255.255.248
	gateway 10.70.1.209
#A9
auto eth1
iface eth1 inet static
	address 10.70.1.225
	netmask 255.255.255.252
```
### HollowZero (Webserver) = A9 
```
#A9
auto eth0
iface eth0 inet static
	address 10.70.1.226
	netmask 255.255.255.252
	gateway 10.70.1.225
```
## Routing 
### NewEridu (Router) = Untuk selain A1 dan A5 
```
# (A2-A4)
post-up route add -net 10.70.0.0 netmask 255.255.255.0 gw 10.70.1.218
post-up route add -net 10.70.1.192 netmask 255.255.255.248 gw 10.70.1.218
post-up route add -net 10.70.1.0 netmask 255.255.255.128 gw 10.70.1.218
# (A6-A9)
post-up route add -net 10.70.1.200 netmask 255.255.255.248 gw 10.70.1.222
post-up route add -net 10.70.1.208 netmask 255.255.255.248 gw 10.70.1.222
post-up route add -net 10.70.1.128 netmask 255.255.255.192 gw 10.70.1.222
post-up route add -net 10.70.1.224 netmask 255.255.255.252 gw 10.70.1.222
```
### LuminaSquare (Router) = Untuk selain A1, A2, A3, A5 hingga A9 
```
# Kembali
post-up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.70.1.217
# A4
post-up route add -net 10.70.1.0 netmask 255.255.255.128 gw 10.70.1.194
```
### BalletTwins (Router) = Untuk Selain A3, A4, A5 hingga A9
```
# Kembali (A1 & A2)
post-up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.70.1.192
```
### SixStreet (Router) = Selain A1 hingga A4, A5, A6, A7
```
# Kembali
post-up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.70.1.221
# A8 dan A9
post-up route add -net 10.70.1.128 netmask 255.255.255.192 gw 10.70.1.210
post-up route add -net 10.70.1.224 netmask 255.255.255.252 gw 10.70.1.211
```
### OuterRing (Router) = Selain A1 hingga A4, A7, A8
```
# Kembali 
post-up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.70.1.209
# A9
post-up route add -net 10.70.1.224 netmask 255.255.255.252 gw 10.70.1.211
```
### ScootOutpost (Router) = Selain A1 hingga A4, A7, A9
```
# Pulang
post-up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.70.1.209
# A8
post-up route add -net 10.70.1.128 netmask 255.255.255.192 gw 10.70.1.210
```
## Konfigurasi 
### DHCP Server = dhcpserver.sh 
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update && apt-get install isc-dhcp-server -y

echo '
INTERFACESv4="eth0"
INTERFACESv6=""
' > /etc/default/isc-dhcp-server

echo '
# Jane & Policeboo (A2)
subnet 10.70.0.0 netmask 255.255.255.0 {
  range 10.70.0.2 10.70.0.254;
  option routers 10.70.0.1;
  option broadcast-address 10.70.0.255;
  option domain-name-servers 10.70.1.203;
}
# Ellen & Lycaon (A4)
subnet 10.70.1.0 netmask 255.255.255.128 {
  range 10.70.1.2 10.70.1.126;
  option routers 10.70.1.1;
  option broadcast-address 10.70.1.127;
  option domain-name-servers 10.70.1.203;
}
# Caesar & Burnice (A8)
subnet 10.70.1.128 netmask 255.255.255.192 {
  range 10.70.1.130 10.70.1.190;
  option routers 10.70.1.129;
  option broadcast-address 10.70.1.191;
  option domain-name-servers 10.70.1.203;
}
# DHCP server
subnet 10.70.1.200 netmask 255.255.255.248 {}
' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```
### DHCP Relay = dhcprelay.sh 
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update && apt-get install isc-dhcp-relay -y

# IP Fairy: 10.70.1.202
echo '
SERVERS="10.70.1.202"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo '
net.ipv4.ip_forward=1
' > /etc/sysctl.conf

service isc-dhcp-relay restart
```
### DNS Server = dnsserver.sh 
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update && apt-get install bind9 -y

echo 'options {
    directory "/var/cache/bind";

    forwarders {
        192.168.122.1;
    };

    // dnssec-validation auto;

    allow-query { any; };
    auth-nxdomain no;    # conform to RFC1035
    listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

service bind9 restart
```
### Web Server = webserver.sh 
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update && apt-get install apache2 -y

echo "Welcome to $(hostname)" > /var/www/html/index.html

service apache2 restart
```
### Client (Install Dependensi) 
```
post-up apt-get update && apt-get install lynx netcat -y
```

## Misi 2 
### Nomor 1
iptables.sh pada NewEridu 
```
ETH0_IP=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $ETH0_IP
```
### Nomor 2 
iptables.sh pada fairy 
```
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP # block pings TO fairy
iptables -A OUTPUT -p icmp --icmp-type echo-request -j ACCEPT # allow pings FROM fairy
```
untuk mengembalikan seperti semula 
```
iptables -D INPUT -p icmp --icmp-type echo-request -j DROP
iptables -D OUTPUT -p icmp --icmp-type echo-request -j ACCEPT
```
### Nomor 3 
iptables.sh pada HDD 
```
iptables -A INPUT -s 10.74.1.202 -j ACCEPT # accept from fairy
iptables -A INPUT -j REJECT # block all
```
Untuk melakukan pengecekan pada fairy bisa dengan `nc 10.74.1.203 1234` dan untuk pada HDD bisa dengan `nc -l -p 1234`
### Nomor 4 
iptables.sh pada HollowZero
```
iptables -A INPUT -p tcp -s <IP_Burnice> --dport 80 -m time --timestart 00:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -p tcp -s <IP_Caesar> --dport 80 -m time --timestart 00:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -p tcp -s <IP_Jane> --dport 80 -m time --timestart 00:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -p tcp -s <IP_Policeboo> --dport 80 -m time --timestart 00:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -j REJECT
```
- IP Client merupakan IP Dinamis karena meminta pada DHCP sehingga diatas tidak dicantumkan
- Untuk melakukan Pengecekan bisa dengan `curl http://10.74.1.226`

