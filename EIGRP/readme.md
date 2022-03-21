# EIGRP (Enhanced Interior Gateway Routing Protocol )

EIGRP on oma reititysprotokolla, mikä perustuu Cisco alkuperäisen IGRP-protokollasta. EIGRP on edistyksellinen etäisyysvektorin reititysprotokolla, mitä sisältää optimointeja, mitä tarkoituksena on minimoida kaikkia topologian muutoksien aiheutumia reitityksen epävakautta, sekä reitittimen kaistanleveyden käyttöä ja käsittelytehoa. EIGRP eroaa useimmista muista etävektoriprotokollista siinä, että se ei luota jaksottaisiin reitin kaatopaikkoihin, joten se pystyy ylläpitämään topologian taulukkoa. EIGRP käyttää reittien valinta oman DUAL-algoritmia, että reititysilmukka ei synny. DUAL-algoritmi reittiminen pitää pysyä selvittämään, että laite on suoraan kytketty, että hello-viestin avulla EIGRP selvittää ovatko naapurilaitteet reitittimiä vai ei.

EIGRP lähettää päivitystietoja verkosta vain, jos tapahtuu muutos, kuten yhteys poikki tai laite hajoaa. Protokolla tukee myös luokatonta reititystä CIDR (Classless Inter-Domain Routing) sekä kuormantaustasta, että pitää tehkokkaan kuormittavan liikkaa reitittimen resurssia. 

<img src="images/EIGRP-topologyMap-1.PNG" width="450">

Toiminassa tapahtuu naapurien löytäminen, topologien tietojen vaihtaminen ja reittien valinta. Naapurien löytäkseen tapahtuu <i> Hello </i> viestiä IP-osoitteseen kautta, että löytäkseen potentiaalisen vereisen naapurin EIGRP reitittimen, ja suorittaa parametrin tarkistuksen tarkastaen, mistä reitittimistä pitää tulla naapuri. Myös tarkastuksen sisältävät nelljä kohtaa:

1. Pitää läpäistä autentikointi toiminnan
2. Pitää olla konfiguroitu käyttämällä samaa autonomisen systeemin (AS = autonomous system) numeron.
3. Naapurien reititimien lähde IP-osoite, mitä pitää olla samassa aliverkossa kuin lokaalinen reitittimen IP-osoite ja maski.
4. Reitittimien K-arvojen pitää täsmätä, ja Cisco järjestelmä ei suosittele vaihtamista, koska ovat määritetty oletuksena. K-arvoja on:

| K-arvot | Osat  | Kuvaus teksti  |
| ------- | --- | --- |
| K1 | kaistanleveys (bandwidth) | reititin alhaisin kaistanleveys |
| K2 | kuorma (load) | reitin huonoin kuormitus pakettinopeuden perusteella |
| K3 | viive (delay) | reititin kumulatiivinen rajapinnan viive |
| K4 | luotettavuus (reliability) | Luotettavuuden perustuen reitin hengissä pysyminen |
| K5 | MTU (reliability | Pienin MTU reitissä (ei käytetä reitin laskemisessa) |

Kolme tyyppistä taulukkoa: <br>
- Naapuri-informaatio / Neighbor table <br>
 mm. naapurien osoitteet ja ”local interface”) <br>
 &nbsp; $show ip eigrp neighbors

- topology table (topologitaulu) <br>
&nbsp; tarkistaa reitityksen metric luvun, että toteutumisen ja raportoidun etäisyyden. Myös hyppystä, että jos (kuin reititystaulukko komento)
  $show ip eigrp topology  <br>
  
- Varsinaisen reititystaulukko / Routing table <br>
  tarkistaa koko reitityksen yhteydet, protokollat (EIGRP, OSPF, staatinen tai dynaaminen), myös EIGRP metric luku <br>
  &nbsp; $show ip route
  
- tarkista reitittimen porttien kaistanleveys (bandwidth), ja usein ovat nimetty BW XY Kbit/sec. <br>
&nbsp; Jos reitittimeen kytkeytyy serial johto, mitä oletuksena on aina  1544 kb/s <br>
&nbsp; $show interfaces [portti-luku]

# EIGRP operaatio (kaistanleveys ja viive & metric matematiikka)

