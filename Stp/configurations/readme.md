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
Tämä tarkistaa STP protokollan yhteenvedon, että onko PVST vai RVST (Rapid-STP) <br>
$show spanning-tree summary<br>

$show spanning-tree active<br>

# Kytkimen juuri konfigurointi & STP prioriteetti luku

<ins>Root primary</ins> ja <ins> root bridge</ins>, mitä tarkoittaa samaa ja suomeksi "pakotettu juuri" tai "Pää juuri". <ins>root secondary</ins> tarkoittaa varajuuri, mitä kuin pakotettu juuri ei käynnisty tai kohteen kytkimen portti ei aktivoidu, mitä vara juuri korvaisi pakotetun juuren. Varajuuri, mitä pitää kuin olla pää juurin kytkimen vieressä tai kytkeytyy lähistöllä, jotta saa koneen viestin perille kohti vastaanottajaan. (kytkin "pakotettu juuri" & portti fa0/x ---------kaapeli----------- fa0/y "varajuuri" kytkin) & kytkimien STP prioriteetti oletus luku on 32 769. 

Luvun methodin mukaan, että pienin on se voitto, joka kuin muodostuu se pakotettu juuri "root bidge". Yleensä verkonvalvoja vaikuttaa vaalien tulokseen siten, että valittu pääkytkin on mahdollisimman lähellä ydinverkkoa. Se tekee tämän määrittämällä sopivimman juurikytkimen prioriteetin verkon topologian mukaan, samoin kuin toisen kytkimen prioriteetin, josta tulee juurikytkin, jos ensisijainen juurikytkin epäonnistuu.

Pakotetun juuri "root bridge" ja varajuuri "secondary bridge", mitä voidaan konfiguroida PVST ja Rapid-PVST ympäristössä. Myös konfiguroinnissa pää- ja varajuuri ei estä PVST ja Rapid-PVST sisäisen STP järjestelmää.

![Alt text](images/STP-Switch-RootPrimSec.PNG?raw=true)
<pre>
Kytkimien juurien konffaus: <br>
- Pakotetu juuri <br>
$spanning-tree VLAN 1 root primary <br>

- jos on useampi VLAN mukana esim. 1-4 <br>
$spanning-tree VLAN 1-4 root primary <br>

- Vara juurin luominen <br>
$spanning-tree VLAN 1 root secondary <br>

- jos on useampi VLAN mukana esim. 1-4 <br>
$spanning-tree VLAN 1-4 root secondary <br>
</pre>
<h2> STP prioriteetti luku </h2>

- tämä on kytkimen prioriteeti asetama ennaltaan määritetty arvo 24 576, että kertomalla alin luku 4096 (4096 * 6), myös joka on pienempi kuin verkossa havaittu alin silta prioriteetti. Sama homam tämä on bitteinä laskettu eli 0101011 ja jne. Kuva-taulukosta voi tarkasteslla..<br>
$spanning-tree VLAN 1 priority 24576 <br>

STP konfigurointi ympäristössä usein alkulähdön kytkimien porttien yhdistämisessä tapahtuu oletuksena prioriteetin luvun 32 769, että pakotettu juuri tulostuu / aktivoituu samantien. Jos luoo <ins>uudelle </ins> kytkimelle <ins> pakotettu juuri </ins> , mitä tapahtuu uusi prioriteeti luku n. +- 24 577 - 24 596 rajan sisältä, tai jopoa luvultaan +- 28 673 alueella. Komennolla $show spanning-tree , mitä tapahtuu muutos STP protokollan Root ID ja Bridge ID ominaisuuden / teknisen tiedon prioriteetin kohdalla.

![Alt text](images/Bridge-PriorityValues.PNG?raw=true)

![Alt text](images/BridgeId-12Bit.PNG?raw=true)

# PVST & Rapid-PVST mode

![Alt text](images/STP-Switch-ModeTypeAddVlans.PNG?raw=true)

<h2> PVST konfigurointi (mode) </h2>

PVST on Cisco teknisen oman protokolla, mitä voi konfiguroida STP ympäristöön. Cisco laite voi toimia yhdessä muiden PVST laitteiden virittävien stp kansa, mutta se ei toimi IEEE 802.1Q-laitteiden kanssa. IEEE 802.1Q -laitteen kaikki portit käyttävät yhtä kattavaa STP. PVST+ on PVST:n laajennus, jonka avulla Cisco-laitteet voivat toimia myös yhteen virittävää puuta (IEEE 802.1Q) käyttävien laitteiden kanssa.

