<h1>ACL (access control lists) Käyttäjäoikeuslista </h1>

Käyttäjän pääsy oikeudet, että määrittää tulee määrittää pieni aliverkon määrä eli tuttu 255.2555.255.252 ja jne. Myös vaikutta rajopitettu määrä IP-osoite, ketkä voivat pinggata, ja mihin asti pääsevät.
Myös, että tietty määrä IP-osoite ovat määritetty joukko <b> lupa = permit </b> & <b>deny = kieletty </b>

![Alt text](images/ACL-Example.png?raw=true "None")

# 1-99 standard acl
applied closes to the destination <br>
<br>
Jos haluaa suodata osan lähiosoitetta, tavallisen käyttöoikeudenluettelon on yksinkertainen ja riittävä.  <br>
Tavallisen käyttöoikeusluetteloita on kaksi tyypistä: nimetty ja numeroitu. <br><br>

Nimettyjenkäyttöoikeusluettelossa inutiivisilla nimellä kuin numeroina, ja ne tukevat enemmin ominaisuuksia kuin numeroidun käyttöoikeusluettelot.
<br><br>

# 100 - 199 extended acls
applied  closest to the source

määrityksessä kulkeuttuu, että kone sallittaan tai kieletty menemään sovelluskerrokseen, mitä on kuten http (80) / https (443), telnet (23, pääteyhteys internetin ylitse) ja yms protokollat. Sama vaikuttaa pinggaukseen, että onko kyseisen IP-osoittelle yksittäinen vai ryhmitetty joukko, mitä määritetty käyttäjäoikeus.

![Alt text](images/ACL-extended-Ports.PNG?raw=true "None")

# Syntax
Jokin porttille syntaksi 
in - arkoittaa määritystä, että ACL koskee saapuvaa liikennetä

out - tarkoittaa määritystä, että ACL koskee lähtevää liikennetä

# Wildmask calculation
Täyden aliverkko peitte on maksimissaan täys 32-bittinen on, mitä tarkoittaa 255.255.255.255 ja binääri menetelmässä 1 & 0 ( 11111111. 11111111. 11111111. 11111111) ja myös 24-bittinen, mitä täsmää aliverkkon 255.255.255.0 (11111111.11111111.11111111.00000000) ja jne. 

Lasku menetelmässä laskeuttuu täys 32-bittinen vähennettään (-), sitä määritettyä aliverkkon summaa PC kone sisäisen oma aliverkko peite eli esim. /28 (255.255.255.240), mitä jäljellä on enään 0.0.0.15

Lasku toimitus: 32-bittinen on (255.255.255.255) - 28-bittinen (255.255.255.250) = 0.0.0.15

![Alt text](images/ACL-WildcardMask.PNG?raw=true "None")
![Alt text](images/ACL-WildcardMask-example.PNG?raw=true "None")

<h2>Inbound ACL & Outbound ACL</h2>
<br>
<b>Inbound </b> - mitä kuin saapuvat paketit käsittellään ennen kuin ne reititettään lähtevään rajapintaan.<br>
<b>Outbound </b> - mitä saapuvat paketit reitietään lähtevään rajapintaan, ja ne käsittellään lähtevän ACL:n kautta. <br>



