- [Security (tietoturva)](#Security-(tietoturva))
- [VPN (virtual private network)](#VPN-(virtual-private-network))
  * [VPN tyyppit](#VPN-tyyppit)

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

Myös vaikuttaa palomuurien määrityksiin, kuten työpaikan salaisia asioita, mitä ei julkaista ulkopuolisille asiakkaalle tai yrityksille.

Runkoverkoissa käytetään useimmiten useiden asiakkaiden liikenteen erotteluun MPLS:ää, ATM:ää tai yksinkertaisimmillaan IP-osoitekohtaisia pääsylistoja.

IPsec-protokollaa käytetään suljetuissa operaattori-VPN:issä, muttei tietoturvan vaan konfiguroinnin vuoksi. IPsec-tunneleiden konfigurointi operaattorin runkoverkon reunareitittimien välillä yksinkertaistaa konfiguraatiota IP-pääsylistoista huomattavasti, ja ei ole riskiä, että asiakkaiden verkkojen liikenteet pääsisivät sekaantumaan. IPsec on protokollana todistettu kohtalaisen turvalliseksi ja hyvä ohjelmistotuki on antanut sille jalansijan moniin muihinkin käyttötarkoituksiin VPN:ien lisäksi. Muun muassa langattomissa WLAN-lähiverkoissa voidaan käyttää joko WLAN:ien omien suojausten sijasta tai lisäksi IPsec-protokollaa.

## VPN tyyppit

- Remote access
- Site-to-site
- Extranet-based site-to-site

# Linkkit ja lukemista vähän: <br>
https://www.cisco.com/c/dam/en_us/training-events/netacad/course_catalog/docs/CCNAsecurity_DS.pdf <br>
https://staffweb.itsligo.ie/staff/pflynn/Telecoms%203/CCNP%202%20Secure%20WAN%27s/Secure%20Converged%20Networks/CCNA%20Security.pdf <br>
https://nanopdf.com/download/ccna-security_pdf <br>



