<h1>ACL (access control lists) Käyttäjäoikeuslista </h1>

Käyttäjän pääsy oikeudet, että määrittää tulee määrittää pieni aliverkon määrä eli tuttu 255.2555.255.252 ja jne. Myös vaikutta rajopitettu määrä IP-osoite, ketkä voivat pinggata, ja mihin asti pääsevät.
Myös, että tietty määrä IP-osoite ovat määritetty joukko <b> lupa = permit </b> & <b>deny = kieletty </b>

![Alt text](images/ACL-Example.png?raw=true "None")

# 1-99 standard acl
applied closes to the destination <br>
<br>
Jos haluaa suodata osan lähiosoitetta, tavallisen käyttöoikeudenluettelon on yksinkertainen ja riittävä.  <br>
Tavallisen käyttöoikeusluetteloita on kaksi tyypistä: nimetty ja numeroitu. <br><br>

Nimettyjen käyttöoikeus luettelossa inutiivisilla nimellä kuin numeroina, ja ne tukevat enemmin ominaisuuksia kuin numeroidun käyttöoikeusluettelot.

Lupa tai kielletty IP-osoittellee tulee määrittää yksittäisen "access-list x" määrän, että sallii/kieltää kulkemasta reitittimen porttin ylitse. <br>
Esim. nämä tietokoneen isännät ovat kielletty kulkemasta reitittimen porttin ylitse, mutta muut ovat sallittu lähettää pinggauksen reitittimen sisään <br>
access-list 1 deny host 192.168.10.4 <br>
access-list 1 deny host 192.168.10.5 <br>
access-list 1 deny host 192.168.10.6 <br>
access-list 1 deny host 192.168.10.7 <br>
<br>
access-list 11 permit 192.168.10.0 0.0.0.255 <br>
access-list 11 permit any (tämä on vaihtoehtoinen) <br>
Router: int se0/1/0 <br>
ip access-group 11 out <br>

<h3>TAI</h3>
Vaihtoehtona määrittää lasku toimitus, että täys 32-bittisen aliverkkopeiten eli 255, mitä jaettaan suhde määrän, että määrittää sallittun/kielettyn IP-osoitteen rajat. Tässä määrityksessä vaikutta pieni määrä aliverkkoon eli subnetwork, että kyseisen jakaja suhde isäntään, että mitkä alueet ovat salllttu/kieletty kulkemasta reitittimen ylitse.
<br>
![Alt text](images/Subnet-hosts-range.PNG?raw=true "None")

<br>
<b>Esim1)Tässä sallittaan vain puolet isäntä (host) verkosta, että IP-osoitteen 1-127 ovat sallittu ja 128-254 ovat kieletty. </b><br>
Router(config)#access-list 1 deny 192.168.10.126 0.0.0.127 <br>
Router(config)#access-list 1 permit 192.168.10.128 0.0.0.255 <br>
Router(config)# <br>
Router(config)#int gig0/1 <br>
Router(config-if)#ip access-group 1 out <br>
Router(config-if)# <br><br>

![Alt text](images/Sieppaa1-ACL-1.PNG?raw=true "None")

<b>Esim2) Tässä alunperin piti jakautua 1/4 suhteeseen, mutta tässä on vain määritetty, että sallitu IP-osoite on rajaltaan 64-127, ja muut kieletty. Vain kielettyn suhteessa määritetty 0-63, ja muut olevat ovat määrittämätön, että siksi pinggauksessa tapahtui epäonnistuminen.</b><br>
Router(config)# access-list 3 deny 192.168.50.0 0.0.0.63 <br>
Router(config)#access-list 3 permit 192.168.50.64 0.0.0.127 <br>
Router(config)# <br>
Router(config)#int gig0/1 <br>
Router(config-if)#ip access-group 3 out <br>
Router(config-if)#exit <br>
Router(config)#do wr <br>
Building configuration...<br>
[OK]<br>

![Alt text](images/Sieppaa1-ACL-subnet.PNG?raw=true "None")


