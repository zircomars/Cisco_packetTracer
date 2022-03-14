# Hot Standby Router Protocol - HSRP & configurations

![alt text](images/HSRP-sampleConf.PNG?raw=true)

Konfiguroinnissa tapahtuu komennon määrityksellä "preempt". Preempt sanasta on "preemption" ja Suomeks. etuoikeus, sekä Cisco reittimissä on suuuret resurssit, suurempi kaistanleveys tai vähemmän latenssi/viive (latency) muihin verkoihhin reitttimiin verratuna. Myös HSRP:ssä on oletuasrvo, mitä pitää asentaa komennolla "$standby preempt", mitä reititin on korkeampi HSRP-prioriteettitaso, että voi toimia välittömästi. Oletusprioriteetti on 100, mutta prioriteetin arvoa manipuloida vaaliprosessia.

![alt text](images/HSRP-conf-1.PNG?raw=true)

![alt text](images/HSRP-conf-2.PNG?raw=true)

![alt text](images/HSRP-conf-3.PNG?raw=true)

<h2> Sama harjoitus kuin ylempi versio, mutta uusi yritys </h2>

![alt text](images/HSRP-confi-1.PNG?raw=true)

# komennot ja muut varmistukset

Reitittimessä voi tarkistaa HSRP taustan, että on komento etuoikeus suoritustilassa:
$show standby

# configurointi ohjeet ja muut oppaat:
https://study-ccna.com/cisco-hsrp-configuration/ <br>
https://www.routerfreak.com/how-to-configure-hsrp-on-a-cisco-router/ <br>
https://www.youtube.com/watch?v=gxsMuHXCOqg <br>
https://www.youtube.com/watch?v=aVxFnAh2gFA <br>
https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3560/software/release/12-2_25_se/configuration/guide/3560scg/swhsrp.pdf <br>
    <br>
