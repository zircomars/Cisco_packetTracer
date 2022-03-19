# EIGRP (Enhanced Interior Gateway Routing Protocol )

EIGRP on oma reititysprotokolla, mikä perustuu Cisco alkuperäisen IGRP-protokollasta. EIGRP on edistyksellinen etäisyysvektorin reititysprotokolla, mitä sisältää optimointeja, mitä tarkoituksena on minimoida kaikkia topologian muutoksien aiheutumia reitityksen epävakautta, sekä reitittimen kaistanleveyden käyttöä ja käsittelytehoa. EIGRP eroaa useimmista muista etävektoriprotokollista siinä, että se ei luota jaksottaisiin reitin kaatopaikkoihin, joten se pystyy ylläpitämään topologian taulukkoa. 

Kolme tyyppistä taulukkoa: <br>
- Naapuri-informaatio / Neighbor table <br>
 mm. naapurien osoitteet ja ”local interface”) <br>
 &nbsp; $show ip eigrp neighbors

- Naapureilta opittu topologiainformaatio / Topology table <br>
  Kaikki omat ja naapurien verkot  <br>
 &nbsp; metric-arvot ja liitynnät kohdeverkkoihin  <br>
  $Show ip eigrp topology  <br>
  
- Varsinaisen reititystaulukko / Routing table <br>
  reitittimen reititettyt protokollat kuten staatinen (ip route), dynaaminen (RIP), OSPF ja EIGRP, sekä yms. <br>
  &nbsp; $show ip route


# Configurointi & reititysprotokollan täsmennys ja muut infot


# EIGRP operaatio (metric, kaistanleveys ja viive)

