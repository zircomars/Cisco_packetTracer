# STP (spanning tree protocol)

Tarkoittaa, että esim. kolme tai useampi kytkintä (switch), kulkeutuu sellainen kolmilo näköinen muoto, jos yksi niistä portista on poikki, niin viesti kulkeutuu toisesta reitistä, mutta portti pitää vastaanottaa se ja lähettää viestin eteenpäin omasta kytkimen portista. <br>

Kytketty ympäristö, joka eroaa siltaympäristöstä, mitä käsittelee useita VLAN-verkkoja. Kun otat käyttöön pakotetun juurin kytkentäverkossa, käytät yleensä juurisiltaa juurikytkimenä. Jokaisella VLANilla on oltava oma juurisilta, koska jokainen VLAN on erillinen lähetysalue. Kaikkien eri VLAN-verkkojen juuret voivat sijaita yhdessä kytkimessä tai useissa kytkimissä. Jos yhtäkkiä yhteys katkee, mitä viesti kulkeutuu toisesta reitistä, koska jotta STP ympäristössä tapahtuu reititys, jotta se pääsisi perille asti.
<br><br>
switch1 ----- switch2 ------ switch3 ---- switch1  <br>

esim switch2 ja switch3 välinen yhteys on poikki, niin viesti kulkeutuu kohti switch1:stä kohti switch3:lle, mutta kulkeutumisen välisen yhteys pitää olla trunk moodi.
<br>
![Alt text](image/STP-topology1.PNG?raw=true "None") <br>

![Alt text](image/STP-topology2.PNG?raw=true "None") <br>


# STP ohjeet, konfiguraatiot & muu opas:
https://www.cisco.com/c/en/us/support/docs/lan-switching/spanning-tree-protocol/5234-5.html <br>
https://www.cisco.com/c/en/us/tech/lan-switching/spanning-tree-protocol/index.html <br>
https://www.cisco.com/c/en/us/support/docs/smb/switches/cisco-small-business-300-series-managed-switches/smb5760-configure-stp-settings-on-a-switch-through-the-cli.html <br>
https://www.cisco.com/c/en/us/support/docs/lan-switching/spanning-tree-protocol/28943-170.html <br>
