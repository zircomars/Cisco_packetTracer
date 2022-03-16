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

![alt text](images/HSRP-interVLAN.PNG?raw=true)

# configurointi ohjeet ja muut oppaat:
https://study-ccna.com/cisco-hsrp-configuration/ <br>
https://www.routerfreak.com/how-to-configure-hsrp-on-a-cisco-router/ <br>
https://www.youtube.com/watch?v=gxsMuHXCOqg <br>
https://www.youtube.com/watch?v=aVxFnAh2gFA <br>
https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3560/software/release/12-2_25_se/configuration/guide/3560scg/swhsrp.pdf <br>
https://www.geeksforgeeks.org/hot-standby-router-protocol-hsrp/ <br>
