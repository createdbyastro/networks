## 5 Topologies : Bus,Mesh,Star,Ring ,extended star. + 1 Hybrid topology intergrating all 5 topologies , configured with IPv4 and IPv6,VLAN segmentation  and one server(HTTP/DNS/DHCP) and basic security. + Configured with PPP ON WAN LINK.

  ## Part 1 
  ## 5 TOPOLOGIES
| Name of topology | IP address| Default gateway|
|---------|----------|-----------|
|star| 192.168.12.0/24| 192.168.12.1|
|Bus|192.168.10.0/24| 192.168.10.1|
|ex_star| 192.168.50.0/24|192.168.50.1|
|mesh|192.168.1.0/24 | 192.168.1.1|
|ring |192.168.20.0/24|192.168.20.1|

 
## Screenshots of Succesfull messaging withing topologies and pings.

## star topology

<img width="804" height="654" alt="image" src="https://github.com/user-attachments/assets/0472dc45-2f9e-405f-b6b9-f72c583f3774" />
<img width="1432" height="745" alt="image" src="https://github.com/user-attachments/assets/1e924809-d0e1-4a2f-b657-80b9bf65366a" />

## ring topology 
<img width="1025" height="679" alt="image" src="https://github.com/user-attachments/assets/9ea040ff-aa63-4a2e-8bbf-16e744f29938" />
<img width="1561" height="717" alt="image" src="https://github.com/user-attachments/assets/65576463-c251-476e-b9c3-07096ade937c" />

## ext_star
<img width="1785" height="896" alt="image" src="https://github.com/user-attachments/assets/e4dc5077-8e04-4532-a6fc-d6f0d15b1d3f" />

## Bus topology
<img width="1745" height="846" alt="image" src="https://github.com/user-attachments/assets/de7e46de-b476-46f8-91d0-1522f988fa8a" />

## mesh topology 
<img width="1680" height="835" alt="image" src="https://github.com/user-attachments/assets/15c5bee8-6ed4-4268-bbe5-e2e564bb5c85" />


## Part 1 : Hybrid topology  intergrating the 5 topologies , configured with IPv4 and IPv6 , VLAN Segmentation , one server(DNS/HTTP/DHCP) And basic security.

## FiGURE : Hybrid topology.
<img width="1697" height="673" alt="image" src="https://github.com/user-attachments/assets/62b16395-5665-4f91-ae9e-3408c803b632" />



| VLAN | IPv4 ADDRESS | IPv4 DEFAULT Gateway | IPv6 ADDRESS |  IPV6 DEFAULT GATEWAY|
|------|--------------|----------------------|--------------|----------------------|
  |VLAN 10| 192.168.10.0/24|192.168.10.1| 2001:10::/64 | 2001:10::1/64|
  |VLAN 20| 192.168.20.0/24 | 192.168.20.1 | 2001:20::/64 |2001:20::1/64|
  |VLAN 30 |192.168.30.0/24 | 102.168.30.1 | 2001:30::/64| 2001:30::1/54|
  |VLAN 40 | 192.168.40.0/24| 192.168.40.1 | 2001:40::/64| 2001:40:1/64|
  |VLAN 50 | 192.168.50.0/24 | 192.168.50.1 | 2001:50::64/64|2001:50::1/64|
  | SERVER | 192.168.30.10| 192.168.30.1|2001:30::10/64 | 2001:30::1/64 |

  ## CONFUGURATION NOTES 

  
  On core switch : 3560 24ps Multilayer switch creeate vlans
  
enable<br>
configure terminal<br>
vlan 10<br>
name RING<br>
vlan 20<br>
name BUS<br>
vlan 30<br>
name central<br>
vlan 40<br>
name MESH<br>
vlan 50<br>
name EXT_STAR<br>
exit<br>

## SCREENSHOT OF VLAN BRIEF : <img width="1154" height="848" alt="image" src="https://github.com/user-attachments/assets/ab463fe5-05d1-49ec-bf76-f7d10425452d" />

## Switchport confuguration 

