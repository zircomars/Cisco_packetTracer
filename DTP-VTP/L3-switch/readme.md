# L3 switch

L3 tarkoittaa layer 3 tason konfigurointi, mikä on yksi OSI-mallista. Eli verkkokerros, joka välittä ylempien kerrosten tieotliikennepaketteja tietokoneiden välillä,
tarjoten pästä päähän yhteyden erilaisien verkkoratkaisujen ylitse

Layer 3 yhteensopivuuden kytkimen portiliitännässä otimivat oletusarvoiset Layer 2 - käyttöporttit, mutta mitä voi myös määrittää "Router ports", jotka toimivat normaaleina reitittimen liitänöinä. Eli IP-osoitteen suoraan reititetty portti, että lisäksi voi konfiguroida myös Switch VLAN interface (SVI) liitännän vlan:illa, sekä komento, mitä toimii Layer3-kytkimen virtuaalisena kerroksen 3 rajapinnassa.

![Alt text](images/L3-switchMap1.PNG?raw=true "None") <br>


# SVI (Switch virtual interface)

Suom. kytkin virtuaalinen liitäntä, mitä edustaa looginen kerroksen Layer 3 kytkin rajapinta. 
<br>
VLAN verkot jakavat lähetysverkkotunnusta LAN-ympäristössä. Aina kun yhden VLAN:n isännät joutuvat kommunikoimaan toisen VLAN:n isäntien kanssa, että liikenne on reititettävä niiden välillä. SVI- tai VLAN -käyttöliittymissä on virtuaalinen reititys käyttöliittymä, mitä yhdistää laitteen VLAN - laitteen samaan laitteen Layer 3 -reititinmoottoriin eli ryhmittää kokoonpanon yhteen reitittimeen. Vain yksi VLAN -liitäntä voidaan liittää VLAN -verkkoon, mutta sitä tulee määritettävä VLAN -liitäntä VLAN -verkkoa varten vain silloin, kun sitä halutaan reitittää VLAN -verkkojen välillä tai tarjota IP-isäntäyhteytä laitteeseen virtual routing and forwarding (VRF) - esiintymän kautta. Myös VLAN -rajanpinnan luomisen käytössä, kytkin luoo VLAN -rajapinnan oletus VLAN1:lle, että etäkytkimen hallinta voidaan sallia.