EIGRP protokollan reitityksessä lasketaan metrikkaa (metric), että jakautuu kahteen osaan, kaistanleveyttä ja viivettä. Muitakin asetuksia on mahdollista suoraan peilaten K-arvoihin, kuormitus ja luotettavuuteen. Metrikkaan tulosta tapahtuu EIGRP konfiguroinnin jälkeen, että reititin ymmärtää EIGRP rakennetta ja komenolla ($show ip route) löytää metrikkaan tuloksen. Tuloksesta kertoo reitityksen seuraaja <b> (DUAL) </b>, että mahdolliisen seuraaja IP-osoite. Seuraaja reitti märittää mittarin määränpäähän saavuttamista, että reitti on tallennettu reititystaulukoon. Toteutettava seuraaja on varapolku samaan määränpäähän, jota voidaan käyttää välittömästi, jos seuraajareitti epäonnistuu.

![alt text](images/EIGRP-metricCalcu-1.PNG?raw=true)

<h2>EIGRP Metric</h2>

Jokaisessa reitittimen portissa on käyttölittymä tyyppi, että määrittyy reitittimen naaras ethernet, giga tai serial portti. Jokaisen porttissa on jokin ominaisuus kuten viive, kaistanleveys ja muu oletuksen luvun suuruus. Myös konfiguroinnissa voi määrittää manuaalisen kaistanleveyden luvun, että metriikka luku muuttuu saman aikaisesti. Komenolla $show interface (portti-nimi-luku), että löytää kyseisen porttien taustat kuten tiedonsiirto nopeus, kaistanleveys, viive, määritettyn manuaalinen IP-osoite ja muita data yksikköitä. 

![alt text](images/EIGRP-metricInterfacesTypes.PNG?raw=true)

K-taulukkojen arvojen ja yksikköt, että tässä kuvassa on reitittimen porttien teknisien luvujen tyyppit. MTU osoittaa MTU K5, BW tarkoittaa Bandwidth K1 (kaistanleveys), DLY tarkoittaa Delay K3 (viive), Reliability tarkoittaa luotettavuus K4 ja kohta 255/255, viimeisenä rxload tarkoittaa load K2 (kuorma)

![alt text](images/EIGRP-metricExample-1.PNG?raw=true)

Oletuksena serial kaapeli on kaistanleveydeltään 1 544 Kb/s. Jos muutettaan serial kaapelin kaistanleveyttä manuaalisesti, mitä reitityksentaulukkon metriikka summa muuttuu samantien. 

<img src="images/EIGRP-metricExample-2.PNG" width="750">

<h2>Metric lasku toimitus</h2>

Lasku toimitus menee kaavan mukaan, mutta helpoiten ymmärtää tällä, ja käytettään: <br>
( (10^7 / Bandwidth) +  total delay / 10) ) * 256 = metric

<img src="images/EIGRP_formula-1.jpg" width="750">

<h3> Ensimmäinen lasku esimerkki </h3>

Jos on määrittänyt EIGRP protokollan konfiguroinnin, että pinggaukset toimivat, koneet kommunikoivat, reitittimen porttit ovat päällä ja käyttää oletuksen reitittimen kaistanleveyden summaa. Myös käytettään tämän alemman kuvan esimerkkiä. Metric suuruudesta kulkeutuu nopeamman reitityksen mukaan, koska gigabitEthernet:issä on vähemmän viivettä, siksi jos tarkistaa reitityksen taulukkon, mitä tulostuu & näkyy [90/3072]. Koska pinggauksen viesti kulkeutuu Router-0 :sta --> Router-1 --> Router-2:lle.

<img src="calc1/eigrp-math1.PNG" width="525">

Komennolla tarkistaa tavallisen reititystaulukkon ($show ip route) tai EIGRP reititystaulukkon ($show ip router eigrp). Tavallisessa reititystaulukkossa näkyy, mitä tähän kohteen reitittimeen on konfiguroitu, yhteys ja muu kohteen IP-osoite, sekä tarkennettun reitittimen portti numero kohde.

<img src="calc1/eigrp-math2.PNG" width="675">
<img src="calc1/eigrp-math3.PNG" width="500">

<h3> Toinen lasku esimerkki </h3>

<img src="calc1/eigrp-math2-1.PNG" width="525">
<img src="calc1/eigrp-math2-2.PNG" width="675">
<img src="calc1/eigrp-math2-3.PNG" width="500">


<h2>EIGRP DUAL-algoritmi</h2>

# Configurointi & reititysprotokollan täsmennys ja muut infot


