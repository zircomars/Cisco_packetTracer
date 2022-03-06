# EtherChannel & HSRP

Kahden kytkimien porttien välisen yhteys, että kytkeyttyy tai käytettään useita portteja, sekä erikseen oma johto kaapeli fyysisen isännän tietokoneelle. Ilman linkkien yhdistämistä STP estää ylimääräiset linkit reitityssilmukat. EtherChannel-tekniikka on Ciscon Switch-to-Switch-tekniikka, joka ryhmittelee useita Fast Ethernet- tai Gigabit Ethernet -portteja yhdeksi loogiseksi kanavaksi. Kytkimien sisäisen kokkoonpanossa voi olla Fast, Gigabit tai 10-Gigabit Ethernet portti, mitä voi yhdestäö kahdeksaan ylimääräistä passiivista rajapintaa, jotka voivat aktivoitua, kun muut liitännät epäonnistuvat. 

Kytkimien asentamisessa, mitä tapahtuu ensimmäisenä STP protokolla, jos on ilman EtherChannel protokollan konfigurointia, mitä tapahtuu perus pakotettu juuri, sekä kytkimien porttien root ja block asema. Jos otettaan EtherChannelin käyttöön kytkimien linkeissä, että kaikki linkkitilat ovat ylhäällä. Tämä tarkoittaa, että voi hyödyntää kaikkia asennettun linkkit ja hyötyä EtherChannelin eduista, nimittäin kuormituksen tasapainotuksesta, redundanssista ja lisääntyneestä kaistanleveydestä. 

EtherChannel kytkennässä tapahtuu sama dupleksi, nopeus, VLAN konfigurointi (Oletus VLAN1 ja useita tai rajoitettu VLAN-id organisaatio), ja kytkimen porttien moodi (access tai trunk). EtherChannel edussa / hyödyssä on:
- Usein konfigurointi harjoituksissa / tehtävissä voi tehdä EtherChannel käyttöliittymän kunkin yksittäisen portin sijaan.
- Käytössä on olemassa olevia kytkinporttei, ei tarvi päivitystä tarvitaessa, ellei tarvi lisää kaistanleveyttä.
- Sama EtherChannel linkkien välisen kuormitustaso.
- Luo koosteen, mitä STP pitää yhtenä loogisena linkkeinä.
- Tarjoaa redudanssin, koska kokonaislinkkeinä pidetään yhtenä looginen yhteys. Jos yksi fyysinen linkkitys portti katkee, mitä ei aiheuta muutosta topologiassa eikä vaadi STp uudelleen laskentaa.

# EtherChannel Protokollat

- Cisco: Ether Channel, PAgP (Port Aggregation Protocol) Ciscon oma EtherChannel-protokolla, jossa voi yhdistää enintään 8 fyysistä linkkiä yhdeksi virtuaaliseksi linkiksi.  <br>
-  IEEE: LACP (Link Aggregation Control Protocol) IEEE 802.3ad -standardi, jossa voi yhdistää jopa 8 porttia, jotka voivat olla aktiivisia, ja toiset 8 porttia, jotka voivat olla valmiustilassa. <br>

<h3>PAgp (Port Aggregation Protocol) </h3>

<h3>LACP (Link Aggregation Control Protocol) </h3>

# EthernetChannel, HSRP ja muut ohjeet, konfiguraatiot & muu opas:
