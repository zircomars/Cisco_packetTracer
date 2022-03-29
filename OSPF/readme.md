# OSPF (Open Shortest Path First)


- [OSPF areas](#OSPF-areas)
- [OSPF metric and cost](#OSPF-metric-and-cost)
  * [OSPF calculations](#OSPF-calculations)
- [OSPF and EIGRP fusion](#OSPF-and-EIGRP-fusion)
- [](#)
- [](#)

Sitä käytetään erityisesti Internet Protocol (tai IP) -verkoissa. Se on linkitilan reititysprotokolla ja yleisimmin ryhmitelty sisäisten yhdyskäytäväprotokollien kanssa. Se toimii yhden autonomisen järjestelmän (tai AS:n Autonomus System suom. itsenäistä järjestelmää) sisällä. OSPF luokitellaan linkkitilanprotokollana.

Version 1 oli testiversio, ja siitä siirryttiin kohti eteenpäin. Version 2, mikä oli ensimmäinen yleinen versio OSFP:n. Ja versio 2:sta tapahtui muokkausta, ja syntyi version 3, mikä toimii IPV6-osoitteella. 

OSPF:n käyttävien reitittimien on luotava naapurisuhde ennen kuin tapahtuu reittien vaihtamista. Koska OSPF on linkkitilan reititysprotokolla, mitä naapurit eivät vaihda reititystaulukkoa, mutta sijaan vaihtavat tietoa verkon topologiasta. Jokaisen OSPF-reitin suorittaa sitten SPF-algoritmin (Shortest Path first) laskettakseen parhaan reitin, ja lisää ne reititystaulukkoon. Reititin laskee reititysprotokollan algoritmilla nopeimmat reitit itsensä, ja tietämänsä aliverkkojen välillä. Reititysprotkolla myös havaitsee tietojen muutosta, kuten katkenneista reiteistä tai reitittimien porttien muutosta.

<img src="images/OSPF-networkDiagram1.PNG" width="400">

# OSPF areas

# OSPF metric and cost

Metric = cost & laskutus menee: cost = viitekastanleveys / käyttöliittymän kaistanleveys. Oletuksena viitekaistanleveys on 10^8 eli 100 000 000 bps & käyttöliittymä kaistanleveys tarkoittaa reitittimen porttit kuten seriel- ja fast-, giga- ja muu ethernet johto. 

Jokaisen host:i löytyy reititystaulukkosta ($show ip route), että tulostuu esim. [110/65], ja 65 on se host..

<img src="images/OSPF-metricCost1.PNG" width="550">

## OSPF calculations

# OSPF and EIGRP fusion

EIGRP ja OSPF protokollassa on jotakin hyvin samankaltaista yhteistä, mitä selittää protokollien taustalla ja muita syyn kehityksiä. Konfiguraatiossa yhtenä tekijännä on erona OSPF:n ominaisuudessa käyttää alueita, mitä pitää konfiguroida, että vaikka alueita voi olla yksi tai useampi. Sekä EIGRP:ssä konfiguroinnissa tapahtuu mainostaminen, että mainostaa viereisen IP-osoitteen ja sisältyen aliverkkojen määritys, sekä valinta summaus konfigurointi. EIGRP:ssä ja OSPF:ssä lasketaan metriikkat, mutta OSPF:ssä se on cost eli hinta/kustannus, että molemmissa tapahtuu laskenta (matematiikka).

Myös fuusiona, että voi suorittaa kokoonpanon, että reitityksen projektissa suorittaa EIGRP ja OSPF:n protokollan. Reitityksen kommenossa voi mahdollista tuottaa pientä ongelmaa, jotta yhteys pelitää ja reititys toimiii.

<img src="images/EIGRP-OSPF-fusion1.PNG" width="525">
