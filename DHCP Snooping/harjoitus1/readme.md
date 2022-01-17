<h1>Dynamic host configuration portocol snooping configuration</h1>

Määrityksessä tapahtuu "trust", mitä kuin luotettaan oma määrittämä reititin ja serveri, ja muussa tapahtuu sitä nuuskinta tai turvallisuuden tekniikkaa. 
Tämän tekniikkan tapahtuu kytkimessä, että määritettyksessä mitä tietokoneet kommunikoivat keskennään.

<hr>

<h2>Arp protokolla reititys</h2>

Cisco packet tracer reitityksessä ARP protokolla tunnistaa pinggauksen, tai viesti on onnistunut/saappunut perille. 
ARP protokolla perus selvittää Ethernet verkon käytetäävän loogisen osoitteen vastaavan fyysinen osoite. Käyttäjän tietokone on perus IP-osoite, mutta fyysinen osoite on MAC-osoite. Varsinaisen arp protokollan tarkistaminen voi tarkistaa komennosta (CMD) komennolla, "arp -a" , mitä tulostuksena tulostuu internet ip-osoite, fyysinen mac-osoite ja tyyppi (dynaaminen/staatinen)

![alt text](images/ARP-dynamic.PNG?raw=true)
![alt text](images/ARP-PC-arpAdd_After.PNG?raw=true)
![alt text](images/ARP-PC-arpAdd_Before.PNG?raw=true)

<hr>

<h2>Varsinainen DHCP snooping reititys </h2>

DHCP serverin reititys, ja koneet DHCP:ksi.

![alt text](images/DHCP-snoopDynamic.PNG?raw=true)
![alt text](images/DHCP-snoop-ServerDHCPadd.PNG?raw=true)
![alt text](images/DHCP-snoop-ServerOwnAdd.PNG?raw=true)
![alt text](images/DHCP-snoopPCadd.PNG?raw=true)

<h2>Kone DHCP:ksi, ja reititin DHCH snooping määritys</h2>

Reititin DHCP snooping reitityksi, että vastapäässä on luotettava serveri, ja koneet ovat kuin DHCP käyttäjiä. Koska serveri on se luotettava portti, kun sieltää määrittyy DHCP reititys ja polku. Myös oletus VLAN 1 on mukana reitityksessä. 

"IP dhcp snooping" - mitä tulostaa kytkimen määritettyn luotettavan porttin kulku, että serveristä saadaan DHCP reititys tietokoneelle.

Viimeisenä "ip dhcp snooping binding" kuin sitova tai yhteenveto, että kytkin havaitsee / analysoinnut tietokoneiden DHCP reitityksen, että tulostuksena on kytkin porttien yksityiskohdat. Muu tuloksena, että porttin fa/x on y-kone, ja y-koneen sisäisen IP- ja fyysinen MAC-osoite.

![alt text](images/DHCP-snoopSWTrustedPort.PNG?raw=true)
![alt text](images/DHCP-snooping-bindingTable.jpg?raw=true)

<hr>

<h2> harjoitukset ja pientä tutoriaali & ohjetta, että konfigurointia: </h2><br>
https://study-ccna.com/dhcp-snooping/ <br>
https://study-ccna.com/dynamic-arp-inspection-dai/ <br>

<br>
https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst6500/ios/12-2SXF/native/configuration/guide/swcg/snoodhcp.pdf
