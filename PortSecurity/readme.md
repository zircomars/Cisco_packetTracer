<h1>Port security 5.1.2021</h1>

Portin turvallisuus, mikä on Ciscon tuotemerkkin kytkimien <b>porttien turvallisuus</b> käyttö kontrolli ja viitemallien toisen kerroksen eli siirtoyhteyskerros.
Sen avulla, että järjestelmänvalvoja (administrator) voi määrittää yksittäisen kytkinportin sallimista ja tietyn määrän lähde MAC-osoiteitta tunkeutua porttiin.
Sen käyttö estää käyttäjiä lisäämästä kuin "hölmö" kytkmiä laittomasti laajentaakeen verkon kattavutta esim. että 2-3 käyttäjää voivat jakaa yhden pääsyportin.
Hallitsemattomien laitteiden lisääminen vaikeuttaa järjestelmävalvojien suorittamia vianmäärityksiä, että on parasta välttää.

<br>
![Alt text](images/Cisco-portSecurity.PNG?raw=true "None")

Kuka tahansa voi käyttää suojaamattomia verkkoresurssei yksinkertaisesti kytkemällä isäntään johonkin käytetättvien olevista kytkinporteista. Käyttäjä voi myös vaihtaa fyysistä sijaintiaan LAN-verkossa ilmoittamatta asiasta järjestelmänvalvojalle. Portin suojausominaisuuden avulla voit suojata kerroksen kaksi pääsyä ja pitää käyttäjät oikeilla jäljillä.

Switchport eli kytkmien porttien määrityksien suojatilojen ja -komentojen selittämisessä käytetään simulaatiota (cisco packet tracer) ohjelmistoa. Myös voi käyttää muita simulaatio ohjelmistoa, tai oikeetta fyysistä Cisco tuotteiden kytkintä ja noudattakseen sitä opastusta. Tulostuksessa ei ole eroa, kunhan valitsemasi ohjelmisto sisältää tässä opetusohjelmassa selostetut komennot.
