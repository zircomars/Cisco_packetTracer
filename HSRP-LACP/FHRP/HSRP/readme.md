# Hot Standby Router Protocol - HSRP & configurations

![alt text](images/HSRP-sampleConf.PNG?raw=true)

Konfiguroinnissa tapahtuu komennon määrityksellä "preempt". Preempt sanasta on "preemption" ja Suomeks. etuoikeus, sekä Cisco reittimissä on suuuret resurssit, suurempi kaistanleveys tai vähemmän latenssi/viive (latency) muihin verkoihhin reitttimiin verratuna. Myös HSRP:ssä on oletuasrvo, mitä pitää asentaa komennolla "$standby preempt", mitä reititin on korkeampi HSRP-prioriteettitaso, että voi toimia välittömästi. Oletusprioriteetti on 100, mutta prioriteetin arvoa manipuloida vaaliprosessia. <br>

Komennossa tapahtuu tapahtuu standby 2, mikä on group luku, ja sekä voidaan luoda group [nimi], että jos tapahtuu isompi tai pienempi organisaation HSRP protokollan määritys. Koska jotta reititin ryhmitys tunnistavat oman joukkueen/henkilöstön/organisaation tyypin.

![alt text](images/HSRP-conf-1.PNG?raw=true)

![alt text](images/HSRP-conf-2.PNG?raw=true)

![alt text](images/HSRP-conf-3.PNG?raw=true)

<h2> Sama harjoitus kuin ylempi versio, mutta uusi yritys </h2>

Reitittimen konfiguroinnissa voi suorittaa mainonnan, että kokoonpanossa pitää kommunikoida. Reitityksestä voi esim. suorittaa staatisella tai dynaamisella reitityksellä. Staatinen tapahtuu komenolla: route <vastapään_ip-osoite> <vastapään_aliverkko/subnet> <kohteen-IP_osoite> & tai nopein on: 0.0.0.0 0.0.0.0 <kohteen-IP_osoite>. Dynaaminen  RIP , mitä tapahtuu kohteen reitittimen lähistön IP-osoitteet. <br>

<ins>Huom!</ins> älä luo uutta reititintä, ja laajenna reititystä enempään, koska jos laajentaa reititystä eteenpäin, mitä tuottaa monimutkaisempaa reititystä, että kahden tai useamman reitittimen yhdistäminen ja saada kommunikoimaan menee vaikeaksi.  Myös ei tiedä johtuuko HSRP ryhmityksestä, vai pitääkö luoda laajempi ryhmitys kuten OSPF ja EIGRP.
Staainen ja dynaaminen, mitä kuin mainostaa oman lähialueet. Staatinen, mitä mainostaa vain kauempaa, mutta porttien yhdistämisessä tapahtuu serial kaapeli

![alt text](images/HSRP-confi-1.PNG?raw=true)

# komennot ja muut varmistukset

Reitittimessä voi tarkistaa HSRP taustan, että on komento etuoikeus suoritustilassa ja muut käyttöliittymt / järjestelmät ja muut ominaisuudet, että onko määritetty active vai standby: <br>
$show standby <br>
$show standby brief <br>

Tarkistaa reitittimen HSRP käyttöliittymän, että on status-tilanne (Active & standby), määrittänyt prioriteettin luvun ja Virtual IP-osoitteet: <br>
$show standby brief <br>

# Inter VLAN ja multiple HSRP

Kaksi tai useampaa VLAN-id oman ryhmitys/organisaatiossa, että kulkevat HSRP reitittimen ylitse, ja pääsevät pinggaa esim. serveriin. HSRP reitityksessä tapahtuu kaksi standby <group-luku/nimi>, että sisäisen Virtual IP-osoite. Virtual IP-osoite, mitä pitää täsmätä isäntä tietokoneiden oletusyhdyskäytävä (default-gateway), koska jotta sisäisen käyttöliittymässä muodostuu IP-osoite rajapinta (subinterface). Tässä harjoituksessa tapatui. VLAN7 ja 5, että reitittimen porttiin määrittyy Gig0/0.7 ja Gig0/0.5 oma IP-osoite, että kuin reitittimen pää portti Gig0/0 luodaan muutama <ins> sijainen osoite </ins>. Ennen sitä kytkimiin tulee määrittää portille trunk moodi, koska oletuksena kytkemissä kulkeutuu vain VLAN1, ja jotta saisi vietyä tai kommunikoitua useampi VLAN-id orgsanisaatio eteenpäin. <br>

HSRP konfigurinnoissa tapahtuu, että molemmissa konfigurnnoissa tapahtuu kaksi osainen, että on "active" ja "standby" ryhmitys, koska määrityksessä HSRP protokollan prioriteeti luku on 100, että valitaan isompi luku kuin oletuksena. Kaksi osaisessa tapahtuu kuin Inter VLAN-methodi, mutta HSRP:ssä luodaan kuten Group 7 (VLAN 7) ja Group 5 (VLAN5), että Router-4:ssa on pää 7 ja sivullinen 5, sekä Router-5:ssa on pää 5 ja sivullinen 7. Myös viimeisenä tapahtuu dynaamienn reititys, että reititin mainostaa viereisen IP-osoitteen, ja dynaamisen RIP versio 2:lla.

Dynaaminen RIP protokollan perus määrittää etäisyysvektori reititys prokollan, että käytettävän lähistön alueet, ylläpitä ja myös määrittää reititystaulukon automaatttisesti, että verkko muuttuu tai verkkoyhteyskatkeaa. Versio 2:ssa, jotta voi lähettää ja vastaanottaa RIP-pakettei päivitätkseen reittejä koko verkossa.

![alt text](images/HSRP-interVLAN.PNG?raw=true)

Ylemmän kuvan kahden reitittimen ja sisäisen HSRP konfigurointi, että määrityksessä tapahtuu kuin Inter-VLAN, mutta määrityksessä tapahtuu vastaava alirajapinta numero. Konfiguroinnin jälkeen tapahtuu, että Router-4 sisäisen VLAN7 on active, ja VLAN5 on standby, sekä Router-5 sisäisen VLAN5 on active ja VLAN7 on standby.

![alt text](images/HSRP-twoStandbyInterVlan.PNG?raw=true)

<h3>Pieni yhteenveto tilanne (status), konfirugointi ja muut infot: </h3>

![alt text](images/HSRP-InterVlan-1.PNG?raw=true)

![alt text](images/HSRP-InterVlan-2.PNG?raw=true)

![alt text](images/HSRP-InterVlan-3.PNG?raw=true)

![alt text](images/HSRP-InterVlan-4.PNG?raw=true)


# configurointi ohjeet ja muut oppaat:
https://study-ccna.com/cisco-hsrp-configuration/ <br>
https://www.routerfreak.com/how-to-configure-hsrp-on-a-cisco-router/ <br>
https://www.youtube.com/watch?v=gxsMuHXCOqg <br>
https://www.youtube.com/watch?v=aVxFnAh2gFA <br>
https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3560/software/release/12-2_25_se/configuration/guide/3560scg/swhsrp.pdf <br>
https://www.geeksforgeeks.org/hot-standby-router-protocol-hsrp/ <br>
