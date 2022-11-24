# STP (spanning tree protocol)

Tarkoittaa, että esim. kolme tai useampi kytkintä (switch), kulkeutuu sellainen kolmio tai puu juuren/oksan näköinen muoto, jos yksi niistä portista on poikki, niin viesti kulkeutuu toisesta reitistä, mutta portti pitää vastaanottaa se ja lähettää viestin eteenpäin omasta kytkimen portista. <br>

Kytketty ympäristö, joka eroaa siltaympäristöstä, mitä käsittelee useita VLAN-verkkoja. Kun otat käyttöön pakotetun juurin kytkentäverkossa, käytät yleensä juurisiltaa juurikytkimenä. Jokaisella VLANilla on oltava oma juurisilta, koska jokainen VLAN on erillinen lähetysalue. Kaikkien eri VLAN-verkkojen juuret voivat sijaita yhdessä kytkimessä tai useissa kytkimissä. Jos yhtäkkiä yhteys katkee, mitä viesti kulkeutuu toisesta reitistä, koska jotta STP ympäristössä tapahtuu reititys, jotta se pääsisi perille asti.
<br><br>
switch1 ----- switch2 ------ switch3 ---- switch1  <br>

esim switch2 ja switch3 välinen yhteys on poikki, niin viesti kulkeutuu kohti switch1:stä kohti switch3:lle, mutta kulkeutumisen välisen yhteys pitää olla trunk moodi. Koska jos on useampi VLAN-id, että taisi organisaation tai ryhmä viestin kuljettua perille. <br><br>
![Alt text](image/STP-topology1.PNG?raw=true "None") <br>

# Kytkimen porttien roolit ja asemat

![Alt text](image/STP-SwitchDetails.png?raw=true "None") <br>

Kytkimien porttissa tapahtuu rooli STP ympäristössä, kun kytkeytyy ristikytkentä. Koska suorakytkentä, mitä kuin toimii ristikytkentä, mutta sisäisen fyysisen kaapeli asennettu erilaisena. Eri porttien rooleja tapahtuu spanning tree hallintoi verkojen topologiassa ja redudanttisia yhteyksiä, että välityssilmukka ei pääse muodostumaan. Spanning tree porttien rooleja on kuten:

- Root - portti: mitä sijaitsee muissa kytkimissä, ja nopeis reitti root kytkimille. Root portti, mitä välittää dataliikennettä kohti muihin root-kytkimiin, ja saapuvista root-portti data framien lähettäjälaitteen MAC-osoite voidaan tallentaa MAC-taulukkoon. Jokaisessa kytkimessä voi olla vain yksi root-portti.
- Designated - portti: tämä porttin rooli, mitä voi olla sekä root tai muissa kytkimissä. Root kytkimien kaikki portti ovat designated portteja. Koska designated-portit vastaanottavat ja välittävät dataliikennettä kohti root-kytkentään, ja vain yksi designated-portti voi olla verkkosegmentti kohde. Saapuvien data framien lähttäjien MAC-osoite voidaan tallentaa MAC-taulukkoon.
- Nondesignated - portti: Mikä on kuin "ei designoitu), mitä ei välitä dataliikennettä eli kuin estetty (blocking) portti. Saapuvien porttien data frame lähettäjien MAC-osoitetta ei tallenna MAC-taulukkoon.
- Disabled portti: mitä tarkoittaa suljettu portti.
<br>
Myös jokaisessa portissa on roolien tilanne tai aseman taustat (state), että datan välitäessä tai estetyissä tilassa, ja spanning tree:n muodstaman loogisen topologia protokolla. Jokaisessa tilanteessa on vaihteleva protokolla, että versioiden välillä tapahtuu tyyppilinen tila kuten:

- Blocking (estetty): Porttien on oltava rooliltaan nondesignated, mitä ei osallistu datanvälitykseen STP ympäristössä. Portti vastaanottaa BPDU frame määrittäkseen root-kytkimen sijainnin ja root ID:n eli siltatunnus (bridge ID), että sen roolien kytkimen porttien tulee omaksua lopullisessa STP:n aktiivisessa topologiassa. Oletuksena portti pysyy tilassa n. 20 sekunttia (max age).
- Listening (kuunteleva): STP määritetyissä ympäristössä, että portti voi osallistua datavälityksiin. Kytkin vastaanottaa ja välittää BPDU frame:ja eteenpäin tiedotakseen viereisille kytkimille, että sen portti valmistautuu osallistumaan STP:n aktiviisiin topologiaan välittämään dataliikennettä. Oletuksena portti pysyy n. 15 sekuntia (forward delay).
- Learning (oppiva): Portti valmistautuu välittämään data frame:iä ja tallentaa MAC-osoitteita CAM-taulukkoon, että oletus portti pysyy tilassa n. 15 sekuntia (forward delay).
- Forwarding (välittävä/edelleenlähetävä): Porttin tilanne on osa STP:n aktiivista topologiaa, että välittää dataliikennettä, sekä lähettää ja vastaanottaa BPDU frame:ja.
- Disabled (suljettu): Suljettu tila, mitä ei osallistu STP:n topologiaan, eikä välitä dataa tai BPDU frame:ja.

