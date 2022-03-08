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

