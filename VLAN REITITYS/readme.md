<h1>VLAN reititys</h1>

Vitual LAN, toimii kuin ryhmä pääteasema, mitä usein konfiguroituu usein kytkimeen ja reitittimeen, että kytketyissä verkossa, sekä loogisen segmentoitu toiminnon tai sovelluksen mukaisen riippumien käyttäjien fyysisestä sijainnista. VLAN:illa on samat attribuutit kuin fyysisellä LAN-verkoilla, mitä voi ryhmitää pääteasemat ja ne eivät fyysisesti sijaitsisi samassa LAN-verkon segmentissä.

Mikäkin kytkinportti voi kuljettaa VLAN:ia, unicast-, broadcast ja multicast pakettia välittäen ja tulvittaa vain kyseisen VLAN pääteasemia. Jokaista VLAN-verkkoa pidetään loogisena verkkona, ja paketit, mitä on tarkoitettu asemille ja eivät kuuluu VLAN:iin, ja on välitettävä reitittimen kautta.

VLAN verkossa liitetään yleensä IP-aliverkko (255.255.255.0), ja esim kaikkissa tietyn IP-aliverkon pääteasemat kuuluvat samaan VLAN:iin. Myös kommunikoinissa VLAN-verkkojen välillä, mitä tapahtuu reitittävä liikkenne.

## Default vlan

default eli oletus, yleensä cisco kytkimien laiteessa on oletuksena valmiiksi oletus vlan num. 1, mikäli jos tulee useita vlan-id:tä niin kantsii luoda erillinen vlan-id numero ja nimeäminen esim. VLAN 4 - hallitus.

## access & trunk

kytkimissä usein määritellään access tai trunk moodia.
access - moodi tarkoittaa, että määritettään yksittäinen portti, jossa suoriuttuu oma vlan id (palvelin), jotka kommunikoi keskennään
trunk - moodi tarkoittaa, että voidaan kuljettaa useita vlan id:tä, että kaksi tai useampi kytkin kommunikoin toisiinsa

# Inter VLAN

![Alt text](InterVLAN.PNG?raw=true "None")

<hr>

# Multilayer Switch Inter-VLAN Routing

![Alt text](VLAN-inter-Multilayer.PNG?raw=true "None")

# Multilayer Switch L3 - voi konfiguroida
<ul>
  <li>VLAN</li>
    <dd>VLAN id + oma ip-osoite & mask </dd>
  <li>Port mode</li>
    <dd>access & trunk + encapsulation dot1Q </dd>
  <li>DHCP</li>
    <dd></dd>
</ul>

# Multilayer Switch vs Router
<br>
<b> Reititintä  </b> tunnetaan parhaiten, että välittää tietoja tietoverkon eri osien väliltä. Reitittiemn muodostamisessa usein tapahtuu monipuolisia topologiaa, että esim.  tähti muotoinen topologia reititys. Reitittimen tehtävänä on välitää viestin, että vastaanottaja saa viestin lähettäjältä. 

Myös reitittimen sisällä tapahtuu reititysprotokolla, että tapahtuu reititys protokolla kuten ryhmittää reittei tai aleuita, määrittää pääsyn reitityksen, ja sekä hallinan etäisyyttä. 
<br><br>
<b>Multilayer switch (MLS) </b>, on tietokone verkkolaite, mikä on OSI-mallin toinen kerros (2-layer) ja tavallisen verkkokytkin, ja sisällä tarjoaa lisää toimintoja korkeammille OSI-kerroksille.
<br>
Parhaiten tunnettaan nimellä L3 kytkin, ja hybridilaite, mitä yhdistää kytkimen ja reitittimen (combo). Fyysisen näkökulmasta monikerroksien kytkin ovat identtisiä tavallisen kytkimen kanssa, että on 24 tai 48 verkko Ethernet porttia ja osa SFP-ready porttia. Myös voi pinota kuten L2 kytkin, ja ero on laatikon sisällä, että laitteisto ja ohjelmisto. <br><br>

- Jos multilayer kytkin L3 ovat nopeampi kuin reitittimet, ja erona on monikerroksinen kytkin ja reitittimen välillä. <br>
Multilayer kytkin L3:ssa on hyviä puolia, mitä niiden TCAM (ternary Content-addressable Memory) on suunniteltu toimimaan Ethernet:in kanssa, että vain kupari- ja kuitukaapeli. Reititin sijaan voi toimia useiden eri tekniikoiden kanssa, ja tukee erilaisia rajapintoja. Reitittimessä voi lisätä jotain liitäntöjä asettamalla sopivan moduulin, että tätä ei ole multilayer kytkimen ominaisuudessa.

Reitittimessä on monipuolisia toimintoja, että ne tukevat monia erilaisisa reititysprotokollia, hienosäätöä ja mukautuksia. Koska multilayer kytkin, mitä yrittävätä tehdä kaiken voittakseen tavallisen reitittimen laitteiston siällä, että niiden kokoonpanossa ei voi olla tätä tarkkuutta, ja ne tarjoavat rajoitetun joukon ominaisuutta. Myös nämä ominaisuudet voi olla hyviä useimmissa käyttötarkoituksissa, mutta on jotain asioita, mitä L3 kytkin ei yksinkertaisesti pysty tekemään.

https://www.ictshore.com/free-ccna-course/inter-vlan-routing-multilayer-switch/

![Alt text](Multilayer-Switch-DHCP-VLANs.PNG?raw=true "None")

# konffaus staatinen reititys ohje:
https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus9000/sw/7-x/unicast/configuration/guide/b_Cisco_Nexus_9000_Series_NX-OS_Unicast_Routing_Configuration_Guide_7x/b_Cisco_Nexus_9000_Series_NX-OS_Unicast_Routing_Configuration_Guide_7x_chapter_01101.pdf <br>
