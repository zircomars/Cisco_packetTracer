- [lyhyt teoria](#lyhyt-teoria)
- [radius harjoitus](#radius-harjoitus)
  * [harjoitus 1](#harjoitus-1)
  * [harjoitus 2](#harjoitus-2)
  * [harjoitus 3](#harjoitus-3)

- [tacacs harjoitukset](#tacacs-harjoitukset)
  * [tacacs harj 1](#tacacs-harj-1)
  * [tacacs harj 2](#tacacs-harj-2)
  * [tacacs harj 3](#tacacs-harj-3)

# lyhyt teoria

Harjoituksien kohdalla pari tärkeetä komentoa:
<br>
<h3> määritettävien aaa - lausekkeessa riippuu, mitä ollaan tai mitä on konfiguroimassa sisään </h3>

| komento | kuvaus |
| ----- |----- |
| $aaa authentication login default group [radius/tacacs+] local | paikallista user-db:tä tulee käyttää, jos RADIUS tai TACACS+ -palvelin ei ole käytettävissä | 
| $aaa authentication login default local group [radius/tacacs+] local | sallitaan, että sekä paikallistaa ja RADIUS tai TACACS+-tiliä voidaan käyttää |  

<hr>

Tämä komento periaatteessa korvautuisi kokonaisuudessaan lähes kaikken: <b> Router(config)#aaa authentication enable default group [radius/tacacs] local </b> <br> 
Tämän komento authentikointi turvallisuuden voimakkuus on vähä parempi kuin jos konffaisi reititimen sisään: $enable password abcd & Koska, kun yritettään kirjautua telnet host:in polkun kautta [ip-osoite] sisään kohti reititintä se kysyy kahesti käyttäjätunnus ja salasanaa. Cisco packet tracer simulaatiossa tämä komento antaa PC-koneiden tai yksittäisen reititimen kirjautua sisään hallinnoida konfigurointi asetuksia, että luoneen serverin AAA käyttäjätunnuksia. Simulaatiossa, kun otettaan reititintä polkua $enable - (lyhenne $en)käyttöön eli hallinnoidaan ja muokkataan sisäisen konfigurointi asetuksia, niin kysyy uudestaan käyttäjätunnus ja salasanaa, eli...

<img src="images/aaa_host-login-2.PNG" width="250">

Jos konfiguroi $enable password abcd - mitä perus kysyy salasanaa, mikä sen vahvuus on melko heikkoa, kun siirryttään $enable polun jälkeen. Eli..

<img src="images/aaa_host-login-1.PNG" width="250">

myös ei ole estettä konffata (enable password) komentoa, mutta se ois toinen vaihtoehto, kun kirjaudutaan telnet host:in kautta reititimen sisään niin authentikointi enable group komento ei tulisi mukaan. Lisäksi jotta haluttaan vahvistaa (enable password) toimisi niin pitää lisätä ($Router(config)#aaa authorization exec default group radius local) - ei ole estettä onko radius vai tacacs+ pohja..

<hr>

# radius harjoitus

## harjoitus 1 

<img src="images/radius-harjoitus-1.PNG" width="750">

<b>Serveri </b> <br>
<br>
<img src="images/radius-harjotus-2.PNG" width="600">

<b>Routerien steppit </b>
| konffaus steppit | server käyttöliittymä |
| ------- | --------- |
| Router(config)#aaa new-model <br> Router(config)#radius-server host 10.10.10.2 key moi <br> Router(config)#aaa authentication login default group radius local <br> Router(config)#line vty 0 5 <br> Router(config-line)#login authentication default <br> Router(config-line)# <br><br> new: tämä puuttui <br> Router(config)#aaa authentication enable default group radius local <br> <br> vaikka pääseee routerien sisään, mutta tähän asti <br><br> Router> <br> Router>en <br> Username: <br> Password: <br> Router# | services / aaa valikko <br><br> - <b>Network configuration</b> <br> client name : routeri <br> client ip: 10.10.10.1 <-- reititimen portti liitäntä IP-osoite ja serverin välinen yhteys <br> secret : moi <-- avain, mikä määriyttyy pääsypalvelimeen <br> servertype: radius <-- vaihtoehtona on tacas <br><br> -  <b>User setup </b> <br> tässä valikkossa luodaan käyttäjätunnus, mikä muistuttaa vähä kuin kytkimen tai reitittimen sisään luodaan telnet/ssh tunnukset <br> myös saa luoda toisen tunnuksen, jossa sisään kirjautumisessa sallii  yhden tai useamman käyttäjäntunnukset |
| määritettävien aaa - lausekkeessa riippuu, mitä ollaan tai mitä on konfiguroimassa sisään | 
| $aaa authentication login default group radius local | paikallista user-db:tä tulee käyttää, jos RADIUS-palvelinta ei ole käytettävissä | 
| $$aaa authentication login default local group radius | jos halutaan, että sekä paikallistaa ja RADIUS-tiliä voidaan käyttää |  

<b> HUOM! </b> <br> komento ($aaa new-model) joka sovletaa välittämästi paikallista todentamista, että linjoihin ja liitäntöihin. Jos telnet sessio avataan reitittimelle, joten tämä komennto käyttöönoto jälkeen (yhteys aikakatkaisee) ja yhteys muodostuu uudelleen, käyttäjä on todennettu reitittimen paikallisen tietokonnan avulla. On suositeltavaa määrittää käyttäjätunnus ja salasana pääsypalvelimelle ennen AAA-määrityksen aloittamista, jotta et lukittuisi reitittimeen. 

<hr>

## harjoitus 2

Vasen R0 & oikea R1 <br>
<img src="images/radius-harjoitus2-1.PNG" width="850"> <br>

Ensimmäisenä konffataan reititykset, että 192.168.50.0/24 ja 192.168.60.0/24 kommunikoivat/pinggaavat toisiinsa, ennen kuin konffaa radius authentikoinnin sisään. Konffauksesta voi konffata joko staatisella tai dynaamisella pohjalla, että koneet pinggavat. 

<img src="images/radius-harjoitus2-2.PNG" width="350"> <br>

Kun koneet pinggavat toisiinsa, sen jälkeen konfiguroidaan R1 sisään radius määritykset. Konffauksesta username cisco password cisco999 - kohta on valinnainen, koska tämän määrityksen jälkeen se ei tallennu serverin tietokanta järjestelmään, mutta serveriin pitää manuaalisesti luoda käyttäjätunnus ja salasana.

<img src="images/radius-harjoitus2-3.PNG" width="350"> <br>


## harjoitus 3

Special harjoitus 3, että tarkistellaan kahden radius konffauksen pientä eroa, mutta periaatteessa molemmat toimivat ja vaikuttaa autentikontien vahvuuteen. Koska kirjautumisen kanssa kirjaudutaan telnet host:in kautta reititimeen antamalla käyttäjätunnus ja salasana kaksi kertaa vai kerran, että kirjauduttua syötettään kyseisen salasana..

<img src="images/radius-harjoitus3-1.PNG" width="450"> <br>
<img src="images/radius-harjoitus3-2.PNG" width="350"> <br>
<br> <hr>
<img src="images/radius-harjoitus3-3.PNG" width="450"> <br>
<img src="images/radius-harjoitus3-4.PNG" width="350"> <br>
<img src="images/radius-harjoitus3-5.PNG" width="350"> <br>


# tacacs harjoitukset

## tacacs harj 1

<img src="images/tacacs-harjoitus-1.PNG" width="500">

<b>Routerien steppit </b>
| konffaus steppit | server käyttöliittymä |
| ------- | --------- |
| Router(config)#aaa new-model <br> Router(config)#aaa authentication login default group tacacs+ local<br> Router(config)#aaa authentication enable default group tacacs+ local <br><br> tacacs server need host ip-add and key word <br> Router(config)#tacacs-server host 200.0.0.100 key toinen <br><br> VTY line & suoritettaan telnet <br> line vty 0 4 & login authentication default - mean we want to use login <br> credentials from the tacacs server preferably <br> Router(config)#line vty 0 4 <br> Router(config-line)#login authentication default <br> Router(config-line)# <br><br> | AAA server <br> 200.0.0.100 <br><br> services / aaa valikko <br><br> network configuration valikko <br> client name: switch <br> client ip: 200.0.1 <br> secret: toinen <br> servertype: tacacs <br><br> serverissä luodaan käyttäjätunnuksia ja salasana <br> user setup: <br> username: puu <br> pass: puu123 <br><br> toinen käyttis: <br> koivu <br> koivu123 |
| ennen sitä pitää muuttaa hostname eli routerin nimeäminen <br> Router(config)#hostname Routeri <br> Routeri(config)#crypto key generate rsa  <br> The name for the keys will be: Routeri.cisco.com <br> Choose the size of the key modulus in the range of 360 to 2048 for your <br> General Purpose Keys. Choosing a key modulus greater than 512 may take a few minutes. <br><br> How many bits in the modulus [512]: 1024 <br>% Generating 1024 bit RSA keys, keys will be non-exportable...[OK] <br><br> Routeri(config)#ip domain name cisco.com Routeri(config)#ip ssh version 2 <br><br> Please create RSA keys (of at least 768 bits size) to enable SSH v2. <br> Routeri(config)#crypto key generate rsa <br><br> Line vty:lle, että suoritettaan ssh, koska videossa ei haluta telnet <br> Routeri(config)#line vty 0 4 <br> Routeri(config-line)#transport input ssh <br> Routeri(config-line)#exit <br><br> PC / KONE KÄYTTÄJÄT <br> C:\>ssh -l puu 200.0.0.1 | vaihtoehtona on konffata ssh sisään, ettei käytettäisi telnet:iä & tämä vaihe on vapaaehtoinen | 
| määritettävien aaa - lausekkeessa riippuu, mitä ollaan tai mitä on konfiguroimassa sisään ja ilman näitä kahta ei päästäisi reititimen sisään | 
| $aaa authentication enable default group tacacs+ local | kaikki käyttäjät todennetaan ensin tacacs-palvelimella ja jos se ei vastaa, otetaan yhteyttä paikalliseen tietokantaan | 
| $aaa authentication login default group tacacs+ local | paikallista käyttäjätunnusta ja salasanaa käytetään, samoin kuin aktivointisalasanassa |  

## tacacs harj 2

Staatinen reititys & AAA tacacs yhteys

<img src="images/tacacs-harjoitus-2.PNG" width="750">

Ensimmäisenä konffaa staatisen reitityksen eli mainostaa reititimen vastapään olevan IP-osoitteen ja sen jälkeen määrittää R2:lle tacacs+ konffit

<img src="images/tacacs-harjoitus-2-1.PNG" width="350">


## tacacs harj 3

Tacacs+ L3 switch (3560-24PS) konffaus 

<img src="images/tacacs-harjoitus-3.PNG" width="750">

Harjoituksen konfiguroidaan oletus vlan 1 ensimmäisenä, koska käytettään L3 switch:iä telnet protokollaa pääyhteyksenä, jotta PC:n kautta mennään L3 switch:n asetuksien sisään. Myös L3 switch asetuksista konfiguroidaan tacacs+ konffauksia, ja huom. tässä on pientä eroa verrattuna tacacs harjoitus 1 ja 2:n kanssa.

<img src="images/tacacs-harjoitus-3-1.PNG" width="700">




