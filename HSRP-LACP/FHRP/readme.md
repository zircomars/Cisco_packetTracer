# First-Hop Redundancy Protocols (FHRP)

TIetokone verkottumisen protokolla, mitä on suunnitteltu suojaamaan oletusyhdyskäyttävää (default gateway) käytettyyn on aliverkon (subnet) anatama kaksi tai useampaan reitittimiä tarjoavia varmuuskiopiota. Jokaisessa organisaation verkon isännällä pitää olla tarve reitittimen oletusyhdyskäytävä (default gatewa), mitä isäntä voi muodostaa yhteyden internettiin. Mutta jos yhdyskäytävän (gateway) reititin siirtyy offline-tilaan, tai oletusyhdyskäytävän IP-osoite muutetaan määrityksen aikaan.

Yhdyskäytävän reitittimen vaihtaminen aiheuttaa pidemmän palvelukatkon organisaation käyttäjille, eikä se ole reaktiivinen tapa käsitellä ongelmaa.

(FHRP) on hypyn redundanssi protokolla, mitä on suunniteltu tarjoamaan redundanssia yhdyskäytävän reitittimen organisaation verkon käyttämällä virtuaalista IP-osoitetta ja virtuaalista MAC-osoitetta. FHRP:n toteuttamiseksi yhdyskäytävä reitittimenä tulisi olla kaksi tai useampia reitittimiä. Virtuaalista IP-osoitetta ja virtuaalista MAC-osoitetta käytetään molemmissa reitittimessä. Virtuaalinen IP-osoite on oletusyhdyskäytävän IP-osoite kaikille organisaation verkossa oleville laitteille. Yhtä reititintä käytetään aktiivisena reitittimenä (yhdyskäytäväreitittimenä), ja toinen reititin on valmiustilassa. Jos aktiivinen reititin siirtyy offline-tilaan, valmiustilassa oleva reititin tulee olemaan kaikkien isäntien yhdyskäytäväreititin. 

Esimerkkit protokollia on kuten:

- Hot Standby Router Protocol (HSRP) 
- Virtual Router Redundancy Protocol (VRRP) 
- Virtual Router Redundancy Protocol version 2 (VRRPv2)

- Common Address Redundancy Protocol (CARP)
- Gateway Load Balancing Protocol (GLBP)
- ICMP Router Discovery Protocol (IRDP

# Toteuttamisessa tapahtuu kolme tapaa FHRP protokollassa on: (HSRP, VRRPP & GLBP) 

<h3>Hot Standby Router Protocol (HSRP) </h3>

Ciscon omistama reitittimen redundanssi protokolla, joka mahdollistaa reitittimien klusterin yhteistyön ja kaikki reitittimet ovat valmiita olemaan oletusreitittimiä. Kaikilla klusterin reitittimillä on sama virtuaalinen IP-osoite ja virtuaalinen Mac-osoite. 

HSRP:ssä on kaksi tilaa, mitä on "active" ja "standby" reititin. <ins> Active:ssa </ins>, mitä reititin, joka lähettää ja vastaanottaa aktiivisesti paketin isännälle organisaatiossa. Se on oletusyhdyskäytäväreititin. Vain yksi aktiivinen reititin valitaan reitittimien joukosta. <ins> Standby:ssa </ins>, mitä reitittimet, mitkä ovat vakiintunut aktiivinen reititin siirtyy offline-tilaan, valmiustilassa olevien reitittimien joukosta valitaan aktiiviseksi reitittimeksi. 

Jos aktiivinen reititin siirtyy offline-tilaan, reitittimen vikasieto tapahtuu. Nämä muutokset eivät vaikuta isänteihin. Isäntä säilyttää saman IP-osoitteen ja MAC-osoiteasetuksen. Oletusyhdyskäytävän IP-osoite on edelleen sama kaikissa isännissä. Isännän ARP-taulukossa ei tapahdu muutoksia, koska yhdyskäytävän reitittimen virtuaalinen MAC-osoite on sama. Muutokset vikasietotilassa tapahtuvat vain reitittimessä ja kytkimessä, eivätkä ne vaikuta isänteihin. 

<h3>Virtual Router Redundancy Protocol (VRRP) </h3>

Toimittaja neutraali redudanssi protokolla, mitä ryhmittelee fyysisen reitittimen klusterin (kaksi tai useampi reitittimiä) tuottakseen uuden yhden virtuaalisen reitittimen. Se mahdollistaa redundanssin määrittämällä saman virtuaalisen yhdyskäytävän IP-osoitteen ja MAC-osoitteen kaikille VRRP-ryhmän fyysisille reitittimille. Tällä hetkellä VRRP on versiossa 2. Siinä on melkein sama konsepti kuin HSRP:ssä. Ainoa ero on, että ennaltaehkäisy on oletusarvoisesti käytössä VRRP:ssä, kun taas HSRP:ssä se on määritettävä manuaalisesti. 

VRRP protokollassa toteutuu kaksi tyypistä tilaa on "master" & "backup" reittitin. <ins> Master router </ins>-  Se on kaikkien organisaation isäntien nykyinen oletusyhdyskäytävä. Se lähettää ja vastaanottaa aktiivisesti paketteja isännille. <ins> Backup router </ins> - Varareititin toimii pääreitittimenä vikasietotilassa tai kun pääreititin siirtyy offline-tilaan.

<h3>Gateway Load Balancing Protocol (GLBP) </h3>

Verrattuna HSRP:hen ja VRRP:hen, GLBP on erilainen. GLBP:n avulla ryhmän sisällä olevat reitittimet voivat suorittaa kuormituksen tasapainotuksen. Yksinkertaisesti sanottuna kaikki oletusyhdyskäytävän IP-osoitteeseen siirrettävä liikenne kuormitetaan yksitellen tai kiertoteitse ryhmän reitittimien kesken. GLBP:llä on sama tila kuin HSRP:llä, jota kutsutaan aktiiviseksi ja valmiustilaksi. GLBP:n aktiivisen ja valmiustilan mekanismi on sama kuin HSRP:n aktiivinen ja valmiustila. 

<hr>

# ohjeet, opas ja muut tutoriaalit:

https://study-ccna.com/cisco-fhrp-explained/ <br>
