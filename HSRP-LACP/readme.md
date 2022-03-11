# EtherChannel (LAPC & PAgP) & FHRP

![Alt text](images/HSRP-LACP-map1.PNG?raw=true)

Kahden tai useamman kytkimien porttien välisen yhteys, että kytkeyttyy / käytettään useita portteja, sekä erikseen oma johto kaapeli fyysisen isännän tietokoneelle. Ilman linkkien yhdistämistä STP estää ylimääräiset linkit reitityssilmukat. EtherChannel-tekniikka on Ciscon Switch-to-Switch-tekniikka, joka ryhmittelee useita Fast Ethernet- tai Gigabit Ethernet -portteja yhdeksi loogiseksi kanavaksi. Kytkimien sisäisen kokkoonpanossa voi olla Fast, Gigabit tai 10-Gigabit Ethernet portti, mitä voi yhdestää kahdeksaan ylimääräistä passiivista rajapintaa, jotka voivat aktivoitua, kun muut liitännät epäonnistuvat. Tämä olettaa, että liikenneseos on olemassa, koska nämä nopeudet eivät koske vain yhtä sovellusta. Sitä voidaan käyttää Ethernet-liitännällä, joka on kierretty parikaapelissa, yksimuotoinen- ja monimuotoinen kuitu. Parikaapelista voidaan kytkeä joko perus suora- tai ristikytkentä kaapeli, että suorassa on molemmissa päissä malliltaan joko T568A tai -B, sekä ristitkytkentä kaapeli tarkoittaa pää on T568A ja häntä T568B.

Kytkimien asentamisessa, mitä tapahtuu ensimmäisenä STP protokolla, jos on ilman EtherChannel protokollan konfigurointia, mitä tapahtuu perus pakotettu juuri, sekä kytkimien porttien root ja block asema. Jos asetettaan EtherChannel protkollan käyttöön kytkimien linkeissä, että kaikki linkkitilat ovat ylhäällä. Tämä tarkoittaa, että voi hyödyntää kaikkia asennettun linkkit ja hyötyä EtherChannelin eduista, nimittäin kuormituksen tasapainotuksesta, redundanssista ja lisääntyneestä kaistanleveydestä. 

EtherChannel kytkennässä tapahtuu sama dupleksi, nopeus, VLAN konfigurointi (Oletus VLAN1 ja useita tai rajoitettu VLAN-id organisaatio), ja kytkimen porttien moodi (access tai trunk). EtherChannel edussa / hyödyssä on:
- Usein konfigurointi harjoituksissa / tehtävissä voi tehdä EtherChannel käyttöliittymän kunkin yksittäisen portin sijaan.
- Käytössä on olemassa olevia kytkinporttei, ei tarvi päivitystä tarvitaessa, ellei tarvi lisää kaistanleveyttä.
- Sama EtherChannel linkkien välisen kuormitustaso.
- Luo koosteen, mitä STP pitää yhtenä loogisena linkkeinä.
- Tarjoaa redudanssin, koska kokonaislinkkeinä pidetään yhtenä looginen yhteys. Jos yksi fyysinen linkkitys portti katkee, mitä ei aiheuta muutosta topologiassa eikä vaadi STp uudelleen laskentaa.

# EtherChannel Protokollat (PAgP & LACP)

- Cisco: Ether Channel, <ins> PAgP </ins> (Port Aggregation Protocol) Ciscon oma EtherChannel-protokolla, jossa voi yhdistää enintään 8 fyysistä linkkiä yhdeksi virtuaaliseksi linkiksi.  <br>
-  IEEE: <ins> LACP </ins> (Link Aggregation Control Protocol) IEEE 802.3ad -standardi, jossa voi yhdistää jopa 8 porttia, jotka voivat olla aktiivisia, ja toiset 8 porttia, jotka voivat olla valmiustilassa. <br>

