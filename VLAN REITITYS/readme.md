<h1>VLAN reititys</h1>

Vitual LAN, toimii kuin ryhmä pääteasema, mitä usein konfiguroituu usein kytkimeen ja reitittimeen, että kytketyissä verkossa, sekä loogisen segmentoitu toiminnon tai sovelluksen mukaisen riippumien käyttäjien fyysisestä sijainnista. VLAN:illa on samat attribuutit kuin fyysisellä LAN-verkoilla, mitä voi ryhmitää pääteasemat ja ne eivät fyysisesti sijaitsisi samassa LAN-verkon segmentissä.

Mikäkin kytkinportti voi kuljettaa VLAN:ia, unicast-, broadcast ja multicast pakettia välittäen ja tulvittaa vain kyseisen VLAN pääteasemia. Jokaista VLAN-verkkoa pidetään loogisena verkkona, ja paketit, mitä on tarkoitettu asemille ja eivät kuuluu VLAN:iin, ja on välitettävä reitittimen kautta.

VLAN verkossa liitetään yleensä IP-aliverkko (255.255.255.0), ja esim kaikkissa tietyn IP-aliverkon pääteasemat kuuluvat samaan VLAN:iin. Myös kommunikoinissa VLAN-verkkojen välillä, mitä tapahtuu reitittävä liikkenne.


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

![Alt text](Multilayer-Switch-DHCP-VLANs.PNG?raw=true "None")
