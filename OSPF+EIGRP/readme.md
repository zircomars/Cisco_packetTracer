# OSPF ja EIGRP combo

- [configurations](#configurations)
  * [OSPF default route](#OSPF-default-route)
  * [redistribution](#redistribution)
- [guide, tutoriaalit ja yms](#guide,-tutoriaalit-ja-yms)

Reitityksessä tapahtuu pientä *redistributing* , mitä kuin tapahtuu jakamisen uudelleen ja yhteenvetoa (summization). Koska useissa verkoissa on erilaisia reititysprotokollia ja tarvitsee jonkinlaisen menetelmän vaihtamiseen, jotta suorittavat reitityksen välillä, siksi kutsuttaan *redistributing*. Molemmissa tapahtuu cost ja metric menetelmä, koska OSPF:ssä käyttää cost ja EIGRP:ssä käyttää k-arvoja, mitä eivät sovi yhteen, ja RIP käyttää hyppylaskua. 

Lisäksi *redistributing* tuoo toisen ongelman kuin, jos et *import* eli tuo reititsytietoa yhdestä reititysprotokollasta toiseen , että on mahdollista luoda reitityssilmukoita. 

<img src="images/EIGRP-OSPF-combo1.PNG" width="1250">

# configurations

Konfiguroinnissa voi tapahtuua oletuksena sen alueen protokollan määritys eli mainostaa oman OSPF ja EIGRP reitityksen, että lisää perintiesen staatisen reitityksen kuin toisi toisen puolen raja puolelta tulevia organisaatioita. 

<img src="images/EIGRP-OSPF-combo2.PNG" width="950">

<img src="images/EIGRP-OSPF-combo3.PNG" width="350">

## OSPF default route

Normaalisessa alueen pistää oletuksen reitityksen, mitä voi olla peräisin mistä tahansa OSPF-reitiyksestä. OSPF voi luoda oletusreitin, mitä on käytettävä (default-information originate) komentoa "default-information originate". On kaksi tapaa mainostaa aluetta, mitä ensimmäisenä on 0.0.0.0 OSPF-tunnus, jos mainosreitittimet on oletusreittei. Toinen on 0.0.0.0:n mainostaminen riippumatta siitä, onko mainosreitittimellä jo oletusreitti. Toinen tapa voidaan toteuttaa lisäämällä avainsana aina oletusinformaation alkuperäkomentoon. <br>

Komento: "default-information originate"

<br> Staattisella oletusreitillä reitittimen tarvitsee vain tietää kohteen sisäisen organisaatiossa, ja käyttää oletusreittiä välittääkseen IP paketien muille osoitteile verkkoon. Myös tapahtuu, jos mainostaa OSPF ja EIGRP protokollien välisen yhteyden toisiinsa.

### redistribution

Suom. uusjako / uudelleen jakaminen.

# guide, tutoriaalit ja yms

https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/47868-ospfdb9.html <br>
https://study-ccna.com/ospf-default-information-originate/ <br>
