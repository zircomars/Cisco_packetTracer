# VTP (Vlan trunk protocol) & DTP (Dynamic trunk protocol)

# DTP (Dynamic trunking protocol)

<h2>DTP interfaces mode taulukko</h2>

![Alt text](image/DTP-InterfaceModes.PNG?raw=true "None") <br>


# VTP (VLAN Trunk Protocol)

Tämän protokollan ominaisuus tapahtuu kytkimissä, kun niitä kytkeytyy useisiin kytkimiin, että lähettää data paketin viestin eteenpäin, ja myös siirtää VLAN id viestiä. 
VTP protokolan VLAN:ssa levitää lähiverkkojen määritelmän koko lähiverkon, että VTP toimialueen kytkimessä. VTP rakenteeltaan on esim. pitkä jana tai kuin sukujuuri muotoinen puu rakenne.

<br>

![Alt text](image/VTP-map1.png?raw=true "None") <br>

![Alt text](image/VTP-map2.png?raw=true "None") <br>

# VTP switch mode
VTP kytkimien moodeja on:
- server : mitä voi luoda, muokata ja poistaa VLAN-verkkoja, ja määrittää muita kokoonpano parametrejä, kuten VTP-versio ja VTP-karsinnat, että koko VTP-toimialueet <br>
- client : asiakas, mitä kuin toimivat samalla kuin server, mutta ei voi luoda, muuttaa tai poistaa VLAN-verkkoja VTP-asiakkaassa. <br>
- transparent : VTP transparent kytkimesssä eivät osallistu VTP:hen. VTP transparent kytkin ei mainosta VLAN kokoonpanoa, eikä synkronoi VLAN kokoonpanoaan vastaanotetujen mainosten perusteella, mutta transparent kytkimet välittävät VTP mainoksia, että ne vastaanottavat trunk porttia VTP-versiossa 2.
