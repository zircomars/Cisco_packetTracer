<h1>Dynaaminen reititys</h1>

# ip route <ip-address> <router head ip-address>
  
  IP router reityksekssä vaikuttaa IP-osoitteiden luokitusta, koska jokaisella IP-osoitteella on ABC-luokitus.
  <ul> 
    <li> A 10.0.0.0 – 10.255.255.255 </li>
    <li> B 172.16.0.0 – 172.31.255.255 </li>
 <li> C 192.168.0.0 – 192.168.255.255 </li>
    </ul> 
  
# router rip

- None—The router neither broadcasts its route table nor does it accept any RIP packets from other routers. This option disables RIP. <br>

- In Only—The router accepts RIP information from other router, but does not broadcast its routing table. <br>

- Out Only—The router broadcasts its routing table periodically but does not accept RIP information from other routers. <br>

- Both—The router both broadcasts its routing table and also processes RIP information received from other routers. <br>

<br>

RIP version <br>

- RIP-1—This is a class-based routing version that does not include subnet information. RIP-1 is the most commonly supported version. <br>
- RIP-2B—This version broadcasts data in the entire subnet. <br>
- RIP-2M—This version sends data to multicast addresses. <br>
