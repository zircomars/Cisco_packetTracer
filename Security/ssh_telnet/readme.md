# Telnet & SSG

# [](#)
  * [Telnet](#Telnet)
  * [SSH](#SSH)

## Telnet
Telnet yhteysprotokolla pääyhteys Internetin ylitse ja sitä muodostettaan asiakkaan tietokoneeseen palvelimen komentorivipalveluihin, jolloin päästään käyttämään palvelimen ohjelmia ja palveluita kuten lukemaan sähköpostia. 

Koska telnet-protokollan asiakaspuoli ei oletusarvoisesti liikennöi palvelinpuolelle mitään protokollakohtaista, voi telnet-ohjelmia käyttää myös yksinkertaisten puhtaiden TCP-yhteyksien ottamiseen tiettyihin palveluihin vaikkapa niiden testaamista varten.

Telnet ei salaa liikennettä, koska mukaan lukien salasanoja), ja protokolla tietoturva taso on heikko, ja usein käytetään ssh, koska monissa käyttötarkoituksissa se on kuin korvattu.

## SSH 
Secure Shell eli salattujen tietoliikenne protokolla. Yleisin SSH käyttö salattun työkalu väline, ja sitä käytettään usein etäyhteydessä SSH-asiakasohjelmissa. Sisään päästäkseen käytettään cli / linux tai muu komentorivien työalua päästäkseen konsolin kautta sisään. SSH voidaan myös suojata FTP-, HTTP- tai muuta liikennettä, joka toimii samalla tasolla kuin tuttu telnet. 

SSH-protokollasta on kaksi versiota, vanhentunut SSH1 ja SSH2. SSH2 kehitettiin kiertämään RSA-algoritmin patentteja.
