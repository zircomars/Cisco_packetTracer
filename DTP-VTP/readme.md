# VTP (Vlan trunk protocol) & DTP (Dynamic trunk protocol)

<h1>VTP & DTP Switch mapping</h1>

![Alt text](image/VTP-map1.png?raw=true "None") <br>

# DTP (Dynamic trunking protocol)

Tämä on trunking protokollan käytettävä automaatinen käsittelevä Cisco runko (trunkaus) Cisco kytkimien välillä. DTP hallitsee trunkauksen neuvottleun vain, jos portit on kytketty suoraan toisiinsa.

Ethernet verkko trunk verkkoliitänässä tukevat erilaisia kanavatiloja. Nämä liitännät voi konfiguroida trunk-johdoksi tai ei-trunkkausta, tai niitä voi käynnistää käsittely-trunk johdannoksi naapurirajapinnalle, tai odottaa saavansa johdon mukaisen trunk viestin toiselta suoraan yhdistelyltä rajapinnalta. Useimmat Cisco kytkimet käyttävät nykyään IEE 802.1Q:ta johdontyyppinö, koska ne ovat pienemmät kuin Inter-Switch Link (ISL)

<h2>DTP interfaces mode taulukko</h2>

DTP neuvottleu sisältää DPT-kehysten vaihdon kahden vierekkäisen rajapinnan välillä. Kun liitäntä on konfiguroitu Switchport dynamisen automaatti- tai dynaamisen toivottuihin tiloihin, mitä se aloittaa DTP-neuvottelun valitakseen oman johtokanavan toimintatilan.

Kun liitäntä on staattisesti määritetty pääsy- tai runkotilaan (access & trunk mode), se osallistuu normaalisti DTP-prosessiin vastaamalla DTP-kehyksiin, jos se vastaanottaa sellaisia.

Taulukko interface, mitä kuvaa kuinka liitäntä valitsee johtokanavan toiminta tavan, että oman trunk-johdon hallintatavan ja DTP-prosessin tulosten perusteella.

![Alt text](image/DTP-InterfaceModes.PNG?raw=true "None") <br>

Edellisen taulukkon pari-muutama modeemi tyyppien erot: <br>
- Dynamic auto: kytkimien oletus porttien modeemi, mitä määrittyy dynamic auto tila, se ei aktiivisesti muuta puolta eli trunk tai access modeemiksi käyttöliittymässä. Tämän automaatinen järjestelmä, mitä liitänässä tulee "trunk" liittäntä vain, jos toisen puoli tulee kytketty liitäntä konfigurointi manuaalisesti "trunk:ksi" tai "dynamic desirable" moodiksi. <br>
- Dynamic desirable: DTP dynaamisessa tilassa voi määrittää litäännän luomista DTP viestinnän ympäristön, ja yrittää aktiivisesti muunta toisen puolen kytkimen rajanpinnan "trunk:iksi"
<br>

<h2>Esimerkkit</h2>

Jos kahden kytkimien välisen toiminta pitää suorittaa konfiguroinnin, että tapahtuu kommunikointi kuten VLAN-id. Oletuksena kytkimissä on VLAN1, mitä kommunikoi ja pinggavat. Jos luoo useampi VLAN-id ryhmän, mitä kytkin portti ei ymmärrä toisia, joten pitää luoda operaatio toiminta tai hallinnon tila ethernet portille. Koska, jokaisen portti ovat oletuksena "dynamic auto", sekä myös uuden projektin luomisessa ja siksi pitää manuaalisesti määrittää yksittelen porttin toimintatilan.
<br><br>
Tämän esimerkkin porttien määrityksessä vaikuttaa vastapään kytkimen kommunikoinnin, että modeemit tuntevat/ymmärtävät toisiaan. Sekä edellisen kuvan taulukkon mukaan, että porttit kommunikoivat ja muodostavat jokin modeemin tyyppin. 
<br> Myös kannattaa tarkistaa kytkimen kohteen porttin taustat, että oletuksena on "dynamic auto" valmiina
<br>
- Jos Switch0 FA0/1 portti on "trunk" ja Switch1 fa0/1 portti on "trunk, mitä välinen yhteys muuttuu trunk
- Jos -//- fa0/1 portti on "access" ja -//- fa0/1 portti on "dynamic auto", mitä välinen yhteys muuttuu access
- Jos porttiin tulee määrittää trunk moodia, mitä reitityksen sisällä voi sallia ja suorittaa määritettyn VLAN-id määrän, että rajan VLAN-id tai poistaa joukkosta. Koska, että esim. poistettu VLAN-id on kuin lakautettu, ja muut voivat kommunikoida muiden koneiden kanssa.
<br><br>
Esim. Switch0 fa0/1 ------------- Switch1 fa0/1<br>
ps. muista sallia VLAN (allowed vlan x-y) määrän

![Alt text](image/DTP-portExample.PNG?raw=true "None") <br>

![Alt text](image/DTP-switchPortStatus.PNG?raw=true "None") <br>

<h2>DTP komennot ja muut taustat/ominaisuudet</h2>




<hr>

# VTP (VLAN Trunk Protocol)

Tämän protokollan ominaisuus tapahtuu kytkimissä, kun niitä kytkeytyy useisiin kytkimiin, että lähettää data paketin viestin eteenpäin, ja myös siirtää VLAN id viestiä. 
VTP protokolan VLAN:ssa levitää lähiverkkojen määritelmän koko lähiverkon, että VTP toimialueen kytkimessä. VTP rakenteeltaan on esim. pitkä jana tai kuin sukujuuri muotoinen puu rakenne.

<br>

![Alt text](image/VTP-map2.png?raw=true "None") <br>

# VTP switch mode
VTP kytkimien moodeja on:
- server : mitä voi luoda, muokata ja poistaa VLAN-verkkoja, ja määrittää muita kokoonpano parametrejä, kuten VTP-versio ja VTP-karsinnat, että koko VTP-toimialueet <br>
- client : asiakas, mitä kuin toimivat samalla kuin server, mutta ei voi luoda, muuttaa tai poistaa VLAN-verkkoja VTP-asiakkaassa. <br>
- transparent : VTP transparent kytkimesssä eivät osallistu VTP:hen. VTP transparent kytkin ei mainosta VLAN kokoonpanoa, eikä synkronoi VLAN kokoonpanoaan vastaanotetujen mainosten perusteella, mutta transparent kytkimet välittävät VTP mainoksia, että ne vastaanottavat trunk porttia VTP-versiossa 2.
