# Komennot ja muut vianmääritykset EtherChannel, LACP ja PAgP:ssä

$show etherchannel summary -  yhden tietorivin port-channel taustasta, että jos on konfiguroitu protokolla eli LACP ja PAgP:tä, group määrä, ja porttien (flags) kuin nimitys ja on konfiguroitu aktiiviseen tilaan 

![Alt text](images/Etherchannel-summary1.PNG?raw=true)

$show etherchannel port-channel - tulostaa yleisen tilan etherchannel liittymästä, näkyy channel-group luku, protokolla (LACP / PAgP), port-security (disabled) ja porttit port-channel:ssa 

$show interfaces etherchannel - Antaa tietoa käyttöliittymän roolista EtherChannelissa, portti tila, channel group määrä, port-channel, ja kytkimien porttien tilanne ja muu informaatio. 

![Alt text](images/Etherchannel-interfaces-1.PNG?raw=true)

![Alt text](images/Etherchannel-interfaces-2Total.PNG?raw=true)


$show interface Port-channel - näyttää EtherChannel-liittymän yleisen tilan, että näkyy port-channel protokolla on ylhäällä (up) ja yhteydessä.

$show spanning tree - näyttää kytkimen pakotettun juurin, että porttien tilanne/kuvauksen, että pakotettun juuren prioriteetty oletus luku. Lisäksi sisältyen etherchannel port-channel luvun määritettyn kokoonpanon, että kohteen kytkimen määritetystä protokollasta kuten Po3 

![Alt text](images/Etherchannel-STP-status.PNG?raw=true)

# LACP konfigurointi vaiheet:

yksi porttista tapahtui määritys "passive", koska se osoittaa, että halutaan saada kytkimen LACP protokollan päälle. Jos toisen laitteen LACP protokollan ilmaisin, että jompi kumppi kytkin on passiivinen moodi

esim. S0-0 ja S1-1 välisen etherchannel konffaus:
<br>
S0 <br>
Switch(config)#int range fa0/1 - 2 <br>
Switch(config-if-range)#channel-group 1 mode active <br>
Switch(config-if-range)#interface port-channel 1 <br>
Switch(config-if)#switchport mode trunk <br>
Switch(config-if)#switchport trunk allowed vlan 1,2, 10-20 <br>
Switch(config-if)#switchport trunk allowed vlan 1-99  <br><br>

S1 <br> 
Switch(config)#int range fa0/1 - 2 <br> 
Switch(config-if-range)#channel-group 1 mode passive <br>
Switch(config-if-range)#interface port-channel 1 <br>
Switch(config-if)#switchport mode trunk <br>
Switch(config-if)#switchport trunk allowed vlan 1-99 <br><br>

<hr> 

# PAgP konfigurointi vaiheet:

S0<br>
Switch(config)#int range fa0/1 - 3 <br>
Switch(config-if-range)#channel-group 1 mode ? <br>
&emsp; active     Enable LACP unconditionally <br>
&emsp; auto       Enable PAgP only if a PAgP device is detected <br>
&emsp; desirable  Enable PAgP unconditionally <br>
&emsp; on         Enable Etherchannel only <br>
&emsp; passive    Enable LACP only if a LACP device is detected <br> <br>

Switch(config-if-range)#channel-group 1 mode desirable <br>

Switch(config-if-range)#channel-protocol ? <br>
&emsp; lacp  Prepare interface for LACP protocol <br>
&emsp; pagp  Prepare interface for PAgP protocol <br>
Switch(config-if-range)#channel-protocol pagp <br>

S1 <br>
Switch(config)#int range fa0/1 - 3 <br>
Switch(config-if-range)#channel-group 1 mode desirable <br>

Switch(config-if-range)#channel-protocol pagp <br>
Switch(config-if-range)#exit <br>
 
<h3> EtherChannel PAgP yhteenveto </h3>

![Alt text](images/EtherChannel-pagp-conf-3Summary.PNG?raw=true)