<!--
Molempien konfiguroinnissa tapahtuu kuin DTP/VTP protokolla, että sisältyen kokoonpanoon STP protokolla. Porttien kytkimessä, mitä vaikuttaa kahden tai useamman kytkimen porttien operaation määritys, sekä kyseisen VLAN-id ja muu operaatio moodit. Operaation moodista on vain kaksi tyypistä (access & trunk), että jakaa sisäisen tai luoneen VLAN-id toiselle kytkimelle/reitittimelle, ja koneen isännät kommunikoivat oman organisaatioiden ryhmien kanssa. Esim. VLAN10 oma IP-osoite, ja VLAN20 ja jne. Sekä kytkimien välisen porttien yhdistämisessä vaikuttaa määritykseen, että onko kysessä useampi kuin kahden kytkimien yhdistäminen vai kolmen kytkimen kokonpano. Koska kytkimien porttien maksimi ja minim määrä, vaikuttaa konfiguroinnin määritykseen, sekä onko LACP tai PAgP moodi. -->

Molempien konfiguroinnissa tapahtuu kuin <ins> DTP/VTP </ins> protokolla, että sisältyen kokoonpanoon <ins> STP </ins> protokolla. DTP/VTP prokolla tarkoittaa, että kytkimien porttien operaation moodi määritys, mutta EtherChannel porttienlinkkien yhditämisessä määritettään kahden tai useamman porttien arkkitehtuuria, sekä erillisenä operaation moodi (access & trunk) määritys on itsensä erillinen operaatio. STP, mikä liittyy Etherchannel teknologiin, koska kytkimien porttien yhdistämisessä tapahtuu pakotettu juuri (bridge root), oletus prioriteetti (32 769) ja Etherchannel oman portti-kanavan-id kokoonpano (port-channel y). Portti-kanavan määrityksestä, mitä lisääntyy STP yhteenvedon taulukkoon ($show spanning tree).<br>

Etherchannel kokoonpanossa tapahtuu perus kahden tai useamman kytkimen kokoonpano esim. kytkin-1 ja kytkin-2 välissä kytkeytyy Ethernet num. 2-4 porttien linkkitystä, että tässä linkkityksessä määritettään PAgP tai LACP protokollaa. Valitujen protokollasta, mitä tapahtuu johdonmukainen konfigurointi komento, että kohteen kytkimen Ethernet num. 2-4 muodostuu portti kanava ryhmitys numero. 

KytkinS1 useampi kuin portti fa0/x (active/passive) ------------- (active) fa0/y useampi portti KytkinS2

![Alt text](images/EtherChannel-modesType.png?raw=true)

<h2>LACP (Link Aggregation Control Protocol) </h2>

LACP on IEEE-standardi, ja osa IEEE 802.3ad -spesifikaatio, mitä sen avulla voi yhdistää useita fyysisiä Ethernet -linkkei verkkolaitteeseen yhdeksi loogiseksi linkiksi, ja mahdollistaa kuormituksen tasaisella liittännässä. Konfiguroinnissa tapahtuu LACP EtherChannel enintään 16 samantyypistä Ethernet verkkoliitäntää. Paikallisessa toiminta ryhmissä tai linkkien yhdistämis ryhmissä enintään 8 jäsenlinkkiä, mitä voi olla aktiivisessa tilassa ja muut 8 voi olla valmiustilassa. Sekä LACP:llä on kaksi tyypistä konfigurointi tyypistä moodia:

- <ins> Active </ins> - Liitäntä lähettää aktiivisesti LACP-paketteja yrittäessään muodostaa LACP-yhteyden. Konfiguroinnissa tapahtuu, kun se suorittaa liitännän määritystilan, että asettaa kanavaryhmän (channel-group) numeron, ja LACP-tilassa yrittämään aggressiiviesti muodostaa LACP EtherChannel protokollan. Jos neuvottelut (negotiations) epäonnistuu, mitä EtherChannel ohitaa liikennettä.
- <ins> Passive </ins> - Käyttöliittymä voi vastata LACP-neuvotteluihin, mutta se ei koskaan aloita itsestään. Konfiguroinnissa tapahtuu, kun se suoritaa liitännän määritystilan, että asettaa kanavaryhmän (channel-group) numeron, ja LACP-tilan kuntelemaan LACP-paketteja, mutta ei aggressiivisesti ja ehdoitta muodostamaan EtherChannel:ia LACP:n avulla.

