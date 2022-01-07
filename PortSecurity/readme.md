<h1>Port security 5.1.2021</h1>

Portin turvallisuus, mikä on Ciscon tuotemerkkin kytkimien <b>porttien turvallisuus</b> käyttö kontrolli ja viitemallien toisen kerroksen eli siirtoyhteyskerros.
Sen avulla, että järjestelmänvalvoja (administrator) voi määrittää yksittäisen kytkinportin sallimista ja tietyn määrän lähde MAC-osoiteitta tunkeutua porttiin.
Sen käyttö estää käyttäjiä lisäämästä kuin "hölmö" kytkmiä laittomasti laajentaakeen verkon kattavutta esim. että 2-3 käyttäjää voivat jakaa yhden pääsyportin.
Hallitsemattomien laitteiden lisääminen vaikeuttaa järjestelmävalvojien suorittamia vianmäärityksiä, että on parasta välttää.

<br>

![Alt text](images/Cisco-portSecurity.PNG?raw=true "None")

Kuka tahansa voi käyttää suojaamattomia verkkoresurssei yksinkertaisesti kytkemällä isäntään johonkin käytetättvien olevista kytkinporteista. Käyttäjä voi myös vaihtaa fyysistä sijaintiaan LAN-verkossa ilmoittamatta asiasta järjestelmänvalvojalle. Portin suojausominaisuuden avulla voit suojata kerroksen kaksi pääsyä ja pitää käyttäjät oikeilla jäljillä.

Switchport eli <b> kytkmien porttien määritykset </b> suojatilojen ja -komentojen selittämisessä käytetään simulaatiota (cisco packet tracer) ohjelmistoa. Myös voi käyttää muita simulaatio ohjelmistoa, tai oikeetta fyysistä Cisco tuotteiden kytkintä ja noudattakseen sitä opastusta. Tulostuksessa ei ole eroa, kunhan valitsemasi ohjelmisto sisältää tässä opetusohjelmassa selostetut komennot.

Kytkimessä voi olla kytkeytty reitittimeen, fyysisen langallisen pöytätietokoneelle, kannettava tietokone, ja muihin liitäntä verkkoon. Näiden fyysisen verkko yhdistelmässä käytetään Ethernet/verkko kaapelia, mitä kytkin käyttää näidhen yhdistettynä laitteiden MAC_osoitetta, jotta tunnistaa ja pyytää palvelun tarjoamista. Näiden porttien turvaaminen on tärkeä tehtävä, jotta vain valtuutetut käyttäjät voivat liittää järjestelmänsä verkkoon kytkimen kautta. Ennen minkään kytkimen määrittämistä organisaatioverkossa otetaan huomioon portin suojaus, koska se varmistaa, että aito ja valtuutettu käyttäjä on yhteydessä verkkoon. Tämä Cisco IOS Switches -suojausominaisuus voidaan määrittää vain pääsyportteihin, ja oletusarvoisesti tämä ominaisuus on poistettu käytöstä. 

<h2>Konfigurointi </h2>

Kytkimien käyttöönottossa Cisco laiteissa, mitä pitää varmistaa, että on tietojen luottamuksellisuus, aitous ja eheyksen säilytys.

<h3>Tärkeät moodit</h3>

<dl>
  <dt>Protect</dt>
    <dd>Tätä tilaa käytettäessä ilmoitusviestiä ei lähetetä, kun tämä rikkomus tapahtuu & tilassa datapaketit määrittyy MAC-osoitteiden siirtämistä vain verkon sisällä</dd>
    
  <dt>restrict</dt>
    <dd>Kun rikkomus tapahtuu tässä tilassa, kytkinportti sallii liikenteen tunnetuista MAC-osoitteista 
jatkaa liikenteen lähettämistä samalla kun liikennettä pudotetaan tuntemattomista MAC-osoitteista. 
Toisin kuin suojausrikkomustyyppi, lähetetään myös viesti, joka ilmoittaa rikkomuksesta. &
      
 Kun tämä moodi on käytössä ja portin suojausta rikotaan, kaikki tiedonsiirto estetään ja paketit putoavat. 
Myös lokit luodaan samanaikaisesti, jotta voidaan tarkistaa, mikä laite on yhdistetty Cisco-kytkimelle</dd>
    
  <dt>shutdown</dt>
    <dd>Kun tässä tilassa tapahtuu rikkomus, kytkinportti poistetaan käytöstä ja asetetaan error-disabled -tilaan. 
Kytkentäportti pysyy tässä tilassa, kunnes se poistetaan manuaalisesti; tämä on oletusportin suojausrikkomustila. & 
      
Tämän moodi on oletusarvoisesti käytössä ja portin tilaksi muutetaan error-pois käytöstä, 
mikä rajoittaa kytkettyä laitetta suorittamasta mitä tahansa toimintoja ja poistaa myös kyseisen portin käytöstä</dd>
</dl>

<h2>MAC-osoite</h2>

Avaa koneesta cmd, ja syötä komento kuin "ipconfig /all"
mitä avaa IP-osoitteiden määritykset ja muut yksityiskohdan ominaisuudet.
myös TCP/IP konfiguroinnin kaikki adapterit

Kohde on kuin (physical address : abcd.pälä.pälä)

<b> HUOM! </b> varsinainen windows cmd on eri näköinen ja tämä on simulaatio
Varsinaisen MAC-osoite on 12 numeorinen esim: 00:1A:C2:7B:00:47
Tätä lukua tai määritystä tulostuu myös langattomana, että langallisena verkkona

myös jokaisella fyysisellä osoite on eri ja se on sama kuin mac-osoite koska sitä käytetään kommunikoimalla laitteiden välisen Ethernet verkoa.

Kun lähetetään pyyntö etäisännän IP-osoitteeseen (esim. verkkosivustolle), tietokoneesta lähettää pyynnän lähiverkon yhdyskäytävään (default gateway),
ja se käyttää fyysistä MAC osoiteitta viestin kohteena, mutta looginen IP osoite lopullisen määränpään isäntäosoite. 

Reititin välittää sitten viestin eteenpäin, ja tietää kenelle vastauksen palautetaan
 
<br>

<h2>Maximum number </h2>

Kytkin määrityssä tulee rajoittaa isäntien enimmäismäärää (maximum number)
numerot ovat 1 - 132
Vaatimuksessa mukaan voidaan rajoittaa rajapinnan liittyvien isäntien määrää.

Asettamisessa tämä rajan, mitä mihin tahansa välillä 1 - 132.
Rajapinnan liitettään laitteiden maksimi määrä on 132 ja oletus arvo on 1.
switchport määrityksessä maksimiarvo komento asettaa isäntien ensimmäismäärän

<br>

<h2>Konfiguroinnin jälkeen</h2>

Määritetyissä konfiguroinissa menee, että jokaisen portin tulee määrittää se (port security)
myös voi olla fyysistä, koska verrattuna trunk ja access,
mitä voidaan rajata (range), että on useampi portti kuin yksi portti

Konfiguroinnun jälkeen kannattaa pinggata, että viesti kulkeutuu oletusyhdyskäytävään, koska kytkimen port-security:n kohteen koneessa tapahtuu pientä muutosta.
<br>
Että kytkin portti fa 0/x ------- kone, välisessä port-security on joko <b> Enabled / käytössä </b> tai <b> Disabled / liikumisrajoitteinen </b>

$sh port-security interface fa (port/number)

$show port-security address

taulukkosa näyttöö mac osoitteen koneen ja tyyppin, että onko staatinen vai dynaaminen, että kytkimen portti kohde
$sh mac address-table

port security poistaminen
$no switchport port-security
