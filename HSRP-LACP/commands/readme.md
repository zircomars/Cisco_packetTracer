# Komennot ja muut vianmääritykset EtherChannel, LACP ja PAgP:ssä

$show etherchannel summary -  yhden tietorivin port-channel taustasta, että jos on konfiguroitu protokolla eli LACP ja PAgP:tä, group määrä, ja porttien (flags) kuin nimitys ja on konfiguroitu aktiiviseen tilaan 

$show etherchannel port-channel - tulostaa yleisen tilan etherchannel liittymästä, näkyy channel-group luku, protokolla (LACP / PAgP), port-security (disabled) ja porttit port-channel:ssa 

$show interfaces etherchannel - Antaa tietoa käyttöliittymän roolista EtherChannelissa, portti tila, channel group määrä, port-channel, ja kytkimien porttien tilanne ja muu informaatio. 

$show interface Port-channel - näyttää EtherChannel-liittymän yleisen tilan, että näkyy port-channel protokolla on ylhäällä (up) ja yhteydessä.
