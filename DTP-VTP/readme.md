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
