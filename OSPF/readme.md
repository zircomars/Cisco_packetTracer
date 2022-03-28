- [OSPF (Open Shortest Path First)](#OSPF-(Open-Shortest-Path-First))
- [OSPF metric and cost](#OSPF-metric-and-cost)
 * [OSPF calculations](#OSPF-calculations)
- [OSPF and EIGRP fusion](#OSPF-and-EIGRP-fusion)
- [](#)
- [](#)

# OSPF (Open Shortest Path First)

Sitä käytetään erityisesti Internet Protocol (tai IP) -verkoissa. Se on linkitilan reititysprotokolla ja se on yleisimmin ryhmitelty sisäisten yhdyskäytäväprotokollien kanssa. Se toimii yhden autonomisen järjestelmän (tai AS: n) sisällä. OSPF on epäilemättä yleisin sisäinen yhdyskäytäväprotokolla (tai IGP), joka toimii pääasiassa suurissa yritysverkoissa.

# OSPF metric and cost

Metric = cost & laskutus menee: cost = viitekastanleveys / käyttöliittymän kaistanleveys. Oletuksena viitekaistanleveys on 10^8 eli 100 000 000 bps & käyttöliittymä kaistanleveys tarkoittaa reitittimen porttit kuten seriel- ja fast-, giga- ja muu ethernet johto. 

Jokaisen host:i löytyy reititystaulukkosta ($show ip route), että tulostuu esim. [110/65], ja 65 on se host..

## OSPF calculations

# OSPF and EIGRP fusion
