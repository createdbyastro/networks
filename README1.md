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




                
                
