# EIGRP (Enhanced Interior Gateway Protocol)


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

