<h1>Langattomat lähiverkot 30.12.2021 </h1>
Harjoituksissa käytettään DCHP verkkoprotokollaa, että määrittyy esim rajoitettu IP-osoite (192.168.0.1 - 192.168.0.50 ja perus aliverkon peite on 255.255.255.0)
Myös fyysisen langallisen/langattoman reitittimelle tulee porttiin määritetty fyysinen IP-osoite

<h2>Langattoman lähiverkon tietoturvat</h2>
Langattoman lähiverkon tietoturva koostuu menetelmistä, joiden tarkoituksena on lisätä tiedonsiirron ja 
kirjautumisen turvallisuutta WLAN-verkoissa. Menetelmät koostuvat yksinkertaisista verkkoonpääsyn 
ja autentikoinnin ratkaisuista sekä moninkertaisesta tiedon salaamisesta.

<h3>Autentikointi & salausprotokollat</h3>
<ul>
<li>WEP (wired Equivalent Privacy)</li>
  <li><dl>
    <dt>WPA (Wi-Fi Protected Access)</dt>
      <dd>WPA2, WPA3</dd>
    </dl></li>
  </ul><br>
  
![Alt text](images/WirelessSecurityType.PNG?raw=true "None")

<b> WPA-PSK </b> - WPA on suunniteltu käytettäväksi 802.1X-todennuspalvelimen kanssa joka jakaa eri avaimet kullekin käyttäjälle. Sitä voidaan kuitenkin käyttää myös vähemmän suojatussa PSK (Pre-Shared Key) -tilassa. PSK on suunniteltu koti- ja pientoimistoverkkoihin joissa jokaisella käyttäjällä on sama salasana. WPA-PSK:ta kutsutaan myös nimellä WPA-Personal. WPA-PSK-tekniikan avulla langaton Brother-laite voidaan liittää tukipisteisiin TKIP- tai AES-salausmenetelmällä. WPA2-PSK-salauksella langaton Brother-laite voidaan liittää tukipisteisiin AES-salausmenetelmällä.

<h1>Langatomien verkkojen protokollat</h1>
Jokaisessa protokollassa voi yritää tuoda esiin oman vahvuus ja heikkoutensa, että kuvailla jotain mahdollisia hyökkäyksiä

<h3>WEP (Wired Equivalent Privacy) </h3>
Se on IEEE:n 802.11-standardin ensimmäinen työaseman ja tukiaseman välistä langatonta tietoliikennettä suojaamaan kehitetty salausmenetelmä. WEP-salauksen on tarkoitus suojata langatonta verkkoa salakuuntelulta ja estää valtuuttamattomilta käyttäjiltä pääsy verkkoon.

WEP yritti rajoittaa pääsyä langattoman verkon tietoihin samalla tavalla kuin langalliset lähiverkot (LAN) suojaavat tietoja. Käyttäjät, joilla on fyysinen pääsy verkon tukiasemiin, ovat ainoita, joilla on pääsy langallisiin verkkoihin. Langattomat verkot, kuten Wi-Fi, käyttävät salausprotokollia, kuten WEP, estääkseen luvattoman pääsyn verkkotietoihin.

WEP <b> yksityisyys (privacy) </b> on alunperin n. 64 bittinen RC4 virran salausavaimen algoritimien kanssa, että langattomasti lähetetyn tiedon salaamista. Protokollan myöhemmät versiot lisäsivät tuen 128-bittisille avaimille ja 256-bittisille avaimille turvallisuuden parantamiseksi. WEP käyttää 24-bittistä alustusvektoria, mikä johti 40, 104 ja 232 bitin tehollisiin avainten pituuksiin. 

WEP <b> tietojen ehesy </b> . WEP käyttää CRC-32-tarkistussumma-algoritmia tarkistaakseen, että lähetetty data on muuttumaton määränpäässään. Lähettäjä käyttää CRC-32:n syklistä redundanssitarkistusta luodakseen 32-bittisen hajautusarvon tietosarjasta. Vastaanottaja käyttää samaa sekkiä vastaanottaessaan. Jos arvot eroavat toisistaan, vastaanottaja voi pyytää uudelleenlähetystä. 

  <hr>

<h3> WPA (Wi-fi Procted Access) 1-3 </h3>
Se on WLAN-verkon käytettävä salausprotokolla ja tätä kehitti aiemmin käytetyn WEP-salauksen ongelmien paljastettua 2000-luvun alussa. WPA julkaistui 2003, Wi-FI Alliance tarkoituksena pitää sitä väliitoimenpiteenä ennakoidakseen turvalllisemman ja monimutkaisemman WPA2 saatavuutta ja WPA2 julkaistui vuonna 2004. Viimeisenä WPA3 julkaistui 1/2018, ja sisältää useita tietoturvaparannusta verrattuna WPA2:seen.


<hr>
  <h3>Access Point & tukiasema/reitittimet </h3>
  Verkkolaiteisto, mitä sallii muita Wi-Fi laiteitta, että voi muodostaa langallisen verkoston kokoonpanon. Erillisenä laitteena tukiasemalla voi olla langallinen yhteys reitittimeen, mutta langattomassa reitittimessä se voi olla myös kiinteä osa itse reititintä. AP on erilainen kuin hotspot, joka on fyysinen sijainti, jossa Wi-Fi-yhteys on käytettävissä.
