# OSPF ja EIGRP combo

- [configurations](#configurations)
 * [OSPF default route](#OSPF-default-route)
- [guide tutoriaalit ja yms:](#guide,-tutoriaalit-ja-yms:)

Reitityksessä tapahtuu pientä *redistributing* , mitä kuin tapahtuu jakamisen uudelleen ja yhteenvetoa (summization). Koska useissa verkoissa on erilaisia reititysprotokollia ja tarvitsee jonkinlaisen menetelmän vaihtamiseen, jotta suorittavat reitityksen välillä, siksi kutsuttaan *redistributing*. Molemmissa tapahtuu cost ja metric menetelmä, koska OSPF:ssä käyttää cost ja EIGRP:ssä käyttää k-arvoja, mitä eivät sovi yhteen, ja RIP käyttää hyppylaskua. 

Lisäksi *redistributing* tuoo toisen ongelman kuin, jos et *import* eli tuo reititsytietoa yhdestä reititysprotokollasta toiseen , että on mahdollista luoda reitityssilmukoita. 

<img src="images/EIGRP-OSPF-combo1.PNG" width="1250">

# configurations

Konfiguroinnissa voi tapahtuua oletuksena sen alueen protokollan määritys eli mainostaa oman OSPF ja EIGRP reitityksen, että lisää perintiesen staatisen reitityksen kuin toisi toisen puolen raja puolelta tulevia organisaatioita. 

<img src="images/EIGRP-OSPF-combo2.PNG" width="950">

<img src="images/EIGRP-OSPF-combo3.PNG" width="350">

## OSPF default route



# guide, tutoriaalit ja yms:
