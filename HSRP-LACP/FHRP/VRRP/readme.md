# VRRP (Virtual Router Redundancy Protocol)

Joka on dynaaminen jakaa vastuun yhdestä tai useammasta virtuaalireitittmestlä lähiverkoon VRRP-reitittimille, jolla on useita monikäyttölinkin reitittimet voivat käyttää samaa virtuaalista IP-osoiteta. VRRP kokoonpanossa on yksi reititin tulee valita tila (status), että yksi reitin tulee "master"ksi, ja muut toimivat "backup":ksi, että jos virtuaalireititin "master" - isäntä epäonnistuu. VRRP on suunniteltu käytettäväksi monikäyttö- ryhmälähetys- tai lähetyskykyisten Ethernet Lan verkkojen ylitse. LAN-asiakkaat voidaan määrittää virtuaaliseen laitteseen käyttämällä oletusyhdyskäytävää.
<br><br>
Osa VRRP-protokollassa on hyvin samankaltainen kuin HSRP, mutta määrityksen tapa kulkeutuu VRRP Cisco RouterIssa on melkoinen sama tapa. Koska HSRP:ssä reititimessä tapahtuu tila (status) active ja standby, että VRRP:ssä "master" ja "backup", sekä prioritetti luku ja yhteistä on määrittää group luku. <br><br>

<ins>Huom!</ins> varsinaisesti Cisco Packet tracer simulaatio ympäristössä puuttuu tämmöinen VRRP protokollan konfigurointi, mutta sitä voi toimia kuin HSRP.

<h2>Versiot</h2>

VRRP:ssä mahdollistaa laitteiden ryhmitystä muodostamalla yhden virtuaalisen IP-osoitteiden tarjoaman redudanssin. LAN-asiakkaat voidaan sitten määrittää virtuaalilaitteeseen oletusyhdyskäytäväksi (default gateway). Vers 3:ssa ProtocolSupport-ominaisuus tarjoaa mahdollisuden tukea IPV4- tai IPV6 osoitetta, että Vers. 2:ssa tukee vain IPV4:sta. Vers. 3:ssa tukee näitä seuraavia ominaisuuksia:

- Yhteentoimivuus useita valmistajan ympäristöä
- Tukee IPV4 ja IPV6-osoiteta
- Parannettu skaalautuvuus VRRS-polkujen käyttöä

# VRRP router priority & preemption

Prioriteetti määrittää VRRP reitittimen roolin, että muuttuuko <ins> "master" </ins> vai <ins> "backup":ksi </ins>, että jos virtuaalisen reitittimen isäntä epäonnistuu. "Master" roolia on kuin yksi, että jos sattuu prioritetti luku olemaan suurempi kuin alkuperäisen "master" määritettyn luku. Prioritettin arvot menee kuin HSRP, eli 1-254, että käyttämällä vrrp priority komentoa. Sekä oletusarvo on 100, että jos reititin-A pitää olla "master", mitä pitää olla yli oletusarvosta.

Oletusarvoisesti ennaltaehkäisevä järjestelmä on käytössä, jolloin korkeamman prioriteetin virtuaalisen reitittimen varmuuskopio, joka tulee saataville, ottaa käyttöön virtuaalisen reitittimen varmuuskopion, joka valittiin virtuaalisen reitittimen pääkäyttäjäksi. Voit poistaa tämän ennaltaehkäisevän mallin käytöstä komennolla $no vrrp preempt. Jos ennaltaehkäisy on poistettu käytöstä, virtuaalisen reitittimen varmuuskopio, joka on valittu virtuaalisen reitittimen pääkäyttäjäksi, pysyy isäntänä, 
kunnes alkuperäinen virtuaalisen reitittimen isäntä palautuu ja siitä tulee jälleen isäntä. 

# VRRP konfigurointi ja muut info komennot

# configurointi ohjeet ja muut oppaat: <br>
www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipapp_fhrp/configuration/15-e/fhp-15-e-book/VRRPv3-Protocol-Support.pdf <br>
 <br>
https://www.mustbegeek.com/configure-vrrp-in-cisco-ios-router/ <br>
https://www.geeksforgeeks.org/introduction-of-virtual-router-redundancy-protocol-vrrp-and-its-configuration/?ref=gcse <br>
https://cciethebeginning.wordpress.com/?s=vrrp <br>
https://www.routerfreak.com/comparing-hsrp-versus-vrrp-same-thing-only-different/ <br>

https://ipcisco.com/lesson/vrrp-configuration-on-cisco-2/ <br>
https://www.mustbegeek.com/configure-vrrp-in-cisco-ios-router/ <br>
https://ipcisco.com/vrrp-virtual-router-redundancy-protocol-part-4/ <br> 
https://www.pearsonitcertification.com/articles/article.aspx?p=2141275 <br>

https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus5000/sw/command/reference/unicast/n5k-ucast-cr/n5k-vrrp_cmds_show.pdf <br>
https://www.cisco.com/c/en/us/td/docs/routers/crs/software/crs_r4-0/addr_serv/configuration/guide/ic40crs1book_chapter10.html <br>
https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipapp_fhrp/configuration/xe-3se/3850/fhp-xe-3se-3850-book/fhp-vrrp.html <br>
https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipapp_fhrp/configuration/xe-16-5/fhp-xe-16-5-book/fhrp-vrrpv3-xe.html <br>

https://www.youtube.com/watch?v=8Rg0hZtVshQ <br>
https://www.youtube.com/watch?v=zhmH58Ptpic <br>
