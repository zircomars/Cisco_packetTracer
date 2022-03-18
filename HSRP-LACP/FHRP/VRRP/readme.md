# FHRP - VRRP (Virtual Router Redundancy Protocol)

Joka on dynaaminen jakaa vastuun yhdestä tai useammasta virtuaalireitittmestlä lähiverkoon VRRP-reitittimille, jolla on useita monikäyttölinkin reitittimet voivat käyttää samaa virtuaalista IP-osoiteta. VRRP kokoonpanossa on yksi reititin tulee valita tila (status), että yksi reitin tulee "master"ksi, ja muut toimivat "backup":ksi, että jos virtuaalireititin "master" - isäntä epäonnistuu. VRRP on suunniteltu käytettäväksi monikäyttö- ryhmälähetys- tai lähetyskykyisten Ethernet Lan verkkojen ylitse. LAN-asiakkaat voidaan määrittää virtuaaliseen laitteseen käyttämällä oletusyhdyskäytävää.
<br>
Osa VRRP-logiikasta on hyvin samankaltainen kuin HSRP, mutta tapa määrittää VRRP Cisco RouterIssa on melkoinen sama tapa. Koska HSRP:ssä reititimessä tapahtuu tila (status) active ja standby, että VRRP:ssä "master" ja "backup", sekä prioritetti luku

# VRRP router priority & preemption

Prioriteetti määrittää VRRP reitittimen roolin, että muuttuuko <ins> "master" </ins> vai <ins> "backup":ksi </ins>, että jos virtuaalisen reitittimen isäntä epäonnistuu. "Master" roolia on kuin yksi, että jos sattuu prioritetti luku olemaan suurempi kuin alkuperäisen "master" määritettyn luku. Prioritettin arvot menee kuin HSRP, eli 1-254, että käyttämällä vrrp priority komentoa. Sekä oletusarvo on 100, että jos reititin-A pitää olla "master", mitä pitää olla yli oletusarvosta.

Oletusarvoisesti ennaltaehkäisevä järjestelmä on käytössä, jolloin korkeamman prioriteetin virtuaalisen reitittimen varmuuskopio, joka tulee saataville, ottaa käyttöön virtuaalisen reitittimen varmuuskopion, joka valittiin virtuaalisen reitittimen pääkäyttäjäksi. Voit poistaa tämän ennaltaehkäisevän mallin käytöstä komennolla $no vrrp preempt. Jos ennaltaehkäisy on poistettu käytöstä, virtuaalisen reitittimen varmuuskopio, joka on valittu virtuaalisen reitittimen pääkäyttäjäksi, pysyy isäntänä, 
kunnes alkuperäinen virtuaalisen reitittimen isäntä palautuu ja siitä tulee jälleen isäntä. 

# configurointi ohjeet ja muut oppaat: <br>
www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipapp_fhrp/configuration/15-e/fhp-15-e-book/VRRPv3-Protocol-Support.pdf <br>
 <br>
https://www.mustbegeek.com/configure-vrrp-in-cisco-ios-router/ <br>
 <br>
 <br>