This trunk port will carry multiple vlan between switches, i configured this between all switch to switch<br>
<br>

interface fa0/port <br>
switchport mode trunk<br>
switchport trunk allowed vlan 10,20,30,40,50 <br>
<br>
## For each switch connected to my core switch in every vlan these are my configurations .
  for switch in vlan 10:<br>
enable<br>
configure terminal<br>
vlan 10<br>
name RING<br>
exit<br>
interface gigabitEthernet0/1<br>
 switchport trunk encapsulation dot1q<br>
 switchport mode trunk<br>
 switchport trunk allowed vlan 10,20,30,40,50<br>
 no shutdown<br>
exit<br>
Then i followed method  for all switches connected to the core switch in every vlan.
  
The Access port will transport a single, this was configured between PC and a switch.
It was also configured between the server and the core switch.<br>
<br>

interface fa0/port<br>
switchport mode access<br>
Switchport access vlan ( vlan the pc and switch are in or server )<br>
exit <br>

## screenshot of trunk port brief from core switch
<img width="1282" height="836" alt="image" src="https://github.com/user-attachments/assets/d4189809-fcdc-4af1-9764-e483cd0f460f" />

## Configuration of the router 
on my router i configured sub interfaces <br>
enable<br>
conf t<br>
int g0/0.10<br>
encapsulation dot1Q 10<br>
ip address 192.168.10.1 255.255.255.0<br>
ipv6 address 2001:10::1/64 <br>
exit<br>

int g0/0.20 <br>
encapsulation dot1Q 20 <br>
ip address 192.168.20.1 255.255.255.0<br>
ipv6 address 2001:20::1/64<br>
exit<br>

int g0/0.30<br>
encapsulation dot1Q 30<br>
ip address 192.168.30.1 255.255.255.0<br>
ipv6 address 2001:30::1/64<br>
exit<br>

int g0/0.40<br>
encapsulation dot1Q 40<br>
ip address 192.168.40.1 255.255.255.0<br>
ipv6 address 2001:40::1/64<br>
exit<br>

int g0/0.50<br>
encapsulation dot1Q 50<br>
ip address 192.168.50.1 255.255.255.0<br>
ipv6 address 2001:50::1/64<br>
exit <br>

Those commands turn one router port into multiple virtual ports, each one belonging to a different department (VLAN), allowing them to send messages and communicate through a single cable.
## screen shot of IP interface brief : <img width="918" height="888" alt="image" src="https://github.com/user-attachments/assets/5008ae86-fe18-484c-b7f8-4d71563b6eeb" />
## For inter vlan communicaton between vlan 10 and 20, i configured the router with helper addresses.<br> 
## configuration notes <br>
interface g0/0.10<br>
 encapsulation dot1Q 10<br>
 ip address 192.168.10.1 255.255.255.0<br>
 ipv6 address 2001:10::1/64<br>
 ip helper-address 192.168.30.2   <-- Server IP<br>

interface g0/0.20<br>
 encapsulation dot1Q 20<br>
 ip address 192.168.20.1 255.255.255.0<br>
 ipv6 address 2001:20::1/64<br>
 ip helper-address 192.168.30.2<br>
 ip helper-address 192.168.30.10 forwards DHCP requests from each VLAN to your server.<br>
 When a pc sends DHCP request, it can not cross vlans or routers. so i used IP -helper addresses to fix this . because  the outer blocks the rquests from pcs to reach other vlans.<br>
                                                                                                                                                                                   
  ## Server setup
  
 ## IPv4 settings <br>
iP Address: 192.168.30.10<br>
Subnet Mask: 255.255.255.0<br>
Default Gateway: 192.168.30.1 <br> 
## IPv6 setrings<br>
IPv6 Address: 2001:30::10/64<br>
Default Gateway: 2001:30::1<br>

