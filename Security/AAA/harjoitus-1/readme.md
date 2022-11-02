- [radius harjoitus](#radius-harjoitus)
  * [harjoitus 1](#harjoitus-1)
  * [harjoitus 2](#harjoitus-2)

- [tacacs harjoitukset](#tacacs-harjoitukset)
  * [tacacs harj 1](#tacacs-harj-1)
  * [tacacs harj 2](#tacacs-harj-2)

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


# tacacs harjoitukset

## tacacs harj 1

## tacacs harj 2
