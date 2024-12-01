# Jarkom-Modul-5-IT13-2024

## Anggota Kelompok IT 13

| Nama Lengkap          | NRP        |
| --------------------- | ---------- |
| Muhammad Dzaky Ahnaf  | 5027231039 |
| Muhammad Nafi Firdaus | 5027231045 |

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
