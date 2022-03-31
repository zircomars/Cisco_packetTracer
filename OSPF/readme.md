# OSPF (Open Shortest Path First)

- [OSPF areas](#OSPF-areas)
  * [LSA types](#LSA-types)
- [OSPF metric and cost](#OSPF-metric-and-cost)
  * [OSPF calculations](#OSPF-calculations)
- [OSPF single and multi areas](#OSPF-single-and-multi-areas)
  * [Single area](#Single-area)
  * [Multi area](#Multi-area)
  * [OSPF DR and DBR](#OSPF-DR-and-DBR)
- [OSPF and EIGRP fusion](#OSPF-and-EIGRP-fusion)
- [OSPF tutoriaalit ja muut guide asiat](#OSPF-tutoriaalit-ja-muut-guide-asiat)

Sitä käytetään erityisesti Internet Protocol (tai IP) -verkoissa. Se on linkitilan reititysprotokolla ja yleisimmin ryhmitelty sisäisten yhdyskäytäväprotokollien kanssa. Se toimii yhden autonomisen järjestelmän (tai AS:n Autonomus System suom. itsenäistä järjestelmää) sisällä. OSPF luokitellaan linkkitilanprotokollana.

Version 1 oli testiversio, ja siitä siirryttiin kohti eteenpäin. Version 2, mikä oli ensimmäinen yleinen versio OSFP:n. Ja versio 2:sta tapahtui muokkausta, ja syntyi version 3, mikä toimii IPV6-osoitteella. 

OSPF reitityksessä tallentaa reititys- ja topologien tiedot kuten: naapuri, topologian ja reititystaulukko. (Neighbor & topology & routing tables)

OSPF:n käyttävien reitittimien on luotava naapurisuhde ennen kuin tapahtuu reittien vaihtamista. Koska OSPF on linkkitilan reititysprotokolla, mitä naapurit eivät vaihda reititystaulukkoa, mutta sijaan vaihtavat tietoa verkon topologiasta. Jokaisen OSPF-reitin suorittaa sitten SPF-algoritmin (Shortest Path first) laskettakseen parhaan reitin, ja lisää ne reititystaulukkoon. Reititin laskee reititysprotokollan algoritmilla nopeimmat reitit itsensä, ja tietämänsä aliverkkojen välillä. Reititysprotkolla myös havaitsee tietojen muutosta, kuten katkenneista reiteistä tai reitittimien porttien muutosta.

OSPF protokollassa on viisi tyypistä aluetta (areas), mitkä autonominen järjestelmä voi jakaa alueitta, jotka auttavat vähentämään linkkitilailmoituksia, ja muutaa OSPF-yläliikennettä ja myös lähetettää verkkoon.

<img src="images/OSPF-networkDiagram1.PNG" width="400">

OSPF - reitityksen komennot, että käyttöliittymistä tarkistaa reitityksen taustat, reititystaulukkot, informaatiot ja muut yksityiskohdat:

| $komennot | komentojen kuvaus |
| --------- | -------- |
| show ip protocols | Tarkistaa koko reitittimien protokollan taustat ja muut informaatiot |
| show ip route | Tarkistaa reitittimen koko reititystaulukkon, että yhteys tyypit ja metriikka luvut |
| show ip route ospf | Tarkistaa koko reitityksen määritettyn ospf tiedot ja infot |
| show ip ospf interface | Tarkistaa informaation koko ospf aktiivisen käyttöliittymän |
| show ip ospf neighbor detail | Listaa ospf naapurien infot ja taustat |
| show ip ospf neighbor | |
| show ip ospf database | Tarkistaa ospf tietokannan datat |
| debug ip ospf events | |


Reitittintyypit OSPF:ssä:

| Tyypit | Kuvaus | 
| ------- | ---- |
| Sisäinen reititin | Tämä reititin sisältää kaikki rajapinnat, jotka kuuluvat toisilleen samalla alueella.|
| Area border router (ABR) | ABR yhdistää yhden tai useamman alueen runkoverkkoon. ABR katsotaan kaikkien niiden alueiden jäseneksi, joihin se on kytketty. Se pitää muistissa useita Link State-tietokantoja, yksi jokaiselle alueelle. |
| runkoverkkoreititin | Reitittintä, jolla on rajapinta runkoverkko alueelle, mitä kutsutaan runkoreittimeksi |
| Autonominen järjestelmän rajareititin | ASBR on reititin, joka on kytketty verkkoon useammalla kuin yhdellä reititysprotokollalla. ASBR vaihtaa reititystietoja itsenäisten reitittimien kanssa. Ne suorittavat ulkoisen reititysprotokollan, käyttävät ilmoitusreittejä tai edes käyttävät molempia menetelmiä. |

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

## LSA types

LSA-tyypit (Link-state advertisement) perus viestintä avulla OSPF:ssän reititys IP protokollaan eli TCP/IP malli. Se kommunikoi reitittimien paikallisten reititystopologien kaikkien muiden paikallisen reitittimien kanssa samalla OSPF-alueella. OSPF on suunniteltu skaalautuvaksi, mitä osa LSA:t eivät ole tulvissa/peittää kaikkiin rajapintoihin, mutta vain niihin, jotka kuuluvat asianmukaisen alueeseen. Yleisen LSA tyypit käytettään 1-5, että 6-11 ovat muita tyyppejä.

<img src="images/OSPF-LSATypes1.PNG" width="550">

| LSA tyypit | Kuvaus | 
| -------- |---------- |
| 1 | reititinlinkkaus (router), sisältä kaikki linkkitunnukset - verkko, jokaisen reitittimien luoma ja paikallinen alue, että reititin lähettää tyypin 1 LSA-paketteja omissa alueessa. |
| 2 | verkkolinkkitila (network), sisältää kaikki segmenttiin liitetyt reitittimet, jotka on luotu DR:llään (Designated Router), ja jotka ovat paikallisia alueita. LSA leviää vain sen alueen sisällä, josta se on peräisin. |
| 3 TAI 4 | koostelinkkitila (Summary LSA & ASBR LSA). Tyyppi 3 kuvaa reittejä paikallisen alueen verkkoihin ja niitä lähetettään runkoalueeseen, että lisäksi sen avulla kertoo paikallisen alueen sisäisille reitittimille, mitkä kohteet voivat saavuttaa ABR:n kautta. Tyyppi 4 kuvaa reittejä ASBR-reitittimiin, että LSA:t leviävät vain sen alueen sisällä, joista sen peräisin ovat. | 
| 5 | ulkoinen linkkitila (autonomous system external LSA). Tyyppi 5 LSA on peräisin ASBR-reittimeltä. Tyyppi 5 kuvaa reittejä sellaisena kohteena, jotka sijaitsevat toisessa AS-alueessa tai toista reititysprotokollaa käyttävissä verkoissa. Tämä LSA leviää koko autonomisen alueen sisällä. |
| 6 | monilähetys (Multicast LSA) |
| 7 | ei niin tynkkä alue (no so stubby area LSA) |
| 8 | ulkoinen attribuuti (external attribute LSA for BGP) |

<img src="images/OSPF-LSATypes2.PNG" width="950">

# OSPF metric and cost

Metric = cost & laskutus menee: cost = viitekastanleveys / käyttöliittymän kaistanleveys. Oletuksena viitekaistanleveys on 10^8 eli 100 000 000 bps & käyttöliittymä kaistanleveys tarkoittaa reitittimen porttit kuten seriel- ja fast-, giga- ja muu ethernet johto. 

Jokaisen host:i löytyy reititystaulukkosta ($show ip route), että tulostuu esim. [110/65], ja 65 on se host..

<img src="images/OSPF-metricCost1.PNG" width="550">

## OSPF calculations

# OSPF single and multi areas

## Single areas

Kun määrittää minkä tahanasa reitityksen, mitä aluksi tapahtuu <ins> yksittäinen alue </ins>, sekä tulee olemaan mukana jos projektissa luoo laajemman monipuolisen alueen. OSPF:ssä on joitain perussääntöjä aluejakoon. Runkoverkko (backbone router) alue 0 tai 0.0.0.0 on määritettävä, koska jos sitä käytää useampaa kuin yhtä aluemääritystä. OSPF:n aluetta voi määrittää kerran, että voi valita minkä tahansa alueen, vaikka tapahtuu ensimmäisenä alueeksi 0. Myös single area on hyvä alku askel, että helppo suorittaa esim. alle 5 reitittimen reititystä, että hyödyssä single area:ssa on:

- Large routing table; suuri reititystaulukko, OSPF:ssä ei oletusarvoisesti suorita reitin yhteenvetoa. JOs reittejä ei ole tiivistetty, reititystaulukko voi tulla hyvin suureksi, riippumatta verkkon koosta.
- Large link-state database (lsdb); LSDB kattaa topologian koko verkon, että jokaisen reitin on säilytettävä merkinnän jokaisen verkon aluealla, vaikka reititystaulukkoon ei ole valittu jokaista reittiä.
- Usein SPF algoritmien laskelmat; suuressa verkossa, muutokset ovat väistämättömiä, joten reitittimet viettävät monia CPU (suoritin, central processing unit) laskemalla uudelleen SPF-algoritmin ja päivittää reititystaulukkoa.

<img src="images/OSPF-singleArea1.PNG" width="400">

## Multi areas

Moni alueessa tapahtuu, että single area on mukana reitityksessä, se on pakko olla keskellä. Koska single area alue 0, mikä kommunikoi moni alueiden välisen yhteyden kuin välittäjänä. Kun verkko laajenee, että reititystauluko, tietokokanta ja SPF-laskelmat voivat kuluttaa kohtuuttoman paljon reitittimen resursseja. Jos suuri OSPF aluetta jaetaan pieniin alueisiin, että tätä myös kutsutaan multi area OSPF:ksi, sekä suuressa verkko alueessa verkon käyttöönotoissa prosessoinnin vähentämiseksi ja muistin yläpuolella. 

Esim. kun reititin saa uutta topologiaa, kuten lisäykset, poistot tai muutosta, jotta reitittimen on uusittava SPF algoritmia, sekä uusi SPF-juuri (Shortest Path First) ja päivittää reititystaulukkon. Multi area OSPF:ssä vaatii hierarkkista verkon suunnittelua. Pääaluetta kutsutaan runkoverkkoalueeksi (area 0), ja kaikkien muiden alueiden on liityttävä runkoalueelle. Koska hierarkkisen reititys tapahtuu edelleen alueiden välillä (interarea routing), kun taas monet pitkäveteiset reititysoperaatiot, kuten tietokannan uudelleenlaskenta, mitä pidetään alueella. OSPF:n hierarkkisen topologioita on kuten:

- Pien reititystaulukko; reititystaulukon merkintöjä on vähemmän verkkoina, että osoitteet voidaan tiivistää alueiden välillä. esim. R1 tiivistää reitit alueelta area 0 ja R2 tiivistää reitit alueelta area 51.
- Reduced link-state update overhead; minimoi käsittelyn ja muistin vaatimukset, koska LSA:n järjestelmässä vaihtelevia reitittimiä on vähemmän.
- Reduced frequency of SPF calculations;

<b>SPF tree topology</b> <br>
<img src="images/OSPF-spfTree1.png" width="500">

<img src="images/OSPF-MultiArea1.PNG" width="400">

## OSPF DR and BDR

DR (Designated Router) & BDR (Backup Designated Router). <br>

BDR - varalla oleva hallitseva reititin OSPF-protokollaa käyttävässä multiaccess-verkkoa & DR - halitseva reititin OSPF-protokollaa käyttävässä multiaccess-verkossa. <ins> Multiaccess </ins> tarkoittaa verkkoa, että on enemmän kuin kaksi reititintä yhdistettynä toisiinsa samassa aliverkossa esim. kytkimen kautta. Yhdistetyt reitittimen kokoonpanossa muodostavat konvergenssin (lähentyminen / yhteen suuntautuminen), missä ne synkronoivat tietokantansa. Kun tietokantojen synkronointi on valmis, mitä naapurireitittimet muodostavat tilaan nimellä *adjacency*, mikä tarkoittaa muodostuu kahden reitittimen välisissä yhteyksissä *Point-to-Point*-yhteyksiä. Multiaccess-verkoissa adjency-toiminassa kuuluu, joka OSPF-protokolla valikoi yhden reitittimestä hallitsevaksi reitittimeksi rooliin <b> DR </b>, mikä muodostaa adjancency:n muiden naapurien kanssa. Tämä yksinkertaistaa verkon toiminnan, koska DR voi lakata toiminnasta, että valitaan myös varalla oleva hallitseva reititin <b> BDR </b>. Sekä muut olevat reitittimet ovat nimellä <b>DROther</b> <br>

Verkon ylläpitäjä (network system administrator) voi määrittää reitittimien arvojärjestyksen manuaalisesti. Tärkein vaihtoehto on muuttaa DR:ksi halutun reittimen multiaccess-verkkon yhdistävän siirtoyhteyden prioritetti suuremmaksi kuin muu reitittimet. Prioritettin oletusarvo on 1, sekä prioritetti sattuu olemaan nolla, mitä reitittimestä ei voi tulla <b> DR:ksi eikä BDR:ksi. </b> Vaihtoehtona on asetta DR:ksi haluttuen reitittimelle mahdollisimman suuri IP-osoitteeksi. Verkossa käytettäessä osoitteesta riippumatta tämä voi tehdä esimerkiksi määrittämällä reitittimelle erikseen Router-ID tai konfiguroida reitittimelle yksittäinen loopback-portti osoite.

DR:n tehtävänä on pitää muiden samassa multiaccess verkossa olevien OSPF:n protokollien käyttävien reitittimien linkkitilausksien tietokannat ajan tasalla. Jos DR-reititin kaatuu tai sammuu, mitä BDR-reitittimestä tulee uusi DR ja DROther-reitittimien ympäristössä/reititiyksessä valitaan uusi BDR. Kun alkuperäisen DR palaa toimintaan eli palaa käyntiin, siitä ei tule uudestaan DR-reititintä, vaan DROther. DROther valitaan DR:ksi jos sekä DR ja BDR lakkautuvat toiminnasta.

<img src="images/OSPF-DR-BDR1.PNG" width="800">

# OSPF and EIGRP fusion

EIGRP ja OSPF protokollassa on jotakin hyvin samankaltaista yhteistä, mitä selittää protokollien taustalla ja muita syyn kehityksiä. Konfiguraatiossa yhtenä tekijännä on erona OSPF:n ominaisuudessa käyttää alueita, mitä pitää konfiguroida, että vaikka alueita voi olla yksi tai useampi. Sekä EIGRP:ssä konfiguroinnissa tapahtuu mainostaminen, että mainostaa viereisen IP-osoitteen ja sisältyen aliverkkojen määritys, sekä valinta summaus konfigurointi. EIGRP:ssä ja OSPF:ssä lasketaan metriikkat, mutta OSPF:ssä se on cost eli hinta/kustannus, että molemmissa tapahtuu laskenta (matematiikka).

Molemmissa ovat sisäisten yhdyskäytävän  reititysprokollia, mitkä auttavat valitsemaan reitit tiedon siirtämistä tai jakamisen vuorovaikutuksen reitittimen kansa. EIGRP:ssä tapahtuu etäisyyvektorireititysprotokolla, ja OSPF käyttää linkkitilan reititysprotokollaa. Molemmissa on kyky oppia verkon dynaamista reittiä, että molempien toiminallisuus on samalainen, mutta osassa on eroa. Esim. EIGRP on Cisc oma IGP, mikä tarkoittaa, että se on suosittu Cisco verkoissa, ja OSPF on avoimen standardi IGP yritysverkoille. Jos vertaa molempien protokollaa

<img src="images/OSPF-EIGRP-diff.PNG" width="750">

Myös fuusiona, että voi suorittaa kokoonpanon, että reitityksen projektissa suorittaa EIGRP ja OSPF:n protokollan. Reitityksen kommenossa voi mahdollista tuottaa pientä ongelmaa, jotta yhteys pelitää ja reititys toimiii.

<img src="images/EIGRP-OSPF-fusion1.PNG" width="525">

# OSPF tutoriaalit ja muut guide asiat

http://ladu.htk.tlu.ee/erika/lasse/routing_protocols/esimerkki_linkkitilaprotokollistaospf.html
https://education-wiki.com/3990219-what-is-ospf


<h2>LSA tyyppit</h2>

https://www.firewall.cx/networking-topics/routing/ospf-routing-protocol/1178-ospf-lsa-types-explained.html

<h2>OSPF linkkit tyypit</h2> <br>
https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/7039-1.html#anc44 <br>
http://www.netcontractor.pl/blog/?p=451 <br>
https://stucknactive.com/2019/04/02/6-14-ospf-lsa-types/ <br>
https://www.digitaltut.com/ospf-lsa-types-tutorial <br>

<h2>EIGRP vs OSPF</h2>
https://askanydifference.com/difference-between-eigrp-and-ospf-with-table/
https://www.router-switch.com/faq/ospf-vs-eigrp.html
https://techdifferences.com/difference-between-eigrp-and-ospf.html
https://www.educba.com/eigrp-vs-ospf/
