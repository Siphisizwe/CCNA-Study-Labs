LAB 15 - VLSM Subnetting
Network: 192.168.5.0/24
Subnetting order (largest to smallest):
1. LAN2 - 64 hosts
2. LAN1 - 45 hosts
3. LAN3 - 14 hosts
4. LAN4 - 9 hosts
5. P2P  - 2 hosts
LAN2 - 64 hosts
2^7 = 128 addresses (126 usable)
/25 chosen because 2^6 = 64 = only 62 usable, not enough
Network address 192.168.5.0/25
Subnet mask        255.255.255.128
First usable           192.168.5.1/25
Last usable            192.168.5.126/25
Broadcast             192.168.5.127/25
Next subnet starts at  192.168.5.128

Lan 1 -45 hosts
2^6 = 64 addresses (62 usable)
/26 chosen 
Network address 192.168.5.128/26
Subnet mask        255.255.255.192
First usable           192.168.5.129/26
Last usable            192.168.5.190/26
Broadcast             192.168.5.191/26
Next subnet starts at  192.168.5.192
Lan 3 -14 hosts
2^4 = 16 addresses (14 usable)
/28 chosen 
Network address 192.168.5.192/28
Subnet mask        255.255.255.240
First usable           192.168.5.193/28
Last usable            192.168.5.206/28
Broadcast             192.168.5.207/28
Next subnet starts at  192.168.5.208
Lan 4 -9 hosts
2^4 = 16 addresses (14 usable)
/28 chosen 
Network address 192.168.5.208/28
Subnet mask        255.255.255.240
First usable           192.168.5.209/28
Last usable            192.168.5.222/28
Broadcast             192.168.5.223/28
Next subnet starts at  192.168.5.224
P2P
2^2 = 4 addresses (2usable)
/30 chosen 
Network address 192.168.5.224/30
Subnet mask        255.255.255.252
First usable           192.168.5.225/30
Last usable            192.168.5.226/30
Broadcast             192.168.5.227/30



DEVICE CONFIGURATION TABLE
PC1 = 192.168.5.129  GW: 192.168.5.190
PC2 = 192.168.5.1    GW: 192.168.5.126
PC3 = 192.168.5.193  GW: 192.168.5.206
PC4 = 192.168.5.209  GW: 192.168.5.222
R1 G0/0   = 192.168.5.190/26  (LAN1 last usable)
R1 G0/1   = 192.168.5.126/25  (LAN2 last usable)
R1 G0/0/0 = 192.168.5.225/30  (P2P first usable)

R2 G0/0   = 192.168.5.206/28  (LAN3 last usable)
R2 G0/1   = 192.168.5.222/28  (LAN4 last usable)
R2 G0/0/0 = 192.168.5.226/30  (P2P second usable)


STATIC ROUTES
R1: ip route 192.168.5.192 255.255.255.240 192.168.5.226
R1: ip route 192.168.5.208 255.255.255.240 192.168.5.226
R2: ip route 192.168.5.128 255.255.255.192 192.168.5.225
R2: ip route 192.168.5.0 255.255.255.128 192.168.5.225
