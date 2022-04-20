# OSPF ja EIGRP combo

- [configurations](#configurations)
  * [OSPF default route](#OSPF-default-route)
  * [redistribution](#redistribution)
  * [redistribution configurations](#redistribution-configurations)
  * [reititystaulukko](#reititystaulukko)
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

- EIGRP into OSPF

<img src="images/OSPF+EIGRP_redistributed-EIGRPtoOSPF.PNG" width="500">

- OSPF into EIGRP

<img src="images/OSPF+EIGRP_redistributed-OSPFtoEIGRP.PNG" width="500">


## redistribution

Reititysprotokollan tarkoituksena on mainostaa muille reititysprotokolille, että kuin suorittaisi kokoonpanon kuten staatinen, dynaaminen RIP, EIGRP ja OSPF tai muu perus suoraan yhdistetyille reiteille, joten tätä kutsutaan Suom. *uusjako / uudelleen jakaminen.* Usein yhessä reititysprotokollan käyttämisessä tapahtuu koko IP-verkko reititys, mitä usein tapahtuu sitä kokoonpanoa tai projektin luomista, kuten yrityksen fuusioiden, useiden verkovalvojen hallintaa, osastoa ja jopa useita toimittajia ympäristössä. Erilaisien reititysprotokollien suorittamista on usein osa verkon suunnittelua, koska jotta saataisi verkko ympäristöä toimimaan ja jakaa dataa asiakkaalle tai muille organisaatioille vastaavia tärkeitä pakettja/tietoja. 

Erot reititysprotokollan ominaisuuksissa, kuten mittareissa, hallinnollisissa etäisyyksissä, luokka- ja luokkattomissa ominaisuuksissa, voivat vaikuttaa uudelleenjakoon. Nämä erot on otettava huomioon, jotta uudelleenjako onnistuu. Reitityksellä tapahtuu, että käyttämällä erillisiä reititysprotokollia jotta haluaa yhdistää puolta verkosta muihin protokolliin.

Jos suorittaa staatista reititystä, mitä eigrp <num> sisään tulee komento kuin (redistribute static) ja samaan ospf <num> reitityksessä (default-information originate), jotta tapahtuu se special / mainonta kahden reitityksen protokollan ympäristössä. 
 
 <img src="images/OSPF+EIGRP_redistributedConf.PNG" width="350">

### redistribution configurations

Kahden reitityksenprotokollassa eli OSPF ja EIGRP tapahtuu syntaksi, ja määrityksessä vaikuttaa kuten EIGRP:n sisäisen K-arvojen termit eli: *kaistanelveys (bandwidth), viive (delay), luotettavuus (reliability)	, MTU (reliability).* Kuin EIGRP yrittäisi saada käsiksi OSPF protokollan, mitä vaikuttaa special komento.

Määrityksessä tapahtuu eng. *Redistribute OSPF into EIGRP* ja myös *Redistribute EIGRP into OSPF*, että jakaa molemmille reititysprotokollien tekijälle ominaisuutta, ja jotta ymmärtävät toisiaan.

- OSPF into EIGRP <br>

100 33 255 1 1500 - kuulemma on oletus arvoinen metrikka arvo  <br>

Router(config)#router eigrp 2  <br>
Router(config-router)#redistribute ospf ? <br>
  <1-65535>  Process ID <br>
Router(config-router)#redistribute ospf 3  <br>
Router(config-router)#redistribute ospf 3 ?  <br>
  match   Redistribution of OSPF routes <br>
  metric  Metric for redistributed routes <br><br>

Router(config-router)#redistribute ospf 3 match ? <br>
  external       Redistribute OSPF external routes <br>
  internal       Redistribute OSPF internal routes <br>
  nssa-external  Redistribute OSPF NSSA external routes <br>
  
Router(config-router)#redistribute ospf 3 metric ? <br>
  <1-4294967295>  Bandwidth metric in Kbits per second <br>
Router(config-router)#redistribute ospf 3 metric ? <br>
  <1-4294967295>  Bandwidth metric in Kbits per second <br>
Router(config-router)#redistribute ospf 3 metric 1000 ? <br>
  <0-4294967295>  EIGRP delay metric, in 10 microsecond units <br>
Router(config-router)#redistribute ospf 3 metric 1000 33 ? <br>
  <0-255>  EIGRP reliability metric where 255 is 100% reliable <br>
Router(config-router)#redistribute ospf 3 metric 1000 33 255 ? <br>
  <1-255>  EIGRP Effective bandwidth metric (Loading) where 255 is 100% loaded <br>
   
Router(config-router)#redistribute ospf 3 metric 1000 33 255 1 ? <br>
  <1-65535>  EIGRP MTU of the path <br>
Router(config-router)#redistribute ospf 3 metric 1000 33 255 1 1500 ? <br>
  match  Redistribution of OSPF routes <br>
  <cr> <br> 
Router(config-router)#redistribute ospf 3 metric 1000 33 255 1 1500 <br><br>

<hr>

- EIGRP into OSPF

Router(config)#router ospf 3 <br> 
Router(config-router)#redistribute eigrp ? <br>
  <1-65535>  Autonomous system number <br><br>
Router(config-router)#redistribute eigrp 2 ? <br>
  metric       Metric for redistributed routes <br>
  metric-type  OSPF/IS-IS exterior metric type for redistributed routes <br>
  subnets      Consider subnets for redistribution into OSPF <br>
  tag          Set tag for routes redistributed into OSPF <br>
  <cr><br><br>
Router(config-router)#redistribute eigrp 2 <br>
% Only classful networks will be redistributed<br><br>

### reititystaulukko

   Kun on määrittänyt EIGRP:stä OSPF:lle ja OSPF:stä EIGRP:lle, niin tarkista reititystaulukko, jotta havaitsee tapahtuman muutoksen.

- Router-0 <br>
   <img src="images/OSPF+EIGRP_redistributed_R0.PNG" width="500">
 
- Router-1 <br>
   <img src="images/OSPF+EIGRP_redistributed_R1.PNG" width="500">
   
- Router-2 <br>
   <img src="images/OSPF+EIGRP_redistributed_R2.PNG" width="500">

# guide, tutoriaalit ja yms

https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/47868-ospfdb9.html <br>
https://study-ccna.com/ospf-default-information-originate/ <br>
https://www.cisco.com/c/en/us/support/docs/ip/enhanced-interior-gateway-routing-protocol-eigrp/8606-redist.html <br>
https://www.cisco.com/c/en/us/support/docs/ip/enhanced-interior-gateway-routing-protocol-eigrp/8606-redist.html#topic3 <br>
https://spankbang.com/4vizt/video/casey+kisses+rocky+emerson+missed+opportunity <br>

https://www.timigate.com/2018/03/configuring-cisco-route-redistribution-between-eigrp-and-ospf.html
https://networklessons.com/cisco/ccie-enterprise-infrastructure/redistribution-between-eigrp-and-ospf

https://www.youtube.com/watch?v=gmvnfUFKLrY


