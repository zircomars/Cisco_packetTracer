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

OSPF protokollassa on viisi tyypistä aluetta (areas), mitkä autonominen järjestelmä voi jakaa alueitta, jotka auttavat vähentämään linkkitilailmoituksia, ja muutaa OSPF-yläliikennettä ja myös lähetettää verkkoon.

<img src="images/OSPF-networkDiagram1.PNG" width="400">

# OSPF areas

OSPF alueita on viisi tyypistä, kuten runkoverkkoalue (backbone area ns. area 0), normaali alue (standard area), tynkäalue (stub area) ja täysin tynkä alue (totally stubby area), ja ei niin tynkkä alue (no so stubby area (NSSA)).

| alueet | kuvaus |
| ----- | ------ |
| runkoverkkoalue | Eng. Backbone area, ja aluen numero on aina alue 0. Kaikkissa muisas alueiden on kytkeydyttävä runkoalueeseen, koska jotta liikenne välitys alueesta toiseen on mahdollisa esim. Area-2 <---> Area-0 <---> Area-4. Runkoalue hyväksyy kaikkien eri LSA-tyypit (Link state Advertisements). Jos käytössä on vain yksi alue, joten aluenumerot voi valita vapaasti, että sen ei tarvitse olla 0. |
| standardi alue | Eng. Standard area. Normali aluenumero, mitä voi mikä tahansa muu paitsi kuin 0, normaalialue hyväksyy kaikki eri LSA-tyypit. |
| tynkäalue | Eng. Stub area, mikä ei hyväksy reititietoa oman AS:n (autonomous system) ulkopuolelta, jos reitittimen pitää reitittää oman AS:n ulkopuolelle, se käyttää oletusreittiä. |
| täysin tynkä alue | Eng. totally stubby area, joka ei hyväksy reitititietoa oman AS:n ulkopuolelta, eikä muista oman AS:n alueista. Jos reitittimen pitää reitittää oman alueen ulkopuolelle, mitä käyttää oletusreittiä. |
| ei niin tynkkä alue | Eng. no so stubby area (NSSA), on eräänlainen tynkä, minkä voi pysyttää tuomaan AS:n ulkoisia reittejä ja lähettämään ne mihin tahansa muuhun alueeseen. Se ei kuitenkaan pysty vastaanottamaan AS:n ulkoisia reittejä verkon muilta alueilta. |

<img src="images/OSPF-areas1.PNG" width="500">

# OSPF metric and cost

Metric = cost & laskutus menee: cost = viitekastanleveys / käyttöliittymän kaistanleveys. Oletuksena viitekaistanleveys on 10^8 eli 100 000 000 bps & käyttöliittymä kaistanleveys tarkoittaa reitittimen porttit kuten seriel- ja fast-, giga- ja muu ethernet johto. 

Jokaisen host:i löytyy reititystaulukkosta ($show ip route), että tulostuu esim. [110/65], ja 65 on se host..

<img src="images/OSPF-metricCost1.PNG" width="550">

## OSPF calculations

# OSPF and EIGRP fusion

EIGRP ja OSPF protokollassa on jotakin hyvin samankaltaista yhteistä, mitä selittää protokollien taustalla ja muita syyn kehityksiä. Konfiguraatiossa yhtenä tekijännä on erona OSPF:n ominaisuudessa käyttää alueita, mitä pitää konfiguroida, että vaikka alueita voi olla yksi tai useampi. Sekä EIGRP:ssä konfiguroinnissa tapahtuu mainostaminen, että mainostaa viereisen IP-osoitteen ja sisältyen aliverkkojen määritys, sekä valinta summaus konfigurointi. EIGRP:ssä ja OSPF:ssä lasketaan metriikkat, mutta OSPF:ssä se on cost eli hinta/kustannus, että molemmissa tapahtuu laskenta (matematiikka).

Myös fuusiona, että voi suorittaa kokoonpanon, että reitityksen projektissa suorittaa EIGRP ja OSPF:n protokollan. Reitityksen kommenossa voi mahdollista tuottaa pientä ongelmaa, jotta yhteys pelitää ja reititys toimiii.

<img src="images/EIGRP-OSPF-fusion1.PNG" width="525">
