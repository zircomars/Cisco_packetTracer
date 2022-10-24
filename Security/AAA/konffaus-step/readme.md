# konfiguration step by step

konfigurointien askel, että mitä pitää konfiguroida. 

määrityksessä pitää olla kaksi tai ehkä jopa useampi kohta pitää huomioida erityisesti, että määritettävien aaa - lausekkeessa riippuu, mitä ollaan tai mitä on konfiguroimassa sisään. Cisco simulaation pääserveri, mikä suoriutuu kuin tietokanta, jossa sisään tallentuu "username" ja "password" eli käyttäjätunnus ja salasanat, että serverin palvelimen ns. avain (key).

1) paikallista user-db:tä tulee käyttää, jos RADIUS-palvelin ei ole käytettävissä <br>
 $aaa authentication login default group radius local

2) halutaan, että sekä paikallistaa ja RADIUS-tiliä voidaan käyttää <br>
 $aaa authentication login default local group radius
 
 <br><br>
 
 ## reititimen konffaus 
 
 Router(config)#aaa ? <br>
  accounting      Accounting configurations parameters. <br>
  authentication  Authentication configurations parameters. <br>
  authorization   Authorization configurations parameters. <br>
  new-model       Enable NEW access control commands and functions.(Disables OLD commands.)
  <br><br>
Router(config)#aaa new <br>
Router(config)#aaa new-model <br><br>

Router(config)#aaa authentication ? <br>
  enable  Set authentication lists for enable. <br>
  login   Set authentication lists for logins. <br>
  ppp     Set authentication lists for ppp. <br>
Router(config)#aaa authentication enab <br>
Router(config)#aaa authentication enable ?<br>
  default  The default authentication list. <br>
Router(config)#aaa authentication enable default ? <br>
  enable  Use enable password for authentication. <br>
  group   Use Server-group. <br>
  none    NO authentication. <br>
Router(config)#aaa authentication enable default group ? <br>
  radius   Use list of all Radius hosts. <br> 
  tacacs+  Use list of all Tacacs+ hosts. <br> 
Router(config)#aaa authentication enable default group radius <br><br>

Router(config)#aaa authentication login ? <br> 
  WORD     Named authentication list. <br>
  default  The default authentication list. <br>
Router(config)#aaa authentication login default ? <br>
  enable      Use enable password for authentication. <br>
  group       Use Server-group. <br>
  local       Use local username authentication. <br>
  local-case  Use case-sensitive local username authentication. <br>
  none        NO authentication. <br>
Router(config)#aaa authentication login default group ? <br>
  radius   Use list of all Radius hosts. <br>
  tacacs+  Use list of all Tacacs+ hosts. <br>
Router(config)#aaa authentication login default group radius ? <br>
  enable      Use enable password for authentication. <br>
  group       Use Server-group. <br>
  local       Use local username authentication. <br>
  local-case  Use case-sensitive local username authentication. <br>
  none        NO authentication. <br><br>

<b> - HUOM!</b> <br>
Router(config)#aaa authentication login default group radius  <br><br>

Router(config)#aa authorization ? <br><br> <br>
  exec     For starting an exec (shell). <br>
  network  For network services. (PPP, SLIP, ARAP) <br>
Router(config)#aa authorization exec ? <br>
  WORD     Named authorization  list. <br>
  default  The default authorization  list. <br>
Router(config)#aa authorization exec default ? <br>
  group             Use Server-group. <br>
  if-authenticated  Succeed if user has authenticated. <br>
  local             Use local database <br>
  none              No authorization (always succeeds). <br>
Router(config)#aa authorization exec default group ? <br>
  radius   Use list of all Radius hosts. <br>
  tacacs+  Use list of all Tacacs+ hosts. <br>
Router(config)#aa authorization exec default group radius  <br><br>


<b> RADIUS SERVER / SERVERI YHTEYS </b> <br>
Router(config)#radius-server ? <br>
  host  Specify a Radius server <br>
  key   Set Radius encryption key. <br>
Router(config)#radius-server host 1.1.1.1 ? <br>
  auth-port  UDP port for RADIUS authentication server (default is 1645) <br>
  key        per-server encryption key (overrides default) <br>
  
Router(config)#radius-server host 1.1.1.1 key ? <br>
  LINE  The UNENCRYPTED (cleartext) shared key <br>
Router(config)#radius-server host 1.1.1.1 key cisco <br>


 
