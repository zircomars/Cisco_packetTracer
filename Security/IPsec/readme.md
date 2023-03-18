# IPsec (IP Security Architecture) 

  * [IPsec framework](#IPsec-framework)
  * [IKE](#IKE)
  * [Phase 1 ja 2](#Phase-1-ja-2)
- [Transport vs tunnel models ](#Transport-vs-tunnel-models)
- [reitittimen komennot ja konffaus](#reitittimen-komennot-ja-konffaus)
  * [tarkista määritykset](#tarkista-määritykset)
  * [reitittimen versio](#reitittimen-versio)
- [IPsec tutoriaalit ja muut guide asiat](#IPsec-tutoriaalit-ja-muut-guide-asiat)
  * [ipsec phase 1 ja 2 ja ike](ipsec_phase_1_ja_2_ja_ike)

TCP/IP-joukkon kuuluva tietoliikenneprotokolla Internet-yhteyksien turvaaminen. Nämä protokollat tarjoavat salauksen, osapuolten todennuksen ja tiedon eheyden varmistamisen. Pääasiassa tämä tarkoittaa UDP-pohjaisia sovelluksia, ICMP-kontrolliviestejä sekä reitityksessä ja tunneloinnissa käytettyjä IP-protokollia kuten GRE:tä, OSPF:aa ja niin edelleen. Verrattaessa kuljetuskerroksen protokolliin (4.layer OSI-malli), kuten SSLään, haittapuolena on se, että IPsec-protokollien pitää pystyä hallitsemaan myös vakaus- ja fragmentoitumisongelmat, jotka yleensä on hoidettu korkeammalla tasolla, TCP- eli kuljetuskerroksella.

Käytössä protokolla voi käyttää vaihtoehtoisia kuten:
- yhteydenpitokanavien turvaamista, jolloin usieden koneiden isäntä tai jopa koko lähiverkon liikenne ohjataan yhden pisteiden (esim. palomuurien) kautta, jossa lähtevän liikenne salataan ja vastaavasti paluulikenne puretan tai
- pakettiliikenteen turvaamiseen koko matkalle lähettäjältä vastaanottajalle, jolloin päätepisteiden tietokoneet hoitavat salauksen vaatiman prosessoinnin.

IPsec-protokollaa voidaan käyttää VPN-ratkaisun eli näennäisen yksityisverkon rakentamiseen kummallakin tavalla. On huomioitava että saavutettava tietoturva eroaa huomattavasti näiden kahden mallin välillä. Sekä IPsec on melkoinen monimutkainen, ja toteuttamisessa on monta eri tapaa.

<img src="images/IPsec-1.PNG" width="500"> <br>
<img src="images/IPsec-2.PNG" width="500">

IPSEC protokollat: <br>
(AH) authentication header <br>
IP protocol 51 ei siällä tietojen luottamuksellisuutta. Se ei salaa tietoja ollenkaan. AH tarjoaa sekä todennus- että eheyspalvelua.  AH ei suorita salausta, se on nopeampi standardi kui ESP

(ESP) Encapsulation security payload: <br>
IP protocol 50 suorittaa luottamuksellista-, todennusta, ja eheyspalvelua. ESP suorittaa salausta ja on luonnostaan turvallisempi kuin AH. ESP esittelee sekä ylätunnisteen, että perävaunun pakettiin.

Policy ID saa olla eri toisistaan, mutta konffauksen algoritmit, aes, ja muut jotakin tiettyjen ominaisuudet pitää olla identtisiä toisistaan
<img src="images/IPSec_phase1-2key.PNG" width="350"> <br>


<img src="images/IPSec_networkMap1.PNG" width="650"> <br>
<img src="images/IPSec_networkMap2.PNG" width="950">

## IPsec framework

IPsec protokollan suojauksen liikenteen teknisen yksittäiset ominaisuudet:

- Confidentiality: luottamuksellisuus, salaamalla tietoja kuka muu kuin lähettäjä ja vastaanottaja ei voi lukea tietoja. 
- Integrity : eheys, haluttaan varmistaan, että kukaan ei muuta popakettien tietoja. Laskemalla has-arvon lähettäjä ja vastaanottaja voivat tarkistaa, että onko pakettiin tehty muutosta.
- authentication: todennus, lähettäjä ja vastaanottajat todentavat toisensa varmistakseen, että puhutaan todella sen tietyn laitteen kanssa, jotta aikoo käyttää.
- anti-reply: toiston esto, vaikka pakettien olisi salattu ja todennettu, hyökkääjä voi yrittää kaapata tiettyjä/näitä paketteja ja lähettää niitä uudestaan. Järjestysnumeroita käyttämällä IPsec ei lähetä päällekkäisiä paketteja.

![Alt text](images/IPsec-framework01.PNG)

Riskiä ja tietoturvan kannalta, ja varautuminen on hyvä olla. Salauksen kannalta voi halutakseen käyttää DES-, 3DES tai AES-salausta. Todennusta varten voi valita MD5:sen tai SHA-välillä. IPsec voi käyttää monissa erissä laiteissa, että käytetään reitittimessä, palomuurissa, host:ssa ja palvelimessa. Muutama esim. kuinka sitä IPsec käytettään:

- Kahden reitittimen välillä luodakseen site-to-site VPN silattu "bridge" kaksi lähiverkkon yhteytä (LAN).
- Palomuurin ja Windows:hostien välisen VPN-etäkäyttöä.
- Kahden Linux -palvelimien välillä suojattujen turvatonta protokollaa, kuten telnet.



## IKE
Internet Key Exchange - versioita on kaksi tyypistä nimellä IKEv1 tai IKEv2.

IKE on standardiprotokolla, joka käytetään luomaan turvallisen ja todennettun viestikanavan kahden osapuolen välille VPN tunnelin kautta. Protokolla varmistaa VPN-neuvottelujen, etä työskentelevän koneen ja verkko käytön turvallisuutta. 

IKE tärkeässä toiminassa on neuvotella IPSec tietoturvayhdistyksiä (SA security associations). SA:ssa ovat tietoturvakäytäntöjä, jotka on määritelty kahden tai useamman entiteetisen/olion välisen viestinnän varten. Molempien osapuolet käyttävät ja edustavat tietoyn määrän joukkon algoritmita ja yhteisesti sovitujen avaimia yritettäisi muodostaa VPN-tunnelia tai yhteytä. Myös IKE on osa IPsec-protokollia ja algoritmia, joita käytettään siirrettävien arkaluonteisia tietojen suojaamista. IETF (internet negineer task force) kehitti IPsec tarjoamaan turvallisuutta IP-verkkopakettien ja suojattujen VPN-verkkojen todentamista ja salauksia varten.

Hybridiprotokolla, IKE, joka toteutaa myös kaksi aikaisempaa suojausprotokollaa kuin <b>Oakley</b> ja <b>SKEME</b>, TCP/IP-pohjaisessa Security Association Key management protocol (ISAKMP) kehyksessä.

SKEME-protokolla on vaihtoehtoinen versio vaihtoavaimelle (exchange key). ISAKMP RFC 2408:aa käytettään neuvotteluihin (negotiations), tietoturvayhteyksien luomista ja yhteyksien turvaamista IPsec-vertaisyrityksien välillä, että avaintenvaihtoa ja autetikointien puutteen määritämistä. Oakley RFC 2412:tä käytetään avainten sopimuksiin tai vaihtoihin, ja sitä määrittää mekanismi, jota käytetään IKE-istunnon aikana avainten vaihdossa. Diffie-Hellman (D-H) on vaihdossa käytetty oletusalgoritmi.

## Phase 1 ja 2

- ISAKMP (Internet Security Association and Key Management Protocol)
- AES (Advanced Encryption Standard) Encryption Algorithm
- SHA (Secure Hash Algorithm) Cryptographic hash function
- PSK (Pre-Shared Key)
- DH (Diffie-Hellman) Method of securely exchanging cryptographic keys over a public channel

![Alt text](images/IPSec_phase1-2-negotiation.PNG)

VPN tunnelin rakentamiseksi IPsec vertaisyritykset vaihtavat joukon viestejä salauksesta ja todennusta ja yrittävät sopia monista erilaisista parametristä, siks tätä kutsutaan VPN-neuvottelut (negotiation). Tämä sekvensi laite on kuin herätin ja toisessa vastapäässä on vastaaja.

Neuvoteltussa suoriuttuu kahden erillisen vaihdeen (Phase 1 ja 2). 
- Phase 1: tarkoituksena on perusta suojattun ja salatun kanavan, jonka kautta turvata phase 2 vertaistaa/neuvotella toisensa yhteytä. Diffie-Hellman avaimen algoritmi luo turvallisen autentikointi viesitntäkanavan. Tämä digitaalisen salaus menetelmä käyttää tiettyissä tehoissa korotettujen lukujen salauksenpurkuavainta tuottamista. Phase 1 ja 2 neuvottelun tuloksena tulisi olla istuntoavaimen ja yksi kaksisuuntainen SA. Kun phase 1 on konfattu onnistuneesti niin kumppani siirtyvät nopeasti phase 2:lle neuvotteluun. Mikäli jos phase 1 vaihe konffaukset epäonnistuu niin laitteet eivät voi kommunikoida toisensa.

- Phase 2: neuvotellussa sen tarkoituksena on, että kahden vertaisen eli phase 1 ja 2:sen sopivia parameterjä, jotka määrittelevät toisensa, että liikennettä voi kulkea VPN:n kautta ja kuinka liikenne salataan ja todennetaan, siksi tätä kutsutaan turvallisuuden yhdistämiseksi (security association)

Phase 1 ja 2 kokoonpanoja on vastattava tunnelin kummasssakin päässä olevista laitteesta, että suoriutuvat kuin peili mukaisena konffauksena.

## Transport vs tunnel models 
Transport vs tunnel models molempien protokollassa (AH & ESP), voi operoida kahta modeemia <br>

- Transport moodi - aluperäisen IP-otsikon jätetään ehjiksi. Käytetään suojaamaan tiedonsirtoa yhdellä laitteella toiselle laitteelle. 

- Tunnel moodi - koko alkuperäisen pakettin hajautettua ja/tai salattua, mukaanlukien sekä hyötykuorma, että mahdolliset alkuperäiset otsikot. Väliaikaisen IP-otsikkoa lisätään pakettiin siirron aikana. Käytettään tunnelin liikenteelle paikasta toiseen.

# reitittimen komennot ja konffaus

## tarkista määritykset

| komennot | kuvaus |
| ----- | ---------- |
| $show crypto ipsec transform-set  | | 
| $show crypto isakmp sa  | varmistaa, että ISAKMP-tunneli on konfiguroitu/olemassa/luotu | 
| $show crypto ipsec sa   | varmistaa, että IPsec-tunneli on konfiguroitu/olemassa/luotu | 
| $show crypto map  | varmistaa crypto map on konfiguroitu, että IPV4 reititys reititimestä, ipsec-isakmp id, BGP reititys eli tietojen vaihtamista. | 

## reitittimen versio <br>
tarkista routerin security määritys "$show version" <br>

jos puuttuu voidaan määrittää sen securityk9:ksi mikä tais olla oletus nimi. Jokaisen routeri määrityksessä on oma "cLuku"
<br><br>
"license boot module c1900 technology-package securityk9"
<br><br>
jokaisessa routerissa on eriluku toi "c1900" kantsii tarkistaa
<br><br>
jos mielestäsi on oikea valikko sit vaan "yes"
muist tallentaa "$copy run start" tai "write" / "wr"
<br><br>
käynnistä uudelleen "$reload" ja tarkista, että on määritetty securitety licenssi

# IPsec tutoriaalit ja muut guide asiat <br>

https://www.cisco.com/en/US/docs/routers/access/800/850/software/configuration/guide/vpngre.html <br>
https://www.firewall.cx/cisco-technical-knowledgebase/cisco-routers/867-cisco-router-site-to-site-ipsec-vpn.html <br>
https://networklessons.com/cisco/ccie-routing-switching/ipsec-internet-protocol-security <br>
https://kalaharijournals.com/resources/141-160/IJME_Vol7.1_159.pdf <br>
https://cybersecfaith.com/2020/11/01/setting-up-an-ipsec-vpn-using-cisco-packet-tracer/ <br>
https://www.cisco.com/en/US/docs/routers/access/800/850/software/configuration/guide/vpngre.pdf  <br>

## ipsec phase 1 ja 2 ja ike

https://www.watchguard.com/help/docs/help-center/en-US/Content/en-US/Fireware/mvpn/general/ipsec_vpn_negotiations_c.html <br>
https://www.techtarget.com/searchsecurity/definition/Internet-Key-Exchange
