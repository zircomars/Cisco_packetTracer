# Käyttäjätunnuksien luominen

Käyttäjätunnuksien luomisesta, että kun kirjaudutaan joko telnet tai ssh protokollan kautta kohti kytkimeen tai reititimen sisään, jotta tarkistettaan sisäiset konfigurointi asetukset. Luomisesta vaikuttaa sen turvallisuutteen, että esim. tarkistaa konffit salasana näkyy tai spesial erikoismerkejä.

# Cisco Privilege Levels 

privilege level security - etuoikeustason suojaus

level 0 - nollataso käyttöoikeus sallii vain viisi komentoa - logout | enable | disable | help & exit

level 1 - käyttäjäntaso käyttöoikeus antaa vain siirtyä user exec tilaan, joka tarjoaa erittäin rajoitetun vain luku - oikeuden reitittimeen

level 15 - käyttöoikeustason käyttöoikeus mahdollistaa pääsyn privileged exec - tilaan ja tarjoaa täydellisen hallinnan reitittimeen

Priviledge konffaus malli: <br>
Router(config)#username admin1 privilege 0 secret Study-CCNA1 <br>
Router(config)#username admin2 privilege 15 secret Study-CCNA2 <br>
Router(config)#username admin3 secret Study-CCNA3 <br>

<hr>

<img src="images/aaa-user-1.PNG" width="650">

<img src="images/aaa-user-2.PNG" width="650">

<img src="images/aaa-user-3.PNG" width="650">

<img src="images/aaa-user-4.PNG" width="450">
