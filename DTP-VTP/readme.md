# VTP (Vlan trunk protocol) & DTP (Dynamic trunk protocol)

<h1>VTP & DTP Switch mapping</h1>

DTP konfiguroinnissa tapahtuu vain kytkimen porttien määritys, että VLAN_id voidaan suorittaa mainonnan, mitä määritetty IP-osoitteet kommunikoivat, ja kuin organisaatiot. Myös DTP:ssä vaikuttaa reitityksen protokolla, että porttien moodit, jotta suorittuu joko "trunk" tai "access" moodi. 
<br>
VTP protokolla, mitä tapahtuu verkkotunnus, mitä sisäisen verkkotunnus. Verkkotunnuksen avulla, mitä client moodi kytkin vastaanottaa pää server sisäisen VLAN-id.

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
- Dynamic desirable: DTP dynaamisessa tilassa voi määrittää liitännän luomista DTP viestinnän ympäristön, ja yrittää aktiivisesti muunta toisen puolen kytkimen rajanpinnan "trunk:iksi". Liitännässä tapahtuu "trunk:iksi", jos vastapään tai naapurin liittymä on asetettu "trunk:iksi", "desirable" tai "auto" moodi.
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
Tarkistaa kytkimen sisäisen informaation <br>
$show dtp <br><br>

Tarkistaa kytkimen ethernet porttin switchport tilanne ja moodi tyypin: <br>
$show int fa0/1 switchport <br>

<br>
Mode tyypin määritys kytkimen ethernet portille esim. fa0/1: <br>
Switch(config-if)#switchport mode access <br>
Switch(config-if)#switchport mode trunk <br>
Switch(config-if)#switchport mode dynamic auto <br>
Switch(config-if)#switchport mode dynamic desirable <br>

Switch(config-if)#switchport nonegotiate<br><br>
<hr>

# VTP (VLAN Trunk Protocol)

Tämän protokollan ominaisuus tapahtuu kytkimissä, kun niitä kytkeytyy useisiin kytkimiin, että lähettää data paketin viestin eteenpäin, ja myös siirtää VLAN id viestiä. 
VTP protokolan VLAN:ssa levitää lähiverkkojen määritelmän koko lähiverkon, että VTP toimialueen kytkimessä. VTP rakenteeltaan on esim. pitkä jana tai kuin sukujuuri muotoinen puu rakenne.<br>

VTP cisco protokollossa tapahtuu VLAN informaatio reititys "trunk" moodilla, että voi oletuksena suorittaa VLAN1, mutta jos pitää VLAN-id oma organisaatio. Koska, että oma organisaatiot kommunikoivat oman viestinnän keskenään. VTP ympäristössä tapahtuu "domain", mikä on kommunikoinnin verkkotunnus, mitä reitityksessä tapahtuu "trunk" moodi. Koska verkkotunnus, mitä kuin jakaa seuraavalle kytkimille jatkuvasti edellisen VLAN-id määrän.
<br>

![Alt text](image/VTP-map2.png?raw=true "None") <br>

# VTP switch mode
VTP kytkimien moodeja on:
- server : mitä voi luoda, muokata ja poistaa VLAN-verkkoja, ja määrittää muita kokoonpano parametrejä, kuten VTP-versio ja VTP-karsinnat, että koko VTP-toimialueet <br>
- client : asiakas, mitä kuin toimivat samalla kuin server, mutta ei voi luoda, muuttaa tai poistaa VLAN-verkkoja VTP-asiakkaassa. Client kytkimen verkkotunnuksess tarkoituksena on saada koneet kommunikoimaan, että pinggavat toisia ja on useita VLAN-id:tä. <br>
- transparent : VTP transparent kytkimesssä eivät osallistu VTP:hen. VTP transparent kytkin ei mainosta VLAN kokoonpanoa, eikä synkronoi VLAN kokoonpanoaan vastaanotetujen mainosten perusteella, mutta transparent kytkimet välittävät VTP mainoksia, että ne vastaanottavat trunk porttia VTP-versiossa 2.

# VTP komennot ja yms

Suurin osa kytkimessä on valmiit VLAN:it, että oletuksena on VLAN1 ja natiivi/sisäänrakennettu VLAN 1002 - 1005. Myös kannattaa luoda kuin oma VLAN-id organisatio, että ne kommunikoivat keskennään. 

<h2>Kytkin liittyy verkkotunnkseen / domain & DTP switchport mode</h2>

Domain tarkoittaa verkkotunnus, mitä kuin pää server:issä jakaa sisäisen VLAN:it organisaation muille kytkimen moodille, että kytkimessä on määritetty transparent tai client moodi, sekä pääsevät saamaan pää server:in sisäisen VLAN-id. Client ja transparent moodissa, mitä kytkimen porttien välisen yhteys tulee olemaan "trunk" moodi, koska pää server jakaa useita VLAN-id:tä, että tapahtuu ryhmitys organisaatio. Myös VLAN-id:llä on eri IP-osoite, että ryhmitys ja pinggaus tapahtuu vain omille organisaatioille/ryhmille. <br>
Jos on <u><b>määrittämätön</b></u> kytkin, mitä oletuksena on server, ja kaikki kuin lähtee tyhjästä, että pitää määrittää manuaalinen moodi tyyppi kytkimelle. Myös se toimii kuin tavallinen kytkin, että tietokoneet kommunikoivat ja pinggaavat toisiaan. Jos on kaksi server:iä, mitä yksi niistä pitää kuin pää server.

<br> PS. VTP konfiguroinnin ympäristössä ei tarvitse aina määrittää porttin "trunk" moodiksi, että sallii VLAN-id:tä. Koska on vähä työllistä, mutta nopeiten määrittää kytkin porttin "dynamic deisrable":ksi, että kytkimen client moodi vastaanottaa / saa pääserverin kaikki VLAN-id.

<br> <h2>Kytkimen porttien hallinto moodi, ja välisen yhteys muodostaminen</h2>
esim. transparent fa0/x --------- fa0/y client 

myös voi määrittää vastakohtaisena::
dyanmic auto ------ dynamic auto = access

dynamic desirable --------- dynamic auto = trunk

trunk -------- trunk = trunk

access ------- trunk = syntax error

access --------- access = access

<br> <h2>Domain verkkotunnuksen liittyminen </h2>
Kytkimen pääserver:ssä luoo kytkimen, että voi luoda, muokata tai poistaa VLAN-id:tä, sekä client ja transparent moodit eivät voi luoda, muokata tai poistaa VLAN-id:tä. 

- Domain tunnuksen liittyminen tai luominen, ja vtp moodi
Switch(config)#vtp domain ? <br>
  WORD  The ascii name for the VTP administrative domain. <br>
Switch(config)#vtp domain <nimi> <br>

<h2> (server | transparent | client) määritys </h2>
  
Switch(config)#vtp mode ? <br>
  client       Set the device to client mode. <br>
  server       Set the device to server mode. <br>
  transparent  Set the device to transparent mode.<br>
  <br>
Switch(config)#vtp mode