## DHCP CONFIGURATION 
|Pool Name|	Default Gateway|	DNS Server|	Start IP|	Subnet Mask|
|--------|-----------------|-----------|---------|-------------|
|VLAN10	|192.168.10.1	|192.168.30.10	|192.168.10.10		|255.255.255.0|
|VLAN20	|192.168.20.1	|192.168.30.10	|192.168.20.10		|255.255.255.0|
|VLAN30	|192.168.30.1	|192.168.30.10	|192.168.30.10		|255.255.255.0|
|VLAN40	|192.168.40.1	|192.168.30.10	|192.168.40.10		|255.255.255.0|
|VLAN50	|192.168.50.1	|192.168.30.10	|192.168.50.10	|	255.255.255.0|

## DNS CONFIGURATION 
|Name| Type |Address|
|----|------|-------|
|www.hybrid.local| A|192.168.30.10|
|central.hybrid.local|A|192.168.30.10|
|server.hybrid.local|A|192.168.30.10|
<br>
what this means An A record maps a domain name → an IP address (IPv4).
So when a PC types a name like www.hybrid.local, the DNS server says:
That name belongs to IP 192.168.30.10.
## screenshot from pc 10 pinging:<br> <br>
<img width="907" height="451" alt="image" src="https://github.com/user-attachments/assets/9984df45-76dc-4ac9-9def-20d0a4c170c6" />

 

## HTTP Configuration
TURNED ON HTTP AND HTTPS ON THE SERVER. <br>
from pc in vlan 10 on the web browser screenshot:<br>
<img width="995" height="699" alt="image" src="https://github.com/user-attachments/assets/537c4aea-82e2-42fb-b7d3-3ab5edf22bba" />

## BASIC SECURITY 

Shutdown all non working ports on core switch<br>
configuration notes for this<br>
<br>
interface range fa0/16 - 24<br>
shutdown<br>
this prevents unwanted devices form connecting into unsued ports.

## PASSWORD INCRYPTION 
enable<br>
configure terminal<br>
service password-encryption<br>
If anyone runs show running-config, they can’t read any passwords in clear text.

## SUCCESFUL MESSAGING WITHING VLANS AND PINGS <br>

## vlan 10<br>
<img width="1030" height="959" alt="image" src="https://github.com/user-attachments/assets/8efaf52f-e9ba-465a-9454-7c626a8b5982" />
<br>
## vlan 20<br>

<img width="956" height="866" alt="image" src="https://github.com/user-attachments/assets/0c093050-e522-4ee0-834b-710932e0c6c0" />
<br>

## vlan 30<br>
<br>
<img width="951" height="830" alt="image" src="https://github.com/user-attachments/assets/8872629e-f404-4e4a-a204-079104d9651a" />
<br>

## vlan 40<br>
<br>
<img width="899" height="980" alt="image" src="https://github.com/user-attachments/assets/ec3a11e8-a967-47ac-8fa4-ac0cb5345d93" />
<br>

## vlan 50<br>
<br>
<img width="915" height="999" alt="image" src="https://github.com/user-attachments/assets/244134be-2c63-4268-9b8f-4c786aed36df" />

## Inter vlan communication between VLAN 10 and VLAN 20 and successfull pings<br>
<br>
<img width="887" height="976" alt="image" src="https://github.com/user-attachments/assets/554584ba-b086-421b-bd1e-f5ba2357a5d0" />

There is vlan segmentation between all topologies within the hybrid except for vlan 10 and 20 where there is inter vlan communication .
<br>

## PART 2 : POInt TO POINT ON WAN LINKS 
<br>
<img width="1358" height="482" alt="image" src="https://github.com/user-attachments/assets/ebe36ef8-84f4-4ad1-a143-476fea8bc280" />

##BLUE HIGHLIGHTED : PPP on WAN is configured 
ON my PPP i have 2 routers connected to vlan 40 and 50.
1. Asignend IP addresses to routers .
   |ROUTER 1|ROUTER 2 |
   |--------|---------|
   |10.10.10.1|10.10.10.2|
2. ## I Concfgured OSPf
   
   confuguration notes<BR>
   
   ENABLE<BR>
   COMFIGURE TERMIINAL<BR>
   ROUTER OSPF 1<BR>
   ROUTER ID 1.1.1.1 <BR>
   

