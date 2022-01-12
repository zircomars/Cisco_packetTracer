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

<hr>

<h2>MAC-osoite</h2>

Avaa koneesta cmd, ja syötä komento kuin "ipconfig /all"
mitä avaa IP-osoitteiden määritykset ja muut yksityiskohdan ominaisuudet.
myös TCP/IP konfiguroinnin kaikki adapterit

Kohde on kuin (physical address : abcd.pälä.pälä)

Kytkin portin suojaus rajoittaa portien sallittujen kelvollista MAC_osoitteen määrää. Kun MAC-osoite tai MAC-osoitteen ryhmä on määritetty ottamaan käyttööön kytkimen portien suojaus, kytkin välittää paketit vain niitä määritettyä MAC-osoitteita portin laitteille. Kytkin hylkää uusia tai toisia laitteita tulevia paketia heti, kun ne saapuvat kytkin portille.

Jos rajoittaa portien sallittua MAC-osoiteitta, mitä osoitteiden määärä tulee olemaan vain pakollinen yksi kytkimien portteista, että saa portin täyden kaistanleveyden.

Jos suojattun MAC-osoite enimmäismäärä on saavutettu, mitä tapahtuu suojarikkomus, kun laiteelle saappuu eri MAC-osoite ja kyseisen liittyvä portti. Usein nyky skenaarioissa, kun kytkin havaitsee tietoturvaloukkauksen, mitä kytkin sulkee portin automaattisesti. Kytki voi määrittäää suojaaman tai rajoittaman vain kyseisen porttin.

<b> HUOM! </b> varsinainen windows cmd on eri näköinen ja tämä on simulaatio
Varsinaisen MAC-osoite on 12 numeorinen esim: 00:1A:C2:7B:00:47
Tätä lukua tai määritystä tulostuu myös langattomana, että langallisena verkkona

myös jokaisella fyysisellä osoite on eri ja se on sama kuin mac-osoite koska sitä käytetään kommunikoimalla laitteiden välisen Ethernet verkoa.

Kun lähetetään pyyntö etäisännän IP-osoitteeseen (esim. verkkosivustolle), tietokoneesta lähettää pyynnän lähiverkon yhdyskäytävään (default gateway),
ja se käyttää fyysistä MAC osoiteitta viestin kohteena, mutta looginen IP osoite lopullisen määränpään isäntäosoite. 

Reititin välittää sitten viestin eteenpäin, ja tietää kenelle vastauksen palautetaan

<hr>

<h2>Suojatut MAC-osoitte tyypit/moodit</h2>
<ul>
  <li>Staatinen</li>
    Konfigurointi suoriuttuu manuaalisesti kytkimien porttien suojauksella, että määrittyy porttiin suorittuu määritetty kohteen konen mac-osoite. Tämä mac osoite tallentuu kytkimen mac-osoite taulukkoon, että kytkin käynnissä olevista kokoonpanoista.
  
  <li>Dynaaminen </li>
  Dynaamisessa kytkin pyrii oppii dynaamisesti, ja tallentaa mac-osoite taulukkoon. Ne poistaa kokoonpanosta, kun kytkin käynnistyy uudelleen.
  
  <li><i> Pysyvä / turvallinen moodi</i></li>
  Pysyvä tai tallentava moodi, mitä suoriuttuu kuin dynaaminen suojatut mac-osoitteet. MAC-osoite suoriuttuu dyynamisesti, ja ne tallentuvat käynnistä olevia kokoonpannoissa.
  
</ul>

<h3>Pysyvä / turvallisuuden moodin ominaisuudesta </h3>

<ul>
  <li>Dynaamisen moodissa saa opittua sen konfiguroinnin, ja muunettaan pysyviksi suojatuksi MAC-osoiteeksi, ja tallentaa käynnissä olevan kokoonpanon</li>
  <li>Jos käyttäjä poistaa pysyvän määrityn mac-osoitteen käytöstä, se määrityn mac-osoiteen taulukko ja muut poistuvat kokoonpanosta</li>
  <li>Jos käyttäjä poistaa kytkimen portin suojatun käytöstä, mitä pysyvä suojatu MAC-osoite pysyvät käynnissä olevissa määrityksissä.</li>
  <li>Jos tallentaa osoitteeet asetustiedostoon, mitä kytkin ei tarvitse määrittää uuuta osoitetta uudestaan ja kytkintä ei tarvitse uudelleen käynnistyä tai sammuttaa käyttöliittymää</li>
</ul>

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

<br>

taulukkosa näyttöö mac osoitteen koneen ja tyyppin, että onko staatinen vai dynaaminen, että kytkimen portti kohde <br>
$sh mac address-table

$sh mac address-table ? 
-- dynamic -- dynamic entry type
-- interfaces -- interface entry type
--static -- static entry type

<br>
port security poistaminen <br>
$no switchport port-security

<hr>

<h2>Muu lisä ohje ja linkkit</h2>
Konffauksen käyttölittymät ja komennot:
https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst4500/12-2/20ewa/configuration/guide/conf/port_sec.pdf
https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst4500/12-2/25ew/configuration/guide/conf/port_sec.html

https://www.certificationkits.com/cisco-certification/ccna-articles/cisco-ccna-switching/cisco-ccna-port-security-and-configuration/
www.certificationkits.com/cisco-certification/ccna-articles/cisco-ccna-switching/cisco-ccna-port-security-and-configuration/
https://study-ccna.com/cisco-port-security-violation-configuration/
https://study-ccna.com/port-security/
https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst2960l/software/15-2_7_e/configuration_guide/sec/b_1527e_security_2960l_cg/port_security.html
