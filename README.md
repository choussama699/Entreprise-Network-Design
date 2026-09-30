# Entreprise-Network-Design

A multi-site enterprise network built in Cisco Packet Tracer. It combines VLANs, inter-VLAN routing, static routing, EtherChannel, and a central server providing DHCP, Email, FTP, DNS, and HTTP/HTTPS services.


Features
Three departments (Admin, IT, Users) segmented into separate VLANs on each site
Inter-VLAN routing (router-on-a-stick) on R1 and R2
Static routing across R1, R2 and R3
EtherChannel between Sw1 and Sw2 for bandwidth and redundancy
Centralized server in its own subnet behind R3
DHCP relay so clients on every VLAN get addresses from the central server
Network Design
Site	Switch	Router	Networks
Left	Sw1	R1	192.168.10.0/24, 192.168.20.0/24, 192.168.30.0/24
Right	Sw2	R2	192.168.110.0/24, 192.168.120.0/24, 192.168.130.0/24
Core / Server	-	R3	10.0.33.0/30 (Server0)


VLANs
Department	Site 1 Subnet	Site 2 Subnet	Host (Site 1 / Site 2)
Admin	192.168.10.0/24	192.168.110.0/24	PC1 / PC4
IT	192.168.20.0/24	192.168.120.0/24	PC2 / PC5
Users	192.168.30.0/24	192.168.130.0/24	PC3 / PC6
Point-to-Point Links
Link	Subnet	Side A	Side B
R1 ↔ R3	10.0.13.0/30	R1: 10.0.13.1	R3: 10.0.13.2
R2 ↔ R3	10.0.23.0/30	R2: 10.0.23.1	R3: 10.0.23.2
R3 ↔ Server0	10.0.33.0/30	R3: 10.0.33.1	Server0: 10.0.33.2

Server Services (Server0 - 10.0.33.2)
Service	Purpose
DHCP	Dynamic addressing for all VLANs (via ip helper-address)
Email	SMTP / POP3 mail service
FTP	File transfer
HTTP / HTTPS	Web service


Verification
show vlan brief
show interfaces trunk
show etherchannel summary
show ip route
show ip interface brief

Connectivity tests:

Ping between VLANs on the same site (e.g. PC1 → PC2)
Ping across sites (e.g. PC1 → PC4)
Ping the server (10.0.33.2) from any PC
Confirm each PC gets an IP through DHCP
Access the server from a PC browser (HTTP/HTTPS), FTP client, and email client
EtherChannel link aggregation
DHCP relay and server services (DHCP, Email, FTP, HTTP/HTTPS)
Network troubleshooting with IOS show commands