Parannettu PVST+ tuki mahdollistaa Ruckus-laitteen yhteentoimivuuden PVST-virittävän puiden ja IEEE 802.1Q -virittävän puun kanssa samanaikaisesti.

Kuvassa tapahtuu, että mikä kytkin moodia valitaan, että konfiguroinnissa tapahtuu kytkimen sisäisen VLAN:it, mitäkin on muakana, jos sattuu iso tia pieni organisaatio. VLAN 1- 20, mitä tarkoittaa sen rajan, että on tällainen määrä projektissa.

<h2>  Rapid PVST konfigurointi (mode) </h2>

Rapid PVST+ -protokolla on IEEE 802.1w -standardi, Rapid Spanning Tree Protocol (RSTP), joka toteutetaan VLAN-kohtaisesti. Rapid PVST+ toimii yhdessä IEEE 802.1D -standardin kanssa, joka edellyttää yhden STP-ilmentymän kaikille VLAN-verkoille VLANin sijaan. Rapid PVST+ on oletusarvoisesti käytössä oletus-VLAN-verkossa (VLAN1) ja kaikissa ohjelmiston äskettäin luoduissa VLAN-verkoissa. Rapid PVST+ toimii yhdessä kytkimien kanssa, jotka käyttävät vanhaa IEEE 802.1D STP:tä. Myös Rapid PVST konfiguroinnissa on kaksi tyypistä linkkiä, että on <ins>point-to-point</ins> & <ins>shared</ins>

RAPID-PVST, mikä kuin havaitsee vian nopeasti kuin tavallinen spanning-tree protokolla, eli yrittää saada pinggauksen virhe pois nopeammin, että vähemmän (request time out). Myös tuloksena voi olla pari kadonnutta pakettia, tai ei yhtään.

Konfiguroinnin kohdalla tapahtuu, että kytkimen porttista tulee olemaan <ins>"point-to-point"</ins>, mitä kytkeytyy kohti seuraavaan kytkimelle. Point-to-point, mikä tehtävänä on virittää STP protokollan konvergenssin aikaansaamista. Jos yhdistät portin toiseen porttiin <ins> point-to-point </ins>-linkin kautta ja paikallisesta portista tulee nimetty portti, se neuvottelee nopeasta siirtymisestä toisen portin kanssa käyttämällä ehdotus-sopimuskättelyä varmistaakseen silmukaton topologia.

Rapid PVST+ saavuttaa nopean siirtymisen edelleen lähetystilaan vain reuna orteissa ja point-to-point -linkeissä. Vaikka linkin tyyppi on konfiguroitavissa, järjestelmä johtaa automaattisesti linkin tyyppitiedot portin duplex-asetuksista. Full-duplex-porttien oletetaan olevan point-to-point-portteja, kun taas half-duplex-porttien oletetaan olevan jaettuja portteja. 

<pre>
<br> Esimerkki kytkimen konfigurointi: <br>
Switch(config)#spanning-tree mode ? <br>
  pvst        Per-Vlan spanning tree mode <br>
  rapid-pvst  Per-Vlan rapid spanning tree mode <br> <br>
Switch(config)#spanning-tree mode rapid-pvst  <br>
Switch(config)#int fa0/1  <br>
Switch(config-if-range)#spanning-tree link-type ? <br>
  point-to-point    Consider the interface as point-to-point <br>
  shared            Consider the interface as shared <br>
Switch(config-if)#spanning-tree link-type point-to-point  <br>
<br>
<ins>Shared</ins> - mikä on, Half-duplex-tilassa toimiva portti yhdistää kytkimen vanha keskitin, joka liittää useita laitteita.

</pre>

# Configuraatio Before - After

<h2>Harjoitus vers. 1 - Uusi pakotettu juuri & muu kytkin tilanne (1)</h2>

![Alt text](images/STP-OldAndNew.png?raw=true)

![Alt text](images/STP-OldAndNew_otherSwitch.PNG?raw=true)

<hr>

<h2>Harjoitus vers. 2 - Uusi pakotettu juuri & muu kytkin tilanne (2)</h2>

![Alt text](images/STP-Secondary-Before.png?raw=true)

![Alt text](images/STP-Secondary-BeforeAfter.png?raw=true)

<h2> Harjoitus vers. 2 - pinggaus ja monta pakettia on kadonnut </h2>

![Alt text](images/STP-Secondary-test1.PNG?raw=true)

![Alt text](images/STP-Secondary-test2.PNG?raw=true)