![Alt text](images/EtherChannel-LACP.PNG?raw=true)

<h2>PAgP (Port Aggregation Protocol) </h2>

PAgP on on EtherChannel-tekniikka, joka on Ciscon oma protokolla. Se on Cisco Ethernet -kytkinporttien looginen yhdistämismuoto, ja  mahdollistaa tiedon / liikenteen kuormituksen tasapainotuksen. PAgP EtherChannel voi yhdistää enintään 8 fyysistä linkkiä yhdeksi virtuaaliseksi linkiksi. Se on myös avoin IEEE-standardi, Link Aggregation Control Protocol, LACP. Myös PAgp teknisessä on kaksi tyypistä moodia kuin "Auto" ja "desirable" - moodit, että vaikuttaa myös yhdistelmän erissä prosessissa ja toimiiko linkkien yhdistäämisen Cisco laitteiden välissä vai ei.

- <ins> Auto moodi </ins> - käyttöliittymä voi vastata PAgP-pakettineuvotteluihin, mutta ei koskaan käynnistä sitä yksinään. Auto moodin konfiguroinnissa tapahtuu,  kun se suoritaa liitännän määritystilassa, että asettaa kanavaryhmän (channel-group) numeron, ja PAgP-tilassa kuuntelee PAgP-paketteja, mutta ei neuvottele agressiivisiä PAgP EtherChannel:ia.
Desirable moodi - rajapinta yrittää aktiivisesti neuvottelutilaa PAgP-pakettien neuvottelua varten. 
- <ins> Desirable </ins> konfiguroinnissa tapahtuu, kun se suoritaa liitännän määritystilassa, että asettaa kanavaryhmän (channel-group) numeron, ja PAgP-tilassa yrittää aggressiivisesti muodostaa PAgP EtherChannel. Jos neuvottelut (negotiations) epäonnistuu, mitä EtherChannel ei ohita liikennettä.

![Alt text](images/EtherChannel-PAGP.PNG?raw=true)

Cisco teknisessä on patentoitu protokolla, mitä on varmistettava, että kaikilla liitännöillä on samat kokoonpanot:
- Nopeus ja dupleksi
- porttien operaation moodi (access & trunk)
- access VLAN käyttöliittymät, oletus VLAN ja sallii VLAN-id:tä käyttöliittymässä
- STP asetukset

<hr>

# EthernetChannel, HSRP ja muut ohjeet, konfiguraatiot & muu opas:

http://vapenik.s.cnl.sk/pcsiete/CCNA3/04_EtherChannel_HSRP.pdf <br>
https://www.freeccnaworkbook.com/workbooks/ccna/configuring-etherchannel-utilizing-pagp <br>
https://www.cisco.com/c/en/us/support/docs/lan-switching/etherchannel/12023-4.html <br>
https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst2960/software/release/12-2_25_sed/configuration/guide/scg1/swethchl.pdf <br>

<h3>PAGP tutoriaalit ja muut ohjeet: </h3> <br>

https://study-ccna.com/port-aggregation-protocol-pagp/ <br>
https://www.omnisecu.com/cisco-certified-network-associate-ccna/how-to-configure-etherchannel-port-aggregation-protocol-pagp-in-cisco-switch.php  <br>

<h3>LACP tutoriaalit & Port-channel ja muut ohjeet: </h3>

https://study-ccna.com/link-aggregation-control-protocol-lacp/ <br>
https://www.cisco.com/c/en/us/td/docs/ios/12_2sb/feature/guide/gigeth.html <br>
https://www.freeccnaworkbook.com/workbooks/ccna/configuring-etherchannel-utilizing-lacp <br>

https://www.grandmetric.com/knowledge-base/design_and_configure/how-to-configure-lacp-on-cisco/ <br>
https://www.omnisecu.com/cisco-certified-network-associate-ccna/how-to-configure-etherchannel-link-aggregation-control-protocol-lacp-in-cisco-switch.php <br>

https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus9000/sw/7-x/interfaces/configuration/guide/b_Cisco_Nexus_9000_Series_NX-OS_Interfaces_Configuration_Guide_7x/configuring_port_channels.pdf
