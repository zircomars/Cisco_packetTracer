# BGP (Border Gateway protocol)

- [Reititysprotokolla](#Reititysprotokolla)
  * [BGP protokollan käyttö](#BGP-protokollan-käyttö)
- [Autonominen järjestelmä](#Autonominen-järjestelmä)
  * [AS numero](#AS-numero)
- [Peering](#Peering)
  * [Dynamic BGP peering](#Dynamic-BGP-peering)
- [eBGP and iBGP](#eBGP-and-iBGP)
- [BGP options](#BGP-options)
  * [Default route](#Default-route)
  * [Default route and ISP Routes](#Default-route-and-ISP-Routes)
  * [All internet routes](#All-internet-routes)
- [Komennot](#Komennot)
  * [verifying](#verifying)
- [Combo EIGRP, BGP ja OSPF](#Combo-EIGRP,-BGP-ja-OSPF)
- [tutoriaalit ja muu guide oppaat](#tutoriaalit-ja-muu-guide-oppaat)
  * [konfigurointi](#konfigurointi)
  * [ebgp and ibgp](#ebgp-and-ibgp)

<img src="images/BGP-path1.PNG" width="750">

# Reititysprotokolla

BGP (border gateway protocol) mikä on Internetin reitityksen protokolla, mitä tarkoituksena on hoittaa reititysekn autonomisten järjestelmän (autonomous systems, lyhenne: *AS*) välillä. BGP tukee luokatonta reititystä ja käyttää reittien yhdistämistä pitäkseen reititystaulukojen koon pienenä. 

Kaksi tyypistä BGP mallista (External & Internal) External BGP (eBGP) - naapurit, jotka yhdistävät erillisenä autonomisen järjestelmän. Internal BGP (iBGP) - naaprurit samssa autonomisessa järjestelmässä.

Vähä niin kuin mainostaa ensin, mitä lähellä löytyy, kuin "OSPF" melkee. Ensin mainostaa oma lähialueet "network (ip-add)", ja määrittää naapruin AS luvun, mikäli on olemassa. Kaapelointi tulee olemaan suorakytkentä, ei mitään ristiinkytkentöi tai serial kaapelia.

## BGP protokollan käyttö

BGP käyttöä ei ole välttämätöntä, kun sitä tarvitaan useita Internet-yhteyksissä. Lähtevien liikenteessä vikasietoisuus tai redudanssi voidaan helposti hoitaa, joko IGP:llä, kuten OSPF tai EIGRP. BGP on myös tarpeetonta, jos ulkoisen AS (kuten internet) on vain yksi yhteys. Linjalla on yli 100 000 reittiä Internetissä ja sisätiloissa reitittimissä ei pitäisi turhaan kuormittaa.

Esim tai ehkä (multi-homed AS Topology) ISP (internet service provider) Internetin - palveluntarjoaja. <br>

Yritys (OSP) ---- BGP---- ISP-3 (EIGRP) -----BGP------ jakautuu joko ISP-2 ja Content Provider(OSPF) <br>

ISP-2 ----- BGP ----- COntent Provider (OSPF)

staatisessa reitityksessa tilanteessa ei kannata käyttää BGP:tä

BGP:ssä käytetään kahdessa reitittämisen itsenäisessä järjestelmässä iBGP ja vastoin protokollan Internet-sovelluksessa eBGP.

BGP käyttää TCP porttia num. 179. 

# Autonominen järjestelmä
Autonominen järjestelmä = AS (autonomous system)

Tarkoittaa TCP/IP- reitityksenprotokolla, käytettävissä yksittisen toimijan verkkokokonaisuutta.

Omistaja vastaa tiettyjen IP-osoitetta liikenteen reitityksellä perille. AS järjestelmässä on tunnettava toisensa ja niiden on käytettävä erityisen autonomisen järjestelsmä välisen reititykseen suunniteltujen protokollaan IP-osoitteen kertomisella.

## AS numero

ASN (Autonomous System Numbers), mitä on joukko Internetin reitittäviä IP-etuliiteitä, mitkä kuuluvat verkkoon tai kokoelmaan verkkoihin, ja jotka kaikki hallinnoi, ohjaa ja valvoo entiteettisen tai organisaatio. AS käyttää yhteistä reitityspolitiikkaa, jota kokonaisuus hallitse. IANA (Internet Assigned Numbers Authority) on määrittänyt AS:lle laajuisen ainutlaatuisen 16-numeroisen tunnistenumeron, mitä tunnettaan parhaillaan ASN tai AS.

IANA antaa as järjestelmän käyttöä, että numeroltaan 1-65411 ovat julkisia (käyttäää alkuperäisen 16-bittiä), ja numerosta 64512 - 65535 on varattuihin yksityisiin (käyttää n. 32-bittiä rajaltaan), ja omiin tarkoituksiin. AS järjestelmä otettiin käyttöö, kun säätelee verkottumisorganisaatioita, kuten Internet-palvelutarjoajia (ISP = Internet service providers), oppilaitoksiin ja valtioiden virastoihin. 

Border Gateway Protocol (BGP), myös joka hallitsee reititettyjä peering-yhteyksiä, etuliitemainoksia ja pakettien reititystä eri autonomisten järjestelmien välillä Internetissä. BGP käyttää ASN:ää jokaisen järjestelmän yksilölliseen tunnistamiseen. 

# Peering

Peering suom. *pääri/pilkottaa* . Tarkoittaa kahden reititimmen (router), jotka muodostavat yhteyden BGP-tietojen vaihtoa, mitä kutsutaan BGP-peeriksi. BGP vertaisyritys vaihtavat reititystietoja keskeisen BGP-istuntojen kautta, jotka kulkevat TCP:n ylitse, joka on luotettava, että yhteysuuntaisen ja virheetön protokolla. Myös voi olla useita reitittimiä esim. A-reitin ----- B-reititin ----- C-reititin, että A- ja B:ssä tapahtuu pieni peering, että B-ja C-reititin. 

<img src="images/BGP-peering1.PNG" width="750">

<img src="images/BGP-peering2.PNG" width="750">

# eBGP and iBGP

BGP:ssä käytetään kahdessa reitittämisen itsenäisessä järjestelmässä iBGP ja vastoin protokollan Internet-sovelluksessa eBGP.

iBGP: n ja eBGP-vertaisarvioinnin välillä on tavassa, jolla yhdeltä vertaiselta vastaanotetut reitit levitetään muille vertaisryhmille. Esimerkiksi uudet reitit oppinut peräisin eBGP peer tyypillisesti uudelleen kaikille iBGP ikäisensä sekä kaikki muut eBGP ikäisensä (jos kauttakulku on käytössä reitittimen). 
Jos kuitenkin uusia reittejä opitaan iBGP-vertaisverkossa, niitä mainostetaan uudelleen vain kaikille eBGP-vertaisryhmille.
Nämä reitin etenemissäännöt edellyttävät tosiasiallisesti, että kaikki iBGP-vertaisryhmät AS: n sisällä ovat yhteydessä toisiinsa täydellä silmällä.

iBGP on vähä kuin oma grouppi routerit, ja routeri jatkaa siitä eteenpäin sitä kutsutaan eBGP, vähä kuin edellisen BGP-1 harjoituksessa.

Tai kaksi erii AS lukua sitä kutsutaan kuin eBGP <br>
esim;; AS(100) -----eBGP----- AS(200)

<img src="images/EBGP-IBGP.PNG" width="500">

<img src="images/EBGP-IBGP2.PNG" width="1250">

<b>HUOM!</b> Cisco packet tracer simulaatiossa ei tuetta *iBGP* konfigurointia, mutta muissa simulaatiossa softassa voi määrittää sen ibgp konfiguroinnin määrityksen.

Alemmasta kuvassa iBGP tunnetaan parhaiten ryhmityksenä, että kuin pinggaus viesti hyppivät toisiinsa tai jos yhteys tapahtuu katkos, mitä viesti kulkeutuu toisesta reitistä. eBGP voi konfiguroida muiden AS-num kanssa, mitä käyttää virtuaalista rajapinnan naapurienosoitteen määritystä, kunhan reititn tietää esim. kolmionmuotoinen verkko topologia.

<img src="images/EBGP-IBGP3.PNG" width="1250">

# BGP options
## Default route

<img src="images/BGP-options-1.PNG" width="500">

## Default route and ISP Routes

<img src="images/BGP-options-2.PNG" width="500">

## All internet routes

<img src="images/BGP-options-3.PNG" width="500">


# Komennot

## verifying

Tarkista BGP konffaus ja yms reititystaulukkot: <br>

| komennot | kuvaus |
| -------- | -------- |
| $ show ip bgp | BGP konfiguroinnun komento, että voi tarkistaa BGP topologian tietokannan & tulos luettelee taulukon kaikista verkoista, joista BGp tietää, että kukin verkon seuraava hypyn, jotkin kunkin reitin attribuutit ja kukin reitin AS-polku. |
| $ show ip bgp summary | Näyttää eri BGP-tietokantojen käyttämä muisti, BGP-toimintatilastot ja luettelon BGP- naapureista, kohteen reitittimen AS-numero |
| $ show ip bgp neighbors | tulostaa tiedon kustakin naapurista, että voidaan muokata lisäämällä naapurin IP-osoitetta |
| $ show ip protocols | tarkista koko protokollan taustat |
| $ show ip route | perus reititystaulukkon reitittimestä |

# Combo EIGRP, BGP ja OSPF

Jos luoo useamman protokollan combon yhdistämisen, että reitityksessä on BGP, EIGRP ja OSPF reititysprotokollat yhdessä samassa ryhmässä. Reitityksessä tapahtuu "redistribute" määritys reitittimeen. 

# tutoriaalit ja muu guide oppaat <br>

https://www.certiology.com/cisco-certifications/ccna/ccna-routing-and-switching/free-cisco-ccna-study-guide/bgp.html <br>
https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/iproute_bgp/configuration/xe-16/irg-xe-16-book/configuring-a-basic-bgp-network.html <br>
https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/iproute_bgp/configuration/15-mt/irg-15-mt-book/irg-overview.html <br>
https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/iproute_bgp/configuration/15-mt/irg-15-mt-book.pdf <br>
https://www.ciscopress.com/articles/article.asp?p=2756480  <br>
https://www.9tut.com/border-gateway-protocol-bgp-tutorial <br>
https://au.int/sites/default/files/documents/31363-doc-session_7-1-_simple_multihoming.pdf <br>
http://luk.kis.p.lodz.pl/ZTIP/BGP.pdf  <br>
https://www.kwtrain.com/blog/bgp-pt1 <br>

## konfigurointi: <br>
https://nsrc.org/workshops/2013/nsrc-marwan-bgp-ixp/raw-attachment/wiki/Agenda/BGP_ref_1_en.pdf <br>
https://www.router-switch.com/faq/bgp-configuration.html <br>
https://www.bgp.us/router/configure-bgp-on-cisco-routers/ <br>
https://www.zframez.com/tutorials/cisco-bgp-configuration-commands.html <br>
https://www.routeralley.com/guides/bgp.pdf <br>

## ebgp and ibgp <br>
https://ipwithease.com/sample-configuration-for-ebgp-and-ibgp/ <br>
http://ce.sc.edu/cyberinfra/workshops/Material/BGP/Lab%208.pdf <br>
https://networklessons.com/bgp/how-to-configure-ebgp-external-bgp <br>
https://www.mustbegeek.com/configure-ibgp-in-cisco-ios-router/ <br>


