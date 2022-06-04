# Firewall - palomuuri


<img src="images/Firewall-1.png" width="500">

<img src="images/Firewall-2.png" width="500">

- [Cisco packet tracer](#Cisco-packet-tracer)
- [Security level](#Security-level)
- [NAT](#NAT)
- [Object group for acl](#Object-group-for-acl)
- [Service Policy](#Service-Policy) 
  * [Policy map and class](#Policy-map-and-class)
  * [](#)
  * [inspect tekijät](#inspect-tekijät)
- [guide, oppaat ja konfiguroinnit:](#guide,-oppaat-ja-konfiguroinnit)
  * [asa 5505](#asa-5505)
  * [Tunnel Groups and group policies](#Tunnel-Groups-and-group-policies)
  * [konfiguraatiot:](#konfiguraatiot:)

# Cisco packet tracer

CIsco simulaatiossa on kaksi tyypistä palomuuri kytkintä (5506-x ja 5505), mutta todellisuudessa voi olla useampi mallinen, että nämä kaksi tukee simulaatiossa. Nimeämisessä käytettään *ASA* eli Adaptive Seuciryt appliances, ja 5506-x on wifi point mukana.

5505 - palomuuri kytkimessä on oletuksena valmiina VLAN 1 ja 2 valmiina, sekä VLAN 1 on määritetty oletuksena (nameif inside, seucrity-level 100, ip add 192.168.1.1 255.255.255.0) ja VLAN2 (nameif outside, security level 0). Muut määrityksessä on dhcp add 192.168.1.5 - 192.168.1.6 inside, dhcp sallii "inside", portti int Eth0 sallii vlan 2.

# Security level

Cisco ASA palomuurissa käytettään ns. security level, suomeksi. turvataso, joka osoittaa kuinka luotettava käyttöliittymä on verrattuna toiseen käyttöliittymän. Mitä korkeampi suojataso on, sitä luotettavampi käyttöliitymä on. Jokaisessa ASA:n liitännässä on suojausvyöhyke, sitä käyttämällä suojataso on eri luottamustasoinen suojavyöhyke.

Korkealla suojaustasolla varustettu käyttöliittymä voi päästä matalan suojaustason liitäntään, mutta päinvastoin ei ole mahdollista, ellemme määritä käyttöoikeusluetteloa, joka sallii tämän liikenteen.

<b>Security level 0</b> : alhaisin suojataso, ja oletusarvoinen määritetty ns. ulkopuoliselle rajapinnalle. Alemmassa suojatasossa ei rajapintaa, koska tämä tarkoittaa, että ulkopuolelta (outside) tuleva liikenne ei pääse tavoittamaan mitään rajapintoja ja ellei salli sitä pääsyluetteloa (access-list)

<b>Security level 100</b> : ASA:n korkein suojataso, ja oletuarvoinen määritelmä (inside) käyttöliitymille. Normaalisti käytämme LAN-verkossa, ja tämä on korkein suojataso, ja voi saavuttaa oletuksen kaikki muihin liitäntään.

<b>Security level 1-99</b> : Luonnissa voi vapaasti luoda mitä tahansa muita haluamansa suojaustason, esim. voi käyttää suojaustasoa 50 DMZ:lle. Tämä tarkoittaa, että liikenne on sallittua sisäverkostomme DMZ:lle (turvataso 100 -> 50) ja myös DMZ:ltä ulkopuolelle (turvataso 50 -> 0). Liikenne DMZ:stä ei voi kuitenkaan voi mennä sisälle, että ilman käyttöoikeusluetteloa (access-list). Koska turvataso 50 tuleva liikenne ei saavutta suojaustasoa 100. Suojaustasoa voi luoda useamman määrän (inside, outside) kappaletta. 

DMZ on demilitarisoitu alue (dimilitarized zone), ja tarkoittaa fyysistä tai loogista aliverkkoa, mitä yhdistää organisaation oman järjestelmän turvattovampaan alueeseen, esim. internetiin. Demilitarisoidun alueen tarkoitus on lisätä ylimääräinen tietoturvataso organisaation lähiverkkoon.

<img src="images/Firewall-inAndout1.png" width="500">

# NAT

NAT (network address translation) osoitteenmuutos, mitä tuttu "inside" ja "outside", sekä PAT. Lyhyesti sisäisen salainen ja julkinen IP-osoite kuten Internet sivustot, ja vaikutava muu määritys.

# Object group for acl

ACL eli access-list. Hallitsevissa Cisco ASA-palomuurissa, mitä takana voi olla satoja tietokonen käyttäjiä, ja kymmensiä palvelimia, ja jokaisessa laitteessa vaaditaan pääsyluettelosääntö (access-list rule), jotka sallivat tai estävän liikenteen.

Monilla laitteilla on tulee antaa kuin käyttöoikeusluettelo lausekkeita, ja käyttöoikeusluettelon lukemista, ymmärtämistä ja päivittämisessa voi olla hallinnollinen painajainen.

Objektiryhmä mitä tulee luoda ns. "ryhmityvä" objekti, mitä voi olla kokoelma IP-osoitte, verkko, porttinumero ja muu. Luomisen pääsyluettelo, mitä on monenlaisia eri käskyjä, sitä voidaan viitata objektiryhmään. Tämä tekee pääsyluettelosta pienemmän ja helpmman luettavan. Aina, kun tekee muutoksia objektiryhmään, mitä näkyvät myös käyttöoikeusluettelossa.

Konfiguroinnin sisällä tapahtuu inside/outside luonti objekti 5505 firewall kytkimessä ja saman aikaisesti NAT (inside,outside) dynaaminen interface: <br>
ciscoasa(config)#object network ? <br>

configure mode commands/options: <br>
  WORD  Specifies object ID (1-64 characters) <br>
<br>
ciscoasa(config)#object network inside-net <br>
	
ciscoasa(config-network-object)#subnet 192.168.1.0 255.255.255.0 <br>
ciscoasa(config-network-object)#nat (inside,outside) dynamic interface <br>
<br>
tarvittaessa tarkista nat  ($show nat) <br>
ciscoasa#show nat <br>
Auto NAT Policies (Section 2) <br>
1 (inside) to (outside) source dynamic inside-net interface <br>
    translate_hits = 0, untranslate_hits = 0 <br>

# Service Policy

Modular Policy Frameworkia käyttävät palvelukäytännöt tarjoavat johdonmukaisen ja joustavan tavan määrittää ASA-ominaisuudet. Tätä voi käyttää palvelukäytäntöä luodaksesi tietylle TCP-sovellukselle ominaisen aikakatkaisukokoonpanon, toisin kuin kaikkia TCP-sovelluksia koskevan konfiguraation. Palvelukäytäntö koostuu useista toiminnoista tai säännöistä, joita sovelletaan käyttöliittymään tai sovelletaan maailmanlaajuisesti.

## Policy map and class

## konffaus toiminnat

## inspect tekijät
<br>
ciscoasa(config-pmap-c)#inspect ? <br>
 mode commands/options: <br>
  dns   <br>
  ftp   <br>
  h323  <br>
  http  <br>
  icmp  <br>
  tftp  <br>

# guide, oppaat ja konfiguroinnit: <br>

https://www.cisco.com/c/en/us/td/docs/security/asa/asa96/configuration/firewall/asa-96-firewall-config.pdf <br>
https://ipwithease.com/asa-firewall-security-levels/ <br>
https://www.cisco.com/c/en/us/support/docs/security/asa-5500-x-series-next-generation-firewalls/115904-asa-config-dmz-00.html <br>
https://networklessons.com/cisco/asa-firewall/introduction-to-firewalls <br>

## asa 5505

https://www.routerfreak.com/basic-configuration-tutorial-cisco-asa-5505-firewall/ <br>

## Tunnel Groups and group policies
https://www.dasblinkenlichten.com/tunnel-groups-and-group-policies-on-the-asa/ <br>

## konfiguraatiot: <br>

https://www.grandmetric.com/knowledge-base/design_and_configure/how-to-configure-security-level-and-nameif-on-cisco-asa/