<h2>Router port in or out</h2>
<br>
-out - mitä tarkoittaa, liikenne, mitä reititin on jo reitittänyt, ja joka poistuu käyttöliittymästä. <br>
-in - mitä tarkoittaa, liikenne, mitä saappuu käyttöliittymään, ja joka reitettään reitittimellä.
<br>

<hr>

# 100 - 199 extended acls
applied  closest to the source

määrityksessä kulkeuttuu, että kone sallittaan tai kieletty menemään sovelluskerrokseen, mitä on kuten http (80) / https (443), telnet (23, pääteyhteys internetin ylitse) ja yms protokollat. Sama vaikuttaa pinggaukseen, että onko kyseisen IP-osoittelle yksittäinen vai ryhmitetty joukko, mitä määritetty käyttäjäoikeus.

esim. Router1(config)# access-list 150 deny tcp host 192.168.1.15 host 192.168.2.50 eq 80
<br>
Tai<br>
Vaihtoehtona on ensimmäisenä luoda pieni organisaatio määritys, että rajoittaa IP-osoitteen tekijöille.
esim. <br>
R1(config)#ip access-list extended <NAME_ACL> <br>
R1(config-ext-nacl)#permit tcp 192.168.10.0 0.0.0.255 any eq 80 <br>
R1(config-ext-nacl)#permit tcp 192.168.10.0 0.0.0.255 any eq 443 <br>
R1(config-ext-nacl)#exit <br>
R1(config)#interface g0/0 <br>
R1(config-if)#ip access-group <NAME_ACL> in <br>
R1(config-if)#ip access-group <NAME_ACL> out

<br>
Esimerkkin komennon loppu perässä on eq , mitä tarkoittaa (Equal) eli yhtä suuri. Myös muita määrityksiä kuten: <br><br>
-gt (greater than) <br>
-lt (less than) <br>
-neq (not equal) <br>
-eq (equal) <br>
-range (range specified)<br><br>

![Alt text](images/ACL-extended-Ports.PNG?raw=true "None")

# Syntax
Jokin porttille syntaksi <br>
in - tarkoittaa määritystä, että ACL koskee saapuvaa liikennetä

out - tarkoittaa määritystä, että ACL koskee lähtevää liikennetä

# Wildmask calculation
Täyden aliverkko peitte on maksimissaan täys 32-bittinen on, mitä tarkoittaa 255.255.255.255 ja binääri menetelmässä 1 & 0 ( 11111111. 11111111. 11111111. 11111111) ja myös 24-bittinen, mitä täsmää aliverkkon 255.255.255.0 (11111111.11111111.11111111.00000000) ja jne. 

Lasku menetelmässä laskeuttuu täys 32-bittinen vähennettään (-), sitä määritettyä aliverkkon summaa PC kone sisäisen oma aliverkko peite eli esim. /28 (255.255.255.240), mitä jäljellä on enään 0.0.0.15

Lasku toimitus: 32-bittinen on (255.255.255.255) - 28-bittinen (255.255.255.250) = 0.0.0.15

<h2>Standard</h2>
Standardissa vaikuttaa IP-osoitteen määritykseen, että rajoittaa tiettyn määrän osoitteen esim. 192.168.10.0 - 192.168.10.255 sisällä on kieletty/lupa, että myös voidaan erikseen määrittää yksittäinen IP-osoite, ja muut ovat sallittu/kieletty.

<h2>Extended</h2>

Extended:issä määrittyy <b> lähde (source) </b> ja <b> määränpäähän (destination) </b2>, että useita verkkosovelluksia kuten verkkonprotokolla http/https, telnet ja jne.

![Alt text](images/ACL-WildcardMask.PNG?raw=true "None")
![Alt text](images/ACL-WildcardMask-example.PNG?raw=true "None")

<h2>Inbound ACL & Outbound ACL</h2>
<br>
<b>Inbound </b> - mitä kuin saapuvat paketit käsittellään ennen kuin ne reititettään lähtevään rajapintaan.<br>
<b>Outbound </b> - mitä saapuvat paketit reitietään lähtevään rajapintaan, ja ne käsittellään lähtevän ACL:n kautta. <br>



