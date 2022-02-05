<h1>NAT (Network address translation) - Osoitteenmuunnos </h1>

NAT:ssa konfiguroinnissa tapahtuu vähintään yksi liitäntä, että yksi sisäinen ja ulkoinen verkko. NAT ympäristössä tapahtuu poistumislaitteessa tynkätoimialue ja runkoverko välisä. Kun paketti poistuu tomialueesta, mitä NAT muuntaa paikallisen merkittävän lähdeosoitteen maailmanlaajuisesti ainutlaatuisen osoitteeksi. Kun paketti tulee toimialueella, mitä NAT muuntaa maailmanlaajuisesti yksillösen kohdeosoitten paikkalisen osoitteeksi. <br>
Jos on useampi kuin yksi lähtöpiste, mitä NAT:lla on oltava sama käännöstaulukko. Jos NAT ei voi varata oositetta, mitä osoitteet ovat loppuneet, mitä pudottaa paketin. Myös NAT lähettää ICMP (Internet Control Message Protocol) isäntäpaketin, mitä ei voida saavuttaa.

<br> Myös konfiguroinnin tapahtuu ACL eli access-list command, että tapahtuu salli/kielto isännän tietokoneen määrityksessä tai useampi kone.

<br><br>
![Alt text](images/Cisco-NAT-map1.PNG?raw=true "None")
![Alt text](images/Cisco-NAT-map2.PNG?raw=true "None")

<hr>

# NAT tyyppit
NAT toimii reitittimessä, mitä yhdistää vain kaksi verkkoa. Ennen kuin lähettää paketteja välittää toiseen verkkoon, mitä NAT muuttaa sisäisen verkkon yksityiseksi paikallisen osoitteen julkiseksi osoitteeksi. Tämä toiminto antaa mahdollisuuden määrittää NAT, että mainostaa vain yhtä osoitetta koo verkostoa ulkomaailmalle. 

# NAT (Static & Dynamic, Overload)
Staatinen: mitä mahdollistaa paikallisten ja yleisten osoitteiden yhdistämistä yksittelen

Dynaaminen: mitä osoitteiden muunnos, että yhdistää rekisteröimättömät IP-osoitteet rekisteröidyksi IP-osoitteiksi rekisteröityjen IP-osoitteiden joukosta.

Overload eli ylikuormitus, mitä useita rekisteröitttömiä IP-osoitteita yhdeksi rekisteröidyksi IP-osoitteeksi käyttämällä eri portteja. Tämä menetelmä tunnetaan myös nimellä PAT. Mitä tuhannet käyttäjät voivat muodostaa yhteyden Internetiin käyttämällä vain yhtä todellista globaalia IP-osoitetta ylikuomirtuksen kautta.

# NAT inside & outside address
NAT "inside" kontekstissä viitaa organisaation omistamisen verkkoa, että jokaisessa on käännettävä. NAT määritettyssä, mitä verkon isännäillä on osoitteet yhdessä tilassa. Tämä isäntä näyttävät verkon ulkopuolisille käyttäjille olevia toisessa tilassa. <br><br>

Vastaavasti "outisde" mitä viitaa niihin verkkoihin, mitä tynkäverkko liittyy, ja jotka eivät ole organisaation hallinnassa. Myös ulkouplisten verkkojen isännät voivat olla käänösten alaisia, ja niilä voi olla paikallisia ja globaaleja osoiteitta.

<h2>Inside</h2>

Inside osoite - mitä IP-osoite, jolla on määritetty sisäverkon isännälle. Verkkotietokeskus NIC tai palvelutarjoaja antama osoite ei ole todennäisesti ole laillinen IP-osoite <br><br>
Inside osoite - NIC:n tai palvelutarjoaaja märittämä laillinen IP-osoite, mitä edustaa yhtä tai useampaa sisäistä paikallista IP-osoitetta ulkomaailmalle.

<h2>Outside</h2>

Outside osoite - ulkoisen isäntä IP-osoite näkyy sisäverkossa, mitä ei vältämättä laillinen osoite, mutta se varataan osoiteavaruudesta, joka on reitiettävissä sisältä "inside"
<br><br>
Outside osoite - IP-osoite, mitä isännän omistaja on määrittänyt isännän ulkoiselle verkolle ja osoite allokoidaan maailmanlaajuisesti reitettävästä osoitteesta tai verkkoavaruudesta.

<hr>

# PAT (Port address translation)

PAT sallii tukea monia isäntä vain harvoilla julkisilla IP-osoitteilla. Myös se toimii luomalla dynaamisen NAT-kartoituksen, mitä valitaan yleinen (julkinen) IP-osoite ja yksilöllinen porttinumero. Reititin säilyttää NAT-taulukkomerkinnän jokaisesta yksityisen IP-osoitteen ja portin yksilölisestä yhdistelmästä, että on käännetty globaalinen osoitteeksi ja yksilöllinen porttinumero.


# muu guide ja ohjeet
<br>
https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipaddr_nat/configuration/xe-16/nat-xe-16-book/iadnat-addr-consv.html <br>
https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipaddr_nat/configuration/15-mt/nat-15-mt-book/iadnat-addr-consv.html <br>
https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus5600/sw/interfaces/7x/b_5600_Interfaces_Config_Guide_Release_7x/config_static_and_dynamic_nat_translation.pdf <br>
https://www.ciscozine.com/nat-and-pat-a-complete-explanation/ <br>



