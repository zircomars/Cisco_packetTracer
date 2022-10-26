# radius harjoitus 

## harjoitus 1 

<img src="images/radius-harjoitus-1.PNG" width="750">

<b>Serveri </b> <br>
<br>
<img src="images/radius-harjotus-2.PNG" width="600">

<b>Routerien steppit </b>
| konffaus steppit | server käyttöliittymä |
| ------- | --------- |
| Router(config)#aaa new-model <br> Router(config)#radius-server host 10.10.10.2 key moi <br> Router(config)#aaa authentication login default group radius local <br> Router(config)#line vty 0 5 <br> Router(config-line)#login authentication default <br> Router(config-line)# <br><br> new tämä puuuttui <br> Router(config)#aaa authentication enable default group radius local <br> <br> vaikka pääseee routerien sisään, mutta tähän asti <br><br> Router> <br> Router>en <br> Username: <br> Password: <br> Router# | services / aaa valikko <br><br> - <b>Network configuration</b> <br> client name : routeri <br> client ip: 10.10.10.1 <-- reititimen portti liitäntä IP-osoite ja serverin välinen yhteys <br> secret : moi <-- avain, mikä määriyttyy pääsypalvelimeen <br> servertype: radius <-- vaihtoehtona on tacas <br><br> -  <b>User setup </b>|
