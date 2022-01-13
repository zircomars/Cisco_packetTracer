<h1>DHCP snooping 13.1.2022 </h1>

<ul>
<li> DHCP snooping - mikä on tietoverkon käytettävä suojaus tekniikka, mitä käytetään parantamassa turvallisuutta DHCP infrastruktuurissa </li>

<li> Infrastruktuuri tarkoittaa palveluista ja rakenteesta, että mahdollista muodostaa yhteiskunnan tominnan. Myös sisältyen muita kokoonpanoi ja teknisiä asioita </li>

<li> DHCP itse toimii OSI-kerroksen tasolla 3, kun taas DHCP-snooping toimii kerroksen 2 laitteissa suodattaakseen DHCP-asiakkailta tulevaa liikennettä. </li>

<li>DHCP - protokollan palvelinta on tärkeää jokaisessa organisaation verkossa, koska useissa käyttäjä laitteet eli fyysiset ja langattomat tietokoneet, mitä käyttävät DHCP protokollaa IP-osoitetta automaatisesti. </li>
  
<li>Verko isäntä luo DHCP protokollan, jotta verkon käyttäjät voi käyttää määritettyä IP-osoitetta</li>
  
</ul>

<hr>
<h2>DHCP snooping ARP</h2>

<ul> 
  <li>DHCP määritys, mitä tehtävänä on jakaa fyysisen tietokone käyttäjille IP-osoitteen, jotta asiakas / kone käyttäjä on LAN ympäristössä.</li>
  <li>DHCP snooping - mitä määrittää LAN - kytkimen sulkemasta pos epäilytn tai kriminaalin DHCP palvelimen ja poistaa haitalliset ja epämuodostuneet DHCP-liikenteen.</li>
  <li>Muu ominaisuudesta voidaan käyttää DHCP snooping tietokantatietoja, mitä varmistaksen IP- eheyden layer 2 tason toimialueella ja tämän avulla mitä tapahtuu..</li>
  <dl>
    <dd>- seuraa ip osoitteiden fyysisen sijainnin yhdistettyn AAA - kirjapitoon tai SNMP:n /dd>
    <dd>- varmistam että isännät käyttävät vain niille määritettyi IP-osoiteitta yhdistettynä lähde-vartijaan eli lähdelukitus </dd>
    <dd>- pyyhi ARP - pyynnöt yhdistettynä arp-tarkastukseen eli arp-protect ARP(address resolution protocol)</dd>
  </dl>
</ul>

<hr>
<h2>DHCP snooping trusted & untrusted port</h2>


<h2>DHCP snooping vahvistamisen komennot ja muut tarkistamiset</h2>

Tämän komento tulee tapahtumaan ja tarkemisessa tulee kytkimille, myös määrityksessä

tulostuu jokinlainen DHCP taulukko
$show ip dhcp snooping
$show ip dhcp snooping binding
