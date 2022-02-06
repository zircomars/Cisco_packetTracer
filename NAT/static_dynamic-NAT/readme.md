<h1>Staatinen ja dynaaminen NAT konfigurointin reititys</h1>

# Static
Staatisessa tapahtuu ip nat inside source static reititys protokolla. Riittää reititin määrityksessä määrittää porttin kumpi on inside tai outside, mitä kuin toimii mainonta melkein.

![Alt text](images/NAT-static-configurationCommand.PNG?raw=true "None")

# Dynamic
Dynaamisessa tapahtuu ip nat pool <NAME> <Alkava --- päätyvä IP-osoite> <subnet-mask>
  
![Alt text](images/NAT-dynamic-configurationCommand.PNG?raw=true "None")


Standardi ACL oikeudenlistan luominen ja reitittimen porttien inside/outside käyttöjärjestelmä

  
# guide ja opas, ja muut linkkit:<br> <br>
  https://packetlife.net/media/library/32/NAT.pdf <br>
  https://www.practicalnetworking.net/stand-alone/cisco-asa-nat/
  https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipaddr_nat/configuration/xe-3s/nat-xe-3s-book/iadnat-ha.pdf  <br>
  https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipaddr_nat/configuration/xe-16/nat-xe-16-book/iadnat-ha.html  <br>
