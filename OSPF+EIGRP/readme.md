# OSPF ja EIGRP combo

- [configurations](#configurations)
  * [OSPF default route](#OSPF-default-route)
  * [redistribution](#redistribution)
- [guide, tutoriaalit ja yms](#guide,-tutoriaalit-ja-yms)

Reitityksessä tapahtuu pientä *redistributing* , mitä kuin tapahtuu jakamisen uudelleen ja yhteenvetoa (summization). Koska useissa verkoissa on erilaisia reititysprotokollia ja tarvitsee jonkinlaisen menetelmän vaihtamiseen, jotta suorittavat reitityksen välillä, siksi kutsuttaan *redistributing*. Molemmissa tapahtuu cost ja metric menetelmä, koska OSPF:ssä käyttää cost ja EIGRP:ssä käyttää k-arvoja, mitä eivät sovi yhteen, ja RIP käyttää hyppylaskua. 

Lisäksi *redistributing* tuoo toisen ongelman kuin, jos et *import* eli tuo reititsytietoa yhdestä reititysprotokollasta toiseen , että on mahdollista luoda reitityssilmukoita. 

<img src="images/EIGRP-OSPF-combo1.PNG" width="1250">

# configurations

Konfiguroinnissa voi tapahtuua oletuksena sen alueen protokollan määritys eli mainostaa oman OSPF ja EIGRP reitityksen, että lisää perintiesen staatisen reitityksen kuin toisi toisen puolen raja puolelta tulevia organisaatioita. Myös määrityksessä on mahdollista keinoa, jotta saisi OSPF ja EIGRP protokollan kommunikoitua yhdessä. Toiminnassa vaikuttaa useiden protokollien määrityksessä kuten dynaaminen RIP, staatinen IP route, ja muita reititysprotokollia. 

<img src="images/EIGRP-OSPF-combo2.PNG" width="950">

<img src="images/EIGRP-OSPF-combo3.PNG" width="350">

## OSPF default route

Normaalisessa alueen pistää oletuksen reitityksen, mitä voi olla peräisin mistä tahansa OSPF-reitiyksestä. OSPF voi luoda oletusreitin, mitä on käytettävä (default-information originate) komentoa "default-information originate". On kaksi tapaa mainostaa aluetta, mitä ensimmäisenä on 0.0.0.0 OSPF-tunnus, jos mainosreitittimet on oletusreittei. Toinen on 0.0.0.0:n mainostaminen riippumatta siitä, onko mainosreitittimellä jo oletusreitti. Toinen tapa voidaan toteuttaa lisäämällä avainsana aina oletusinformaation alkuperäkomentoon. <br>

Komento: "default-information originate"

<br> Staattisella oletusreitillä reitittimen tarvitsee vain tietää kohteen sisäisen organisaatiossa, ja käyttää oletusreittiä välittääkseen IP paketien muille osoitteile verkkoon. Myös tapahtuu, jos mainostaa OSPF ja EIGRP protokollien välisen yhteyden toisiinsa.

## redistribution

Reititysprotokollan tarkoituksena on mainostaa muille reititysprotokolille, että kuin suorittaisi kokoonpanon kuten staatinen, dynaaminen RIP, EIGRP ja OSPF tai muu perus suoraan yhdistetyille reiteille, joten tätä kutsutaan Suom. *uusjako / uudelleen jakaminen.* Usein yhessä reititysprotokollan käyttämisessä tapahtuu koko IP-verkko reititys, mitä usein tapahtuu sitä kokoonpanoa tai projektin luomista, kuten yrityksen fuusioiden, useiden verkovalvojen hallintaa, osastoa ja jopa useita toimittajia ympäristössä. Erilaisien reititysprotokollien suorittamista on usein osa verkon suunnittelua, koska jotta saataisi verkko ympäristöä toimimaan ja jakaa dataa asiakkaalle tai muille organisaatioille vastaavia tärkeitä pakettja/tietoja. 

Erot reititysprotokollan ominaisuuksissa, kuten mittareissa, hallinnollisissa etäisyyksissä, luokka- ja luokkattomissa ominaisuuksissa, voivat vaikuttaa uudelleenjakoon. Nämä erot on otettava huomioon, jotta uudelleenjako onnistuu. Reitityksellä tapahtuu, että käyttämällä erillisiä reititysprotokollia jotta haluaa yhdistää puolta verkosta muihin protokolliin.



# guide, tutoriaalit ja yms

https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/47868-ospfdb9.html <br>
https://study-ccna.com/ospf-default-information-originate/ <br>
https://www.cisco.com/c/en/us/support/docs/ip/enhanced-interior-gateway-routing-protocol-eigrp/8606-redist.html <br>









