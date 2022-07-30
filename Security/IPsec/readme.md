# IPsec (IP Security Architecture) 
TCP/IP-joukkon kuuluva tietoliikenneprotokolla Internet-yhteyksien turvaaminen. Nämä protokollat tarjoavat salauksen, osapuolten todennuksen ja tiedon eheyden varmistamisen. Pääasiassa tämä tarkoittaa UDP-pohjaisia sovelluksia, ICMP-kontrolliviestejä sekä reitityksessä ja tunneloinnissa käytettyjä IP-protokollia kuten GRE:tä, OSPF:aa ja niin edelleen. Verrattaessa kuljetuskerroksen protokolliin, kuten SSLään, haittapuolena on se, että IPsec-protokollien pitää pystyä hallitsemaan myös vakaus- ja fragmentoitumisongelmat, jotka yleensä on hoidettu korkeammalla tasolla, TCP- eli kuljetuskerroksella.

Käytössä protokolla voi käyttää vaihtoehtoisia kuten:
- yhteydenpitokanavien turvaamista, jolloin usieden koneiden isäntä tai jopa koko lähiverkon liikenne ohjataan yhden pisteiden (esim. palomuurien) kautta, jossa lähtevän liikenne salataan ja vastaavasti paluulikenne puretan tai
- pakettiliikenteen turvaamiseen koko matkalle lähettäjältä vastaanottajalle, jolloin päätepisteiden tietokoneet hoitavat salauksen vaatiman prosessoinnin.

IPsec-protokollaa voidaan käyttää VPN-ratkaisun eli näennäisen yksityisverkon rakentamiseen kummallakin tavalla. On huomioitava että saavutettava tietoturva eroaa huomattavasti näiden kahden mallin välillä.

<img src="images/IPsec-1.PNG" width="500"> <br>
<img src="images/IPsec-2.PNG" width="500">


