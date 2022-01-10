<h1>Dynaaminen Port-security reititys</h1>


<h2>MAC osoitteen pysyvä reititys</h2>

Konfiguroinnissa MAC-osoite kuin muuttuu pysyväksi, että määritellyssä voidaan määrittää <b>dynaamisella konfiguroinnila</b> tai määrittää manuaalisesti, että tallentaa osoite taulukkoon ja lisätä käynnissä olevan kokoonpanon. Jos osoite on tallennettu asetustiedostoon, joten käyttöliittym ei tarvitse dynaamisesti uudelleen, kun kytkin käynnistyy itsekseen. Vaikka pysyvät suojatut osoitteet voi määrittää manuaaalisesti, mutta sitä ei suositella.

Määritksen käyttöliittymän muutuma dynaaminen MAC-osoiteet pysyvästi suojautuu MAC-osoitteeksi ja lisäämään ne käynnissä olevia kokoonpannoi ottamalla käyttöön pysyvän oppimisen. Ota kiinteä oppiminen käyttöön kirjoittamalla switchport port-security mac-address sticky-komento. Kun annat tämän komennon, käyttöliittymä muuntaa kaikki dynaamiset suojatut MAC-osoitteet, mukaan lukien ne, jotka opittiin dynaamisesti ennen kuin kiinteä oppiminen otettiin käyttöön, pysyviksi suojatuiksi MAC-osoitteiksi.

Pysyvät suojatut MAC-osoitteet eivät automaattisesti tule osaksi määritystiedostoa, joka on käynnistysmääritys, jota käytetään aina, kun kytkin käynnistyy uudelleen. Jos tallennat pysyvät suojatut MAC-osoitteet asetustiedostoon, käyttöliittymän ei tarvitse opetella näitä osoitteita uudelleen kytkimen käynnistyessä uudelleen. Jos et tallenna määrityksiä, ne menetetään.

Kun suojattujen MAC-osoitteiden enimmäismäärä on määritetty, ne tallennetaan osoitetaulukkoon. Varmistaaksesi, että liitetyllä laitteella on portin koko kaistanleveys, määritä liitetyn laitteen MAC-osoite ja aseta osoitteiden enimmäismääräksi yksi, joka on oletusarvo. 