![Alt text](image/STP-Switch1.PNG?raw=true "None") <br>

![Alt text](image/STP-Switch2.PNG?raw=true "None") <br>

<h2>STP Root Bridge </h2>

Edellisen kuvassa on <ins> "Bridge ID" </ins> , ja sen prioriteetti / etusijaan on 32 769, mikä on Cisco System järjestelmän oletus prioriteetti luku, että pienin voitto luku. Jos prioriteettitaso on tasainen luku, alinta MAC-osoitetta käytetään katkaisijana. <ins> Root Bridge </ins>, mikä tarkoittaa kuin Suomeksi <ins> "juurisilta" </ins>. Juurisilta valitsee 'Bridge-id' perusteella, mikä on kaksiosainen luku. Ensimmmäinen osa, mikä on merkitsevämpi osa, mitä määritetään konfiguraatiossa, ja se on 4096 kertaluku kertoimella 0 - 16. Toisen osan muodostuu kytkimen kanta MAC-osoite, että ensimmäisenä osan oletusarvo on 32 769 eli kerroinluku 8 (4096 * 8). Juurisilta valitaan se kytkin, millä on pienin bridge-id. Kytkinverkossa kytkeytyy verkkokaapelit, mitä kutsutaan <b>Port Path Cost</b> -arvoa, mitä määräytyy oletus linkin nopeuden, ja portin numeron mukaan. <br>
<br>

Prioriteetti lukua laskettaan bitteinä, että se on 16-Bittinen, ja perus laskutapa menee binäärinä eli 1011001. 

![Alt text](configurations/images/Bridge-PriorityValues.PNG?raw=true "None") 

Jokaisen spanning tree ympäristöön osallistuu kytkin, mitä saa <b> 'Root Path Cost'</b> -arvon, mikä määrittää lyhyimmän etäisyyden juurisillan. <ins> Root Path Cost -arvo </ins> on juurisillan ja kytkimen portin välisten <ins> 'Port Path Cost' -arvojen </ins> summa, eli kytkin portti x (Port Path Cost) --------- (Root Path Cost) kytkin portti y). Jos sattuu useita kytkimen portteja osallistuu spanning tree ympäristöön, mitä vaitaan kytkimen <ins> 'Root Path Cost' -arvoksi </ins> pienin arvo, ja valitaan sen arvon omistava kytkinportti juurisillaksi. Loput portit ovat joko redudanttisia porttoje tai osa muut ovat kytkimen juuriportin vastaporttoja. Myös edelllisen kuvan kytkimen portti 'cost'- arvo on 128, mikä koostuu kytkennästä, että konfiguroitavast portin prioriteetti (port priority) - arvosta, ja portin numerosta, siksi ensimmäisen portin portti-ID on 128.1, 128.2 ja jne. Jos kaksi yhteyttä on yhtä nopeita eli sama reitin 'cost', mitä root-port valitaan se portti, jolla on pinein portti-ID-luku. <br>

Varajuuri (root secondary), mitä kuin korvaisi pakotettun <ins> pää juurisillan </ins> (root primary). Root secondary tarkoittaa Suomeksi varajuuri. Konfigurointi toimii kuin pakotetut juurisilta, mutta tunnistamisesta ei ole. Kun pää pakotettu juurisilta porttista sammuu, mitä vara juurisilta käynnistyy samantien. Myös pakotetun juurisilta ja vara juuressa muutoksessa, mitä tapahtuu prioriteetin luvun muutos, koska oletuksena kytkimen määritämätön juurisilta oletuksena on 32 769. Luvun muutoksessa tapahtuu komenolla $show spanning-tree, että kohda <ins>Root ID</ins> & <ins>Bridge ID</ins> kohteen prioriteetti luku. <br>

<h2>Kytkimien porttien host luku</h2>

