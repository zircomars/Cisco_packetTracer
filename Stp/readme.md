# STP (spanning tree protocol)

Tarkoittaa, että esim. kolme tai useampi kytkintä (switch), kulkeutuu sellainen kolmilo näköinen muoto, jos yksi niistä portista on poikki, niin viesti kulkeutuu toisesta reitistä, mutta portti pitää vastaanottaa se ja lähettää viestin eteenpäin omasta kytkimen portista. <br>

Kytketty ympäristö, joka eroaa siltaympäristöstä, mitä käsittelee useita VLAN-verkkoja. Kun otat käyttöön pakotetun juurin kytkentäverkossa, käytät yleensä juurisiltaa juurikytkimenä. Jokaisella VLANilla on oltava oma juurisilta, koska jokainen VLAN on erillinen lähetysalue. Kaikkien eri VLAN-verkkojen juuret voivat sijaita yhdessä kytkimessä tai useissa kytkimissä. Jos yhtäkkiä yhteys katkee, mitä viesti kulkeutuu toisesta reitistä, koska jotta STP ympäristössä tapahtuu reititys, jotta se pääsisi perille asti.
<br><br>
switch1 ----- switch2 ------ switch3 ---- switch1  <br>

esim switch2 ja switch3 välinen yhteys on poikki, niin viesti kulkeutuu kohti switch1:stä kohti switch3:lle, mutta kulkeutumisen välisen yhteys pitää olla trunk moodi.
<br>
![Alt text](image/STP-topology1.PNG?raw=true "None") <br>

![Alt text](image/STP-topology2.PNG?raw=true "None") <br>

# Kytkimen porttien roolit ja asemat

Kytkimien porttissa tapahtuu rooli STP ympäristössä, kun kytkeytyy ristikytkentä. Koska suorakytkentä, mitä kuin toimii ristikytkentä, mutta sisäisen fyysisen kaapeli asennettu erilaisena. Eri porttien rooleja tapahtuu spanning tree hallintoi verkojen topologiassa ja redudanttisia yhteyksiä, että välityssilmukka ei pääse muodostumaan. Spanning tree porttien rooleja on kuten:

- Root - portti: mitä sijaitsee muissa kytkimissä, ja nopeis reitti root kytkimille. Root portti, mitä välittää dataliikennettä kohti muihin root-kytkimiin, ja saapuvista root-portti data framien lähettäjälaitteen MAC-osoite voidaan tallentaa MAC-taulukkoon. Jokaisessa kytkimessä voi olla vain yksi root-portti.
- Designated - portti: tämä porttin rooli, mitä voi olla sekä root tai muissa kytkimissä. Root kytkimien kaikki portti ovat designated portteja. Koska designated-portit vastaanottavat ja välittävät dataliikennettä kohti root-kytkentään, ja vain yksi designated-portti voi olla verkkosegmentti kohde. Saapuvien data framien lähttäjien MAC-osoite voidaan tallentaa MAC-taulukkoon.
- Nondesignated - portti: Mikä on kuin "ei designoitu), mitä ei välitä dataliikennettä eli kuin estetty (blocking) portti. Saapuvien porttien data frame lähettäjien MAC-osoitetta ei tallenna MAC-taulukkoon.
- Disabled portti: mitä tarkoittaa suljettu portti.
<br>
Myös jokaisessa portissa on roolien tilanne tai aseman taustat, että datan välitäessä tai estetyissä tilassa, ja spanning tree:n muodstaman loogisen topologia protokolla. Jokaisessa tilanteessa on vaihteleva protokolla, että versioiden välillä tapahtuu tyyppilinen tila kuten:

- Blocking (estetty): Porttien on oltava rooliltaan nondesignated, mitä ei osallistu datanvälitykseen STP ympäristössä. Portti vastaanottaa BPDU frame määrittäkseen root-kytkimen sijainnin ja root ID:n eli siltatunnus (bridge ID), että sen roolien kytkimen porttien tulee omaksua lopullisessa STP:n aktiivisessa topologiassa. Oletuksena portti pysyy tilassa n. 20 sekunttia (max age).
- Listening (kuunteleva): STP määritetyissä ympäristössä, että portti voi osallistua datavälityksiin. Kytkin vastaanottaa ja välittää BPDU frame:ja eteenpäin tiedotakseen viereisille kytkimille, että sen portti valmistautuu osallistumaan STP:n aktiviisiin topologiaan välittämään dataliikennettä. Oletuksena portti pysyy n. 15 sekuntia (forward delay).
- Learning (oppiva): Portti valmistautuu välittämään data frame:iä ja tallentaa MAC-osoitteita CAM-taulukkoon, että oletus portti pysyy tilassa n. 15 sekuntia (forward delay).
- Forwarding (välittävä/edelleenlähetävä): Porttin tilanne on osa STP:n aktiivista topologiaa, että välittää dataliikennettä, sekä lähettää ja vastaanottaa BPDU frame:ja.
- Disabled (suljettu): Suljettu tila, mitä ei osallistu STP:n topologiaan, eikä välitä dataa tai BPDU frame:ja.

<h2>BPDU</h2>

<b> Bridge protocol data unit </b>, mikä on kuin kehys ja tarkoitta siltaprotokollan tietoyksikkö, mitä sisältävät tietoja STP protokollossa. Kytkin lähettää BPDU käyttämällä ainulaatuisen lähteen MAC-osoitteen, että sen alkuperäisen portti on mutlicast osoitteen määränpäähän on MAC. BÅDU:t lähetetään oletusarvoisen n. 2 sekunnin välein. Konfigurointi BPDU, lähettää juurisillan antaman tietoja kaikille kytkimille. Myös BPDU on kolmen tyyppistä:
- Kokoonpanossa, mitä käytetään kattavan puun laskemiseen
- Topologian muutosilmoitus (TCN), mitä käytetään topologiamuutosten ilmoittamista
- Topologian ilmoituksen muutoksen kuittaus.

<br> BPDU lähetetään ryhmä oletusosoitteeseen malliltaan : 01: 80: C2: 00: 00: 00 tai 01:00:0C:CC:CC:CD

# STP ohjeet, konfiguraatiot & muu opas:
https://www.cisco.com/c/en/us/support/docs/lan-switching/spanning-tree-protocol/5234-5.html <br>
https://www.cisco.com/c/en/us/tech/lan-switching/spanning-tree-protocol/index.html <br>
https://www.cisco.com/c/en/us/support/docs/smb/switches/cisco-small-business-300-series-managed-switches/smb5760-configure-stp-settings-on-a-switch-through-the-cli.html <br>
https://www.cisco.com/c/en/us/support/docs/lan-switching/spanning-tree-protocol/28943-170.html <br>
