# L3 switch

L3 tarkoittaa layer 3 tason konfigurointi, mikä on yksi OSI-mallista. Eli verkkokerros, joka välittä ylempien kerrosten tieotliikennepaketteja tietokoneiden välillä,
tarjoten pästä päähän yhteyden erilaisien verkkoratkaisujen ylitse

Layer 3 yhteensopivuuden kytkimen portiliitännässä otimivat oletusarvoiset Layer 2 - käyttöporttit, mutta mitä voi myös määrittää "Router ports", jotka toimivat normaaleina reitittimen liitänöinä. Eli IP-osoitteen suoraan reititetty portti, että lisäksi voi konfiguroida myös Switch VLAN interface (SVI) liitännän vlan:illa, sekä komento, mitä toimii Layer3-kytkimen virtuaalisena kerroksen 3 rajapinnassa.

![Alt text](images/L3-switchMap1.PNG?raw=true "None") <br>

# Komennot ja konfiguroinnin määritykset

<h2>$no switchport </h2>

Tämä komento, mitä tarjoaa Layer 3 kytkimen käyttöliittymä. Tämä komento, mitä muuttaa Layer 2 portista kohti Layer 3:seen ja saa portin toimimaan reitittimen liitäntä kytkinportin. Reititetty portti ei ole liitetty mihinkään VLAN-verkkooon, eikä se tue VLAN-aliliittymiä. Sitä kuitenkin voi käyttää IP-osoitetta suoraan porttiin, ja lisää IP-osoitteiden määritysvaihtoehtoihin on käytettävissä tämän no switchport kommennon jälkeen. Eli multilayer switch L3 porttiin voidaan järjestää/muodostaa oma IP-osoite, että esim. tuleva reitistä voidaan kuin suorittaa kommunikointi, ja pinggaus, ja muu yhteys reitittimeen ei kulje mitään VLAN-id:tä. Myös välisen yhteys voi tapahtu palomuuri, käyttäjäoikeus (ACL), ja muu alueen reititys (eigrp, ospf & bgp ).
<br><br>
Toimii kuin tavalllisen kytkimen konfigurointi, että voi määrittää VLAN-id:tä, mitä kuin loisi pieni organisaation määrityksen, että ovat eri Layer 3 aliverkoissa. Viestinnässä muiden LAN- tai VLAN-verkkojen ympäristössä mitä tarvitsee Layer 3 toimintaa. Layer 2 ja 3:ssa, mitä yhdistää joitakin kytkimen ominaisuuksia. <br><br>

<b>Esim. multilayer switch konffaus</b>

<h2>$ip routing</h2>

Tämä komento, mitä tarkoituksena on kuin tarkistaa kytkimen sisäisn reititystaulukko, ja kuin routerien/reitittimen komento ($show ip route). Tämän komento määritys tapahtuu vain multilayer switch L3 kytkimessä, että voi tarkistaa sisäisen VLAN-id, koneiden yhteydet, fyysisen sisäisen multilayer switch kytkimen portti ja muu IP-soitteiden määritys. Tavallisessa L2 tason kytkimessä ei voi määrittää tätä komentoa, koska ikään kuin niissä ei ole luotu, määritetty tai sen kokoonpanoa.

![Alt text](images/MLS-L3-Conf-1.PNG?raw=true "None") <br>

![Alt text](images/MLS-L3-Conf-2.PNG?raw=true "None") <br>


# Inter-VLAN routing

<b> Perinteisessä </b> VLAN-verkossa, mitä käytetään segmentoimalla kytkettyjen Layer 2 verkkoa. Riippumatta yhden VLAN.in isännät ei voi kommunikjoida toisen VLAN:in kanssa, eli esim. VLAN-20 ja 10 eivät voi pinggata ja kommunkoida kahden kesken, tai useamman VLAN-id isännät/organisaatiot. Tämän ongelman takia, että tarjotaan Layer 3 kytkin, että on tarjoaa reitityspalvelua. <br><br>

![Alt text](images/Inter-VLAN-map1.PNG?raw=true "None") <br>

