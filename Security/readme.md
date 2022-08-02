- [Security (tietoturva)](#Security-(tietoturva))
- [VPN (virtual private network)](#VPN-(virtual-private-network))
  * [VPN tyyppit](#VPN-tyyppit)
   * [Remote access](#Remote-access)
   * [Site-to-site VPN](#Site-to-site-VPN)
   * [Personal VPN services](#Personal-VPN-services)

# Security (tietoturva)

Tänne tulee kytkimen & reitittimen tietoturva konffaukset kuten palomuurit, ssh, telnet ja jne, kuten pääsyhallinat ja muut käyttäjien todentamisen tunnukset. esim. ssh käyttäjäntunnus, ja salasana.

sama vaikuttaa host käyttäjä esim. yrittää käydä kiinni käsiksi kytkimen/reitittimeen sisään käsiksi, että tarkistettaan sisäisen kytkimen rakenne, ominaisuus, mitä on konfiguroitu ja mitä porttit ovat päällä/pois päältä, ja muut virheet. Toki varsinaisesti kytkimen konfiguroinnista ei nähdä varsinaisesti sitä virheilyä, mutta mikäli sattuu sähkö häiriötä vasta sen jälkeen voidaan epäillä sitä oiretta. Oireita voi olla monipuolisia esim. pinggaus, palomuuri / oikeudet, tai muu sähkö häiriön este.

| Security protkollia on: |  IPsec <br> GRE <br> ISAKMP  <br> NTP <br> AAA <br> RADIUS <br> TACACS <br> SNMP <br> SSH <br> Syslog <br> CBAC <br> Zone-Based Policy Firewall  <br> IPS |
| ---------- | ---------- |

# VPN (virtual private network)
virtuaalinen erillisverkko on tapa, jolla kaksi tai useampia yrityksen verkkoja voidaan yhdistää julkisen verkon yli muodostaen näennäisesti yksityisen verkon. Nykyisin VPN-määritelmä on laajennettu koskemaan myös yksittäisten etätyöasemien liittämistä yrityksen verkkoon.

VPN-verkon yksityisyys ja tietoturva voidaan hoitaa joko fyysisesti tai salauksella. Asiakkaan verkkoja yhdistävä VPN voi siis perustua jommallekummalle seuraavista:

- Perinteiset suljetut verkot, kuten operaattoriverkot fyysisellä suojauksella
- Julkiset ja avoimet verkot, kuten salattu Internet
- 
<img src="images/VPN-diagram1.PNG" width="500">

Myös vaikuttaa palomuurien määrityksiin, kuten työpaikan salaisia asioita, mitä ei julkaista ulkopuolisille asiakkaalle tai yrityksille.

Runkoverkoissa käytetään useimmiten useiden asiakkaiden liikenteen erotteluun MPLS:ää, ATM:ää tai yksinkertaisimmillaan IP-osoitekohtaisia pääsylistoja.

IPsec-protokollaa käytetään suljetuissa operaattori-VPN:issä, muttei tietoturvan vaan konfiguroinnin vuoksi. IPsec-tunneleiden konfigurointi operaattorin runkoverkon reunareitittimien välillä yksinkertaistaa konfiguraatiota IP-pääsylistoista huomattavasti, ja ei ole riskiä, että asiakkaiden verkkojen liikenteet pääsisivät sekaantumaan. IPsec on protokollana todistettu kohtalaisen turvalliseksi ja hyvä ohjelmistotuki on antanut sille jalansijan moniin muihinkin käyttötarkoituksiin VPN:ien lisäksi. Muun muassa langattomissa WLAN-lähiverkoissa voidaan käyttää joko WLAN:ien omien suojausten sijasta tai lisäksi IPsec-protokollaa.

<b> VPN tunneli kaavio </b> <br>
<img src="images/VPN-diagram2.PNG" width="500">

## VPN tyyppit

### Remote access

<img src="images/VPN_remoteaccess.PNG" width="500">

### Site-to-site VPN

Yrityksellä laajentuu jatkuvasti/usein eri osastoon, ja kahden tai useamman aloilla/osastoiden välillä siirrettään jatkuvasti tiedostoi suojaamista, minkä on otettava käyttöön paikallisen VPN. Yleisen sivustojen välisessä VPN:ssä on käytetyt VPN-protokollat eli IPSec (Internet Secuirty Protocol). Tämän tyyppisen VPN:n toteuttamiseksi meidän on määritettävä vaiheen (Phase) 1 ja vaiheen (Phase) 2 VPN-neuvottelut. IKE Phase 1 -neuvottelu on paikka, jossa luomme suojatun salatun kanavan tai salatun verkkoyhteyden kahdelle palomuurille, jotka voivat aloittaa vaiheen 2 neuvottelun.

IKE Phase 2 -neuvotteluissa kaksi palomuuria sopivat konfiguroiduista parametreista, jotka määrittävät, mitä liikennettä voi kulkea VPN-tunnelin kautta ja kuinka liikenne todennetaan ja salataan. Sopimus on nimeltään Security Association. Sekä Vaiheessa 1 että Vaiheessa 2 tulee olla samat parametrit, kuten esijaetut avaimet, todennus, salaus ja IKE-versio.

<img src="images/VPN_sitetosite.PNG" width="500">

On kaksi tapaa ottaa käyttöön sivustojen välinen VPN:

- Intranet VPN - tarjoaa suojatun toimipisteen välisen yhteyden yrityksien sisällä tai sisäisesti
- Extranet VPN - tarjoaa suojatun toimipisteen välillä yhteyden yrityksien ulkopuolella. esim. asiakkaan tai kumpannit voivat käyttää turvallisesti yrityksen yhteystä resurssia.

<img src="images/VPN_sitetosite2.PNG" width="500">

### Personal VPN services

# Linkkit ja lukemista vähän: <br>
https://www.cisco.com/c/dam/en_us/training-events/netacad/course_catalog/docs/CCNAsecurity_DS.pdf <br>
https://staffweb.itsligo.ie/staff/pflynn/Telecoms%203/CCNP%202%20Secure%20WAN%27s/Secure%20Converged%20Networks/CCNA%20Security.pdf <br>
https://nanopdf.com/download/ccna-security_pdf <br>

https://www.cisco.com/c/dam/en_us/training-events/le21/le34/downloads/689/academy/2008/sessions/BRK-134T_VPNs_Simplified.pdf

