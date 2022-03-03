# STP konfigurointi ja muu vianmääritys komennot

Tarkista kytkimen porttien kaistanleveys menee, että siellä näkyy BW (bandwidth) Kbit: $show int fa0/X
komennot: <br>
$show spanning-tree vlan 1 (oletus vlan 1) <br>
TAI <br>
$sh sp vlan 1 <br>

$show spanning-tree detail <br>
TAI <br>
$sh sp detail <br>
<br>
$sh spanning-tree<br><br>

PVST tarkistus taustan komennot:<br>
Tämä tarkistaa STP protokollan yhteenvedon, että onko PVST vai RVST (Rapid-STP)
$show spanning-tree summary<br>

$show spanning-tree active<br>

# Kytkimen juuri konfigurointi & STP prioriteetti luku

Root primary - tarkoittaa pakotetu juuri & root secondary - tarkoittaa vara-juurikytkin <br> & kytkimien STP prioriteetti oletus luku on 32 769. Luvun methodin mukaan, että pienin on se voitto, joka kuin muodostuu se pakotettu juuri "root bidge". Yleensä verkonvalvoja vaikuttaa vaalien tulokseen siten, että valittu pääkytkin on mahdollisimman lähellä ydinverkkoa. Se tekee tämän määrittämällä sopivimman juurikytkimen prioriteetin verkon topologian mukaan, samoin kuin toisen kytkimen prioriteetin, josta tulee juurikytkin, jos ensisijainen juurikytkin epäonnistuu.

Kytkimien juurien konffaus: <br>
- Pakotetu juuri <br>
$spanning-tree VLAN 1 root primary <br>

- jos on useampi VLAN mukana esim. 1-4 <br>
$spanning-tree VLAN 1-4 root primary <br>

- tämä on kytkimen prioriteeti asetama ennaltaan määritetty arvo 24 576, että kertomalla alin luku 4096 (4096 * 6), myös joka on pienempi kuin verkossa havaittu alin silta prioriteetti <br>
$spanning-tree VLAN 1 priority 24576 <br>

- Vara juurin luominen <br>
$spanning-tree VLAN 1 root secondary <br>

- jos on useampi VLAN mukana esim. 1-4 <br>
$spanning-tree VLAN 1-4 root secondary <br>

# PVST konfigurointi

PVST on Cisco teknisen oman protokolla, mitä voi konfiguroida STP ympäristöön. Cisco laite voi toimia yhdessä muiden PVST laitteiden virittävien stp kansa, mutta se ei toimi IEEE 802.1Q-laitteiden kanssa. IEEE 802.1Q -laitteen kaikki portit käyttävät yhtä kattavaa STP. PVST+ on PVST:n laajennus, jonka avulla Cisco-laitteet voivat toimia myös yhteen virittävää puuta (IEEE 802.1Q) käyttävien laitteiden kanssa.

Parannettu PVST+-tuki mahdollistaa Ruckus-laitteen yhteentoimivuuden PVST-virittävän puiden ja IEEE 802.1Q -virittävän puun kanssa samanaikaisesti.

