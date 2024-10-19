- [Cisco packet tracer simulation](#Cisco-packet-tracer-simulation)
  * [Cisco Packet tracer protokollat](#cisco-packet-tracer-protokollat)
  * [Cisco packet tracer laiteistot mallit](#cisco-packet-tracer-laiteistot-mallit)
 - [Other Simulation software by using Cisco materials](#Other-Simulation-software-by-using-Cisco-materials)

# Cisco packet tracer simulation
Cisco packet tracer kertausta ja harjoitusta itsenäisesti & sekä vähän uutta tarvittaessa <br>

![Alt text](kuvat/CiscoPacketTracer-1.PNG?raw=true "None")

<br>

## Cisco Packet tracer protokollat

![Alt text](kuvat/CPT-protocols.PNG?raw=true "None")

<hr>

## Cisco packet tracer laiteistot mallit
<br>
Reititin

![Alt text](kuvat/cisco-packet-tracer-devices-2.PNG) <br>

<br>
Kytkimet

![Alt text](kuvat/cisco-packet-tracer-devices-1.PNG) <br>

<br>
Muut laitteet:

![Alt text](kuvat/cisco-packet-tracer-devices-3.PNG)
![Alt text](kuvat/cisco-packet-tracer-devices-4.PNG)


# Reititimen, kytkimen, tietoturva (security) ja muu konffaus, myös IoT, WLAN, Server ja muu verkon protokollan määritys

<b> Pieni huomio; </b> Kotona, toimistolla/koulussa niin on usein Private IP-osoite, jotka eivät suoraan sanansanalla ole yhteydessä verkkoo (internettiin) vaikka usein verkkokorttista lukee `$ipconfig` niin vaikka sielä lukisi 192.x.x tai 10.x.x. tai jopa 172.x.x jotakin. Se on se palvelutarjoaja mikä tarjoaa julkinen IP-osoiteen, toisaalta kotona kun mennään internettiin niin pitää mennä NAT reitityksen kautta. Tämä tarkoittaa NAT muuntaa private IP-osoitteesta julkiseksi IP-osoitteeksi, näin se tapahtuu verkkojen yhteyksillä. 

Onhan mahdollista hakea googlesta mikä se oman julkisen IP-osoite onkaan ja/tai vaihtoehtona on powershell/cmd:stäkin hakea/tarkista oman julkisen ip-osoite komennolla. Tämä on powershell komento `$Invoke-WebRequest -Uri "http://api.ipify.org" | Select-Object -ExpandProperty Content`

Tämä koskee sama ideana Azure, aws ja google pilvipalveluita.

![Alt text](kuvat/IMG_20191101_140519.jpg?raw=true "None")

# Other Simulation software by using Cisco materials

Olemassa on muitakin kuin Cisco packet tracer simulaatio sovellus, että sisäisen ohjelmistossa puuttuu jotakin määrityksiä ja tueta sisällä. Myös realistisessa Cisco:n laiteesa voidaan määrittää niitä protokollia. On olemassa useita simulaatio sovelluksia, että sisällä on valmiit ominaisuudet, tuet ja muut protokollan tarvittavat tarvikkeet, että kuin toimii realisisten reitittimen/kytkimen konfiguroinnin ympäristössä.
<br><br> 
https://www.netacad.com/courses/packet-tracer (tämä on Cisco packet tracer) <br>
https://www.eve-ng.net/ <br>
https://www.gns3.com/<br>

# Cheat sheet komennot ja muut lunttilaput & guide & chapter materiaalit:
https://www.ii.pwr.edu.pl/~kano/index.html <br>
https://packetlife.net/library/cheat-sheets/ <br>
https://slideplayer.com/slide/3561082/ <br>
https://data.kemt.fei.tuke.sk/PocitacoveSiete/_materialy/Prednasky/ <br>
https://www.routeralley.com/guides/ <br>
https://ipcisco.com/protocol-cheat-sheets/ <br>
http://vapenik.s.cnl.sk/pcsiete/ <br>