![Alt text](image/STP-defaultPortCost.PNG?raw=true "None") 
![Alt text](image/STP-LinkPortCost.PNG?raw=true "None") <br>

<h2>BPDU</h2>

<b> Bridge protocol data unit </b>, mikä on kuin kehys ja tarkoitta siltaprotokollan tietoyksikkö, mitä sisältävät tietoja STP protokollossa. Kytkin lähettää BPDU käyttämällä ainulaatuisen lähteen MAC-osoitteen, että sen alkuperäisen portti on mutlicast osoitteen määränpäähän on MAC. BÅDU:t lähetetään oletusarvoisen n. 2 sekunnin välein. Konfigurointi BPDU, lähettää juurisillan antaman tietoja kaikille kytkimille. Myös BPDU on kolmen tyyppistä:
- Kokoonpanossa, mitä käytetään kattavan puun laskemiseen
- Topologian muutosilmoitus (TCN), mitä käytetään topologiamuutosten ilmoittamista
- Topologian ilmoituksen muutoksen kuittaus.

<br> BPDU lähetetään ryhmä oletusosoitteeseen malliltaan : 01: 80: C2: 00: 00: 00 tai 01:00:0C:CC:CC:CD

# Spanning tree mode

Tämä on sisäisen Cisco Packet Tracer virtuaaliohjelmiston sisäisen kokoonpano STP määritys, mutta todellisuudessa voi olla useampi. Myös protokollasta on julkaistu useita eri versioita, että osa IEEE - komitaen standardoitu, ja toimivat siten muidenkin kuten Cisco System järjestelmän valmistama kytkimet. Osassa kuten PVST+ (per vlan spanning tree plus) ja PVRST+ (per vlan rapid spanning tree plus), ovat Cisco omistusoikeuden julkaisui, ja toimivat siten vain Ciscon oman valmistama kytkimessä. Näiden eri versioissa on kehitty vastaamaan useisiin spanning tree tarpeisiin, että nopeampaan konvegenssiaikaan tai parempaan dataliikenteen ohjauksen verkoon.
![Alt text](image/STP-modes.PNG?raw=true "None") <br>

- <b>PVST+ </b> Per-Vlan spanning tree plus moodi, mikä on Cisco kehittämä parannus IEEE 802.1D STP:n ympäristöön, ja se on Cisco kytkimien oletus spanning-tree versio. Tätä voidaan luoda yhden virittävän spanning tree esiintymän VLAN:in kohteen.  <br>

- <b>Rapid PVST </b> Per-Vlan rapid spanning tree moodi tai toinen lyhenne <b> RSTP </b>, mikä on Ciscon patentoitu parannus IEEE 802.1w RSTP:hen. PVST, mitä sen avulla voi luoda yhden kattava spanning tree esintymän VLAN:in kohteen. Verkon konvergenssi on myös nopeampaa RPVST+:n avulla. Rapid PVST, mitä kuin havaitsee vian nopeasti kuin tavallinen STP protokolla, että koneiden pinggauksessa tulostuu vähemmän tai ei ollenkaan (request time out).

# Spanning tree algorithm

![Alt text](image/STP-defaultPortCost.PNG?raw=true "None") <br>


# STP ohjeet, konfiguraatiot & muu opas:

<!-- https://www.youtube.com/watch?v=7myQEhqtaUc
 <br>
<br>
-->
https://www.cisco.com/c/en/us/support/docs/lan-switching/spanning-tree-protocol/5234-5.html <br>
https://www.cisco.com/c/en/us/tech/lan-switching/spanning-tree-protocol/index.html <br>
https://www.cisco.com/c/en/us/support/docs/smb/switches/cisco-small-business-300-series-managed-switches/smb5760-configure-stp-settings-on-a-switch-through-the-cli.html <br>
https://www.cisco.com/c/en/us/support/docs/lan-switching/spanning-tree-protocol/28943-170.html <br>
http://docs.ruckuswireless.com/fastiron/08.0.60/fastiron-08060-l2guide/GUID-F9905D20-F2BB-4286-B606-49BC36596CF1.html <br>
https://ipcisco.com/lesson/pvst-and-rapid-pvst-configuration-on-packet-tracer/ <br>
https://www.firewall.cx/networking-topics/protocols/spanning-tree-protocol/1054-spanning-tree-protocol-root-bridge-election.html <br>
https://www.9tut.com/spanning-tree-protocol-stp-tutorial <br>
https://www.ccnablog.com/stp-part-i/ <br>

