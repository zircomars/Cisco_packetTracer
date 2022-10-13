# VPN

Cisco packet tracer VPN konffaukset tulee tänne ja muita harjoituksia

# konffaus tunnel interfaces
## GRE

Generic Routing Encapsulation - GRE on Cisco ympäristön kehittämä IP-tunneloitu protokolla. Sisällä tunneloidaan tavallisen VPN-yhteys, ja tavallisen IP-pakettia, mutta osa siirtää myös multicast- ja IPv6-liikennettä. Protokolla on hyvä väline ja toteuttamisessa käyttävät sitä nopeita ja tehokkaita. 

Tunnelit toimivat virtuaalisina point-to-point-linkkeinä, joilla on kaksi päätepistettä, jotka tunnistaa tunnelin lähde (source)- ja tunnelin kohdeosoite (destination) kussakin päätepisteessä.

<img src="images/cisco-tunnel-int-0.PNG" width="650">

<img src="images/cisco-tunnel-int-1.PNG" width="675">

<h3>esimerkki konffaus</h3>

GRE-tunnelin määrittämisessa edellyttää tunnelinrajapinnan luomista, että on looginen käyttöiittymä (interfaces). Myös tunneliin tulee määrittää päätepisteen tunnelin käyttöliitymä

Määrittämällä tunnelin lähde (source) ja kohteen (destination) antamalla tunneli lähteen:
<br>
$tunnel source {ip-address | interface-type} and tunnel destination {host-name | ip-address}
<br>

| R1 | R2 |
| ------- | ------- |
| R1(config)# ip route 0.0.0.0 0.0.0.0 172.16.1.2 <br> <br> R1(config)# interface Tunnel1 <br> R1(config-if)# ip address 172.16.1.1 255.255.255.0 <br> R1(config-if)# ip mtu 1400 <br> R1(config-if)# ip tcp adjust-mss 1360 <br> R1(config-if)# tunnel source 1.1.1.1 <br> R1(config-if)# tunnel destination 2.2.2.2 <br> | R1(config)# ip route 0.0.0.0 0.0.0.0 172.16.1.1 <br> <br> R2(config)# interface Tunnel1 <br> R2(config-if)# ip address 172.16.1.2 255.255.255.0 <br> R2(config-if)# ip mtu 1400 <br> R2(config-if)# ip tcp adjust-mss 1360 <br> R2(config-if)# tunnel source 2.2.2.2  <br>R2(config-if)# tunnel destination 1.1.1.1 <br>

<h3>2 - esimerkki konffaus</h3>

| R0 | R1 |
| ------- | ------- |
| Router(config)#ip route 0.0.0.0 0.0.0.0 1.0.0.1 <br> Router(config-if)# <br> %LINK-5-CHANGED: Interface Tunnel1, changed state to up <br><br> Router(config-if)#ip add 172.16.1.1 255.255.0.0 <br> Router(config-if)#tunnel source giga <br> Router(config-if)#tunnel source gigabitEthernet 0/1 <br> Router(config-if)#tunnel destination 2.0.0.2 <br> Router(config-if)# <br> %LINEPROTO-5-UPDOWN: Line protocol on Interface Tunnel1, changed state to up <br> <br> Router(config)#ip route 192.168.2.0 255.255.255.0 172.16.1.2 <br> | Router(config)#ip route 0.0.0.0 0.0.0.0 2.0.0.1 <br> Router(config-if)# <br> %LINK-5-CHANGED: Interface Tunnel 2, changed state to up <br><br> Router(config-if)#ip add 172.16.1.2 255.255.0.0 <br> Router(config-if)#tunnel source giga <br> Router(config-if)#tunnel source gigabitEthernet 0/1 <br> Router(config-if)#tunnel destination 1.0.0.2 <br> Router(config-if)# <br> %LINEPROTO-5-UPDOWN: Line protocol on Interface Tunnel1, changed state to up <br> <br> Router(config)#ip route 192.168.1.0 255.255.255.0 172.16.1.1 <br> | 

# tunnel interface ohjeita <br>
https://community.cisco.com/t5/networking-knowledge-base/how-to-configure-a-gre-tunnel/ta-p/3131970