<b>Router on a stick</b> Inter-VLAN reititys, VLAN-reititysmenetelmä, mitä on vanhan VLAN-reititysmenetelmän rajoitukset. Se vaatii vain yhden fyysisen Ethernet-liitännän liikenteen reitittämiseen useiden verkon VLAN-verkkojen välillä. Cisco tuotteen reitittimen Ethernet-liitäntä on määritetty 802.1Q-runkoverkostoksi ja yhdistetty Layer 2 -kytkimen runkoporttiin. Erityisesti reitittimen käyttöliittymä on määritetty käyttämällä aliliittymiä reititettävien VLAN-verkkojen tunnistamiseen. <br><br>

![Alt text](images/Inter-VLAN-map2.PNG?raw=true "None") <br>

<b>Inter VLAN reititys L3 kytkin</b>. Nykyaikainen menetelmä VLAN-reitityksen suorittamiseen on käyttää Layer 3 -kytkimiä ja kytkettyjä virtuaalisia rajapintoja (SVI). Inter-VLAN SVI:t luodaan samalla tavalla kuin hallinta-VLAN-liitäntä on määritetty. SVI on luotu kytkimessä olevaa VLAN-verkkoa varten. Vaikka SVI on virtuaalinen, se suorittaa samat toiminnot VLAN-verkossa kuin reitittimen käyttöliittymä. Erityisesti se tarjoaa Layer 3 -käsittelyn paketeille, jotka lähetetään kaikkiin kyseiseen VLAN-verkkoon liittyviin kytkinportteihin tai niistä. 

![Alt text](images/L3-switchMap1.PNG?raw=true "None") <br>


# SVI (Switch virtual interface)

Suom. kytkin virtuaalinen liitäntä, mitä edustaa looginen kerroksen Layer 3 kytkin rajapinta. 
<br>
VLAN verkot jakavat lähetysverkkotunnusta LAN-ympäristössä. Aina kun yhden VLAN:n isännät joutuvat kommunikoimaan toisen VLAN:n isäntien kanssa, että liikenne on reititettävä niiden välillä. SVI- tai VLAN -käyttöliittymissä on virtuaalinen reititys käyttöliittymä, mitä yhdistää laitteen VLAN - laitteen samaan laitteen Layer 3 -reititinmoottoriin eli ryhmittää kokoonpanon yhteen reitittimeen. Vain yksi VLAN -liitäntä voidaan liittää VLAN -verkkoon, mutta sitä tulee määritettävä VLAN -liitäntä VLAN -verkkoa varten vain silloin, kun sitä halutaan reitittää VLAN -verkkojen välillä tai tarjota IP-isäntäyhteytä laitteeseen virtual routing and forwarding (VRF) - esiintymän kautta. Myös VLAN -rajanpinnan luomisen käytössä, kytkin luoo VLAN -rajapinnan oletus VLAN1:lle, että etäkytkimen hallinta voidaan sallia.

# L3 muita ohjeita, ja muita kytkimen liittyviä taustoi: <br>
https://www.fiber-optic-transceiver-module.com/no-switchport-command-how-much-do-you-know.html <br>
https://www.ciscopress.com/articles/article.asp?p=2990405&seqNum=4 <br>
https://www.cisco.com/en/US/docs/ios/lanswitch/configuration/guide/lsw_ml_sw_over_support_TSD_Island_of_Content_Chapter.html <br>
https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst9300/software/release/16-12/configuration_guide/vlan/b_1612_vlan_9300_cg/configuring_layer_3_subinterfaces.pdf <br>
https://www.networkstraining.com/what-is-cisco-svi-configuration-example/ <br>

<!-- http://www.ccna6rs.com/4-3-8-packet-tracer-configure-layer-3-switching-and-inter-vlan-routing-answers/
https://networkengineering.stackexchange.com/questions/68802/difference-between-switchport-trunk-encapsulation-dot1q-and-switchport-mode-trun
https://www.youtube.com/watch?v=Gsacj9G-RG8

-->
