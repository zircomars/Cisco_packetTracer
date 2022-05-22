# Fireweall - palomuuri


<img src="images/Firewall-1.PNG" width="500">

<img src="images/Firewall-2.PNG" width="500">

- [Cisco packet tracer](#Cisco-packet-tracer)
- [Security level](#Security-level)
- [guide, oppaat ja konfiguroinnit:](#guide,-oppaat-ja-konfiguroinnit)
  * [asa 5505](#asa-5505)
  * [konfiguraatiot:](#konfiguraatiot:)

# Cisco packet tracer

CIsco simulaatiossa on kaksi tyypistä palomuuri kytkintä (5506-x ja 5505), mutta todellisuudessa voi olla useampi mallinen, että nämä kaksi tukee simulaatiossa. Nimeämisessä käytettään *ASA* eli Adaptive Seuciryt appliances, ja 5506-x on wifi point mukana.

# Security level

Cisco ASA palomuurissa käytettään ns. security level, suomeksi. turvataso, joka osoittaa kuinka luotettava käyttöliittymä on verrattuna toiseen käyttöliittymän. Mitä korkeampi suojataso on, sitä luotettavampi käyttöliitymä on. Jokaisessa ASA:n liitännässä on suojausvyöhyke, sitä käyttämällä suojataso on eri luottamustasoinen suojavyöhyke.

Korkealla suojaustasolla varustettu käyttöliittymä voi päästä matalan suojaustason liitäntään, mutta päinvastoin ei ole mahdollista, ellemme määritä käyttöoikeusluetteloa, joka sallii tämän liikenteen.

<b>Security level 0</b> : alhaisin suojataso, ja oletusarvoinen määritetty ns. ulkopuoliselle rajapinnalle. Alemmassa suojatasossa ei rajapintaa, koska tämä tarkoittaa, että ulkopuolelta (outside) tuleva liikenne ei pääse tavoittamaan mitään rajapintoja ja ellei salli sitä pääsyluetteloa (access-list)

<b>Security level 100</b> : ASA:n korkein suojataso, ja oletuarvoinen määritelmä (inside) käyttöliitymille. Normaalisti käytämme LAN-verkossa, ja tämä on korkein suojataso, ja voi saavuttaa oletuksen kaikki muihin liitäntään.

<b>Security level 1-99</b> : Luonnissa voi vapaasti luoda mitä tahansa muita haluamansa suojaustason, esim. voi käyttää suojaustasoa 50 DMZ:lle. Tämä tarkoittaa, että liikenne on sallittua sisäverkostomme DMZ:lle (turvataso 100 -> 50) ja myös DMZ:ltä ulkopuolelle (turvataso 50 -> 0). Liikenne DMZ:stä ei voi kuitenkaan voi mennä sisälle, että ilman käyttöoikeusluetteloa (access-list). Koska turvataso 50 tuleva liikenne ei saavutta suojaustasoa 100. Suojaustasoa voi luoda useamman määrän (inside, outside) kappaletta. 

DMZ on demilitarisoitu alue (dimilitarized zone), ja tarkoittaa fyysistä tai loogista aliverkkoa, mitä yhdistää organisaation oman järjestelmän turvattovampaan alueeseen, esim. internetiin. Demilitarisoidun alueen tarkoitus on lisätä ylimääräinen tietoturvataso organisaation lähiverkkoon.

<img src="images/Firewall-inAndout1.PNG" width="500">


# guide, oppaat ja konfiguroinnit: <br>

https://www.cisco.com/c/en/us/td/docs/security/asa/asa96/configuration/firewall/asa-96-firewall-config.pdf <br>
https://ipwithease.com/asa-firewall-security-levels/ <br>
https://www.cisco.com/c/en/us/support/docs/security/asa-5500-x-series-next-generation-firewalls/115904-asa-config-dmz-00.html <br>
https://networklessons.com/cisco/asa-firewall/introduction-to-firewalls <br>

## asa 5505

https://www.routerfreak.com/basic-configuration-tutorial-cisco-asa-5505-firewall/<br>

## konfiguraatiot: <br>

https://www.grandmetric.com/knowledge-base/design_and_configure/how-to-configure-security-level-and-nameif-on-cisco-asa/






