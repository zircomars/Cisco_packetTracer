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

SSH-protokollasta on kaksi versiota, vanhentunut SSH1 ja SSH2. SSH2 kehitettiin kiertämään RSA-algoritmin patentteja. Myös käytettään oletus vlan 1:stä, että täsmentyy se ip-osoite esim. vlan 1 IP-add 10.23.49.3 255.255.255.0 , joten konen isäntä IP-osoite tulemaan 10.23.49.254 255.255.255.255.0 & cmd:llä kirjaudutaan komennolla $ssh -l admin 10.23.49.3

### SSH konffaus

Switch(config)#hostname switch0 <br>
switch0(config)#ip domain-name cisco <br>
switch0(config)#crypto key generate rsa <br>
The name for the keys will be: switch0.cisco <br>
Choose the size of the key modulus in the range of 360 to 2048 for your <br>
</t>  General Purpose Keys. Choosing a key modulus greater than 512 may take a few minutes. <br>
<br>
How many bits in the modulus [512]: 1024 <br>
% Generating 1024 bit RSA keys, keys will be non-exportable...[OK] <br><br>

switch0(config)#service password-encryption <br>

switch0(config)#username admin secret cisco <br>
*Mar 1 0:5:27.978: %SSH-5-ENABLED: SSH 1.99 has been enabled <br>

switch0(config)#enable secret cisco <br>
switch0(config)# <br>
switch0(config)#line vty 0 15 <br>
switch0(config-line)#transport input ssh <br>
switch0(config-line)#logging synchronous <br>
switch0(config-line)#password cisco <br>
switch0(config-line)#login local <br>
switch0(config-line)#exit <br>
switch0(config)#ip ssh version 2 <br>
switch0(config)#exit <br>


# linkkit ja konffauksien juttut:





