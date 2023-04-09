# Dynaaminen reititys

Dynaaminen reititys, mitä helpoiten muistaa reititimen mainostaa lähistön ip-osoitetta. Perinteisesti se tiedonsiirron protokollapinon verkkokerroksen osa, joka päättää, mihin ulostuloihin sisään tulevat datapaketit lähetetään. Tietoliikenne ohjataan kulkemaan tietoliikenneverkossa reittiä, joka kuluttaa vähiten joitakin resursseja.  

Jokaisen reititin vastaanottaa reititystaulun naapurilta. vähä kuin mainostaa naapurin IP-osoitetta, että sillä tallentaa tiedot omaan reititystaulukkoon ja näin se kasvatata sitä etäisyysvektoria ja jne. Tämä tapahtuu säännöllisin väliajoin suoraan naapureina olevien reitittimien kesken molempiin suuntiin.

![Alt text](images/dynamic-router-1.PNG)


## commands

Tarkista reititystaulukko

$show ip protocols
$show ip route | begin gateway
$show ip route | begin default
$show ip route
  
## router rip

- None—The router neither broadcasts its route table nor does it accept any RIP packets from other routers. This option disables RIP. <br>

- In Only—The router accepts RIP information from other router, but does not broadcast its routing table. <br>

- Out Only—The router broadcasts its routing table periodically but does not accept RIP information from other routers. <br>

- Both—The router both broadcasts its routing table and also processes RIP information received from other routers. <br>

<br>

RIP version <br>

- RIP-1—This is a class-based routing version that does not include subnet information. RIP-1 is the most commonly supported version. <br>
- RIP-2B—This version broadcasts data in the entire subnet. <br>
- RIP-2M—This version sends data to multicast addresses. <br>
