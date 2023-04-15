# reititimen konffaus komennot

- [konffaus malli](#konffaus-malli)
  * [R1](#R1)
  * [R2](#R2)
- [konffaus muistisääntö](#konffaus-muistisääntö)

HUOM! jotakin tiettyjä konffauksia ja määritystä cisco packet tracer simulaatiossa ei tue tai ikäänkuin ihan täsmälleen suorita kuin todellisuuden IOS malli.

Router(config)#crypto ? <br>
  dynamic-map  Specify a dynamic crypto map template <br>
  ipsec        Configure IPSEC policy <br>
  isakmp       Configure ISAKMP policy <br>
  key          Long term key operations <br>
  map          Enter a crypto map <br><br>

Router(config)#crypto isakmp ? <br><br>
  client  Set client configuration policy <br>
  enable  Enable ISAKMP <br>
  key     Set pre-shared key for remote peer <br>
  policy  Set policy for an ISAKMP protection suite <br><br>

Router(config)#crypto isakmp policy <br>
Router(config)#crypto isakmp policy ? <br>
  <1-10000>  Priority of protection suite <br>
Router(config)#crypto isakmp policy 10 <br><br>

Router(config-isakmp)#encryption ? <br>
  3des  Three key triple DES <br>
  aes   AES - Advanced Encryption Standard <br>
  des   DES - Data Encryption Standard (56 bit keys). <br>
Router(config-isakmp)#encryption ae <br>
Router(config-isakmp)#encryption aes ? <br>
  128  128 bit keys. <br>
  192  192 bit keys. <br>
  256  256 bit keys. <br>
  <cr> <br><br> 
Router(config-isakmp)#encryption aes 256 <br><br>

Router(config-isakmp)#? <br>
  authentication  Set authentication method for protection suite <br>
  encryption      Set encryption algorithm for protection suite <br>
  exit            Exit from ISAKMP protection suite configuration mode <br>
  group           Set the Diffie-Hellman group <br>
  hash            Set hash algorithm for protection suite <br>
  lifetime        Set lifetime for ISAKMP security association <br>
  no              Negate a command or set its defaults <br><br>

Router(config-isakmp)#aut <br> 
Router(config-isakmp)#authentication ? <br>
  pre-share  Pre-Shared Key<br>
Router(config-isakmp)#authentication pre <br> 
Router(config-isakmp)#authentication pre-share <br><br>

Router(config-isakmp)#group 5 <br>
Router(config-isakmp)# <br><br>

---------------------------------

Router(config)# crypto ? <br>
  dynamic-map  Specify a dynamic crypto map template <br>
  ipsec        Configure IPSEC policy <br>
  isakmp       Configure ISAKMP policy <br>
  key          Long term key operations <br>
  map          Enter a crypto map <br>
Router(config)# crypto isa <br>
Router(config)# crypto isakmp ? <br>
  client  Set client configuration policy <br>
  enable  Enable ISAKMP<br>
  key     Set pre-shared key for remote peer <br>
  policy  Set policy for an ISAKMP protection suite <br>
Router(config)# crypto isakmp key <br>
Router(config)# crypto isakmp key vpnpa55? <br>
WORD  <br>
Router(config)# crypto isakmp key vpnpa55 ? <br>
  address  define shared key with IP address <br>
Router(config)# crypto isakmp key vpnpa55 add <br>
Router(config)# crypto isakmp key vpnpa55 address 10.2.2.2 <br><br>

------------------------------------------------
luodaan crypto ipsec transfer name <br><br>

Router(config)#crypto ? <br>
  dynamic-map  Specify a dynamic crypto map template <br>
  ipsec        Configure IPSEC policy <br>
  isakmp       Configure ISAKMP policy <br>
  key          Long term key operations <br>
  map          Enter a crypto map <br>
Router(config)#crypto ipsec <br>
Router(config)#crypto ipsec ? <br>
  security-association  Security association parameters <br>
  transform-set         Define transform and settings <br>
Router(config)#crypto ipsec tra <br>
Router(config)#crypto ipsec transform-set ? <br>
  WORD  Transform set tag <br><br>

Router(config)#crypto ipsec transform-set VPN-SET ? <br>
  ah-md5-hmac   AH-HMAC-MD5 transform <br>
  ah-sha-hmac   AH-HMAC-SHA transform <br>
  esp-3des      ESP transform using 3DES(EDE) cipher (168 bits) <br>
  esp-aes       ESP transform using AES cipher <br>
  esp-des       ESP transform using DES cipher (56 bits) <br>
  esp-md5-hmac  ESP transform using HMAC-MD5 auth <br>
  esp-sha-hmac  ESP transform using HMAC-SHA auth <br>
Router(config)#crypto ipsec transform-set VPN-SET esp <br>
Router(config)#crypto ipsec transform-set VPN-SET esp-aes ? <br>
  128           128 bit keys. <br>
  192           192 bit keys. <br>
  256           256 bit keys. <br>
  esp-md5-hmac  ESP transform using HMAC-MD5 auth <br>
  esp-sha-hmac  ESP transform using HMAC-SHA auth <br>
  <cr> <br><br>
Router(config)#crypto ipsec transform-set VPN-SET esp-aes esp-sh <br>
Router(config)#crypto ipsec transform-set VPN-SET esp-aes esp-sha-hmac ? <br>
  <cr>

----------<br><br>
crypto map name VPN, map set peer is router three outbound interface set transfoorm can conf before and match address 110 <br><br>

Router(config)#crypto ? <br>
  dynamic-map  Specify a dynamic crypto map template <br>
  ipsec        Configure IPSEC policy <br>
  isakmp       Configure ISAKMP policy <br>
  key          Long term key operations <br>
  map          Enter a crypto map <br>
Router(config)#crypto map ? <br>
  WORD  Crypto map tag <br>
  ipv6  IPv6 crypto map <br>
Router(config)#crypto map VPN-MAP ? <br>
  <1-65535>  Sequence to insert into crypto map entry <br>
  client     Specify client configuration settings <br>
  isakmp     Specify isakmp configuration settings <br><br>

Router(config)#crypto map VPN-MAP 10 ? <br>
  ipsec-isakmp  IPSEC w/ISAKMP <br><br>
  <cr>
Router(config)#crypto map VPN-MAP 10 ip <br>
Router(config)#crypto map VPN-MAP 10 ipsec-isakmp <br>
% NOTE: This new crypto map will remain disabled until a peer and a valid access list have been configured. <br><br>

Router(config-crypto-map)#description VPN connection to R2 <br>
Router(config-crypto-map)# <br>
Router(config-crypto-map)#? <br>
  description  Description of the crypto map statement policy <br>
  exit         Exit from ISAKMP protection suite configuration mode <br>
  match        Match values. <br>
  no           Negate a command or set its defaults <br>
  set          Set values for encryption/decryption <br>
Router(config-crypto-map)#set ? <br>
  peer                  Allowed Encryption/Decryption peer. <br>
  pfs                   Specify pfs settings <br>
  security-association  Security association parameters <br>
  transform-set         Specify list of transform sets in priority order <br><br>

Router(config-crypto-map)#set peer  <br>
Router(config-crypto-map)#set peer 10.2.2.2  <br>
Router(config-crypto-map)#set ? <br>
  peer                  Allowed Encryption/Decryption peer. <br>
  pfs                   Specify pfs settings <br>
  security-association  Security association parameters <br>
  transform-set         Specify list of transform sets in priority order <br><br>

Router(config-crypto-map)#set transform-set ? <br>
  WORD  Proposal tag <br>
Router(config-crypto-map)#set transform-set VPN-SET ---match transform-set "VPN-SET" id/name esp-aes esp-sha-hmac <br><br>

Router(config-crypto-map)#match address ? <br>
  [100-199]  IP access-list number <br>
  WORD       Access-list name <br>
Router(config-crypto-map)#match address 110 <br><br>


find VPN map crypto map to the outgoing from serial serial cable or other port <br>

Router(config)#int se0/3/0 <br> 
Router(config-if)#crypto map VPN-MAP <br>
*Jan  3 07:16:26.785: %CRYPTO-6-ISAKMP_ON_OFF: ISAKMP is ON <br>

<hr>

# konffaus malli

Tätä kutsutaan site-to-site

<img src="../images/cisco-ipsec-1.PNG" width="950"> <br>

molemmissas on lisätty lisenssi/päivitys versio $license boot module c2900 technology-package securityk9 - riippuu reititimen sisäisen datasta, että salliiko sen & mutta harjotuksessa käytetty cisco 2911 reititin <br>

## R1

! <br>
license udi pid CISCO2911/K9 sn FTX1524Z18X- <br>
license boot module c2900 technology-package securityk9 <br>
! <br><br>

!<br>
crypto isakmp policy 10 <br>
 encr aes 256 <br>
 authentication pre-share <br>
 group 5 <br>
! <br>
crypto isakmp key vpnpa55 address 10.2.2.2 <br>
! <br><br>

! <br>
crypto ipsec transform-set VPN-SET esp-aes esp-sha-hmac <br>
! <br>
crypto map VPN-MAP 10 ipsec-isakmp 
 description VPN connection to R2 <br>
 set peer 10.2.2.2 <br>
 set transform-set VPN-SET  <br>
 match address 110 <br>
!<br><br>

!
interface GigabitEthernet0/0 <br>
 ip address 192.168.1.1 255.255.255.0 <br>
 duplex auto <br>
 speed auto <br>
! <br>
!
interface Serial0/3/0 <br>
 ip address 10.1.1.2 255.255.255.252 <br>
 clock rate 2000000 <br>
 crypto map VPN-MAP <br>
! <br> <br>
! <br>
ip classless <br>
ip route 0.0.0.0 0.0.0.0 10.1.1.1  <br>
! <br>
ip flow-export version 9 <br>
! <br>
! <br>
access-list 110 permit ip 192.168.0.0 0.0.255.255 192.168.0.0 0.0.255.255 <br>
! <br>

## R2

! <br>
license udi pid CISCO2911/K9 sn FTX1524Z18X- <br>
license boot module c2900 technology-package securityk9 <br>
! <br><br>

!<br>
crypto isakmp policy 10 <br>
 encr aes 256 <br>
 authentication pre-share <br>
 group 5 <br>
! <br>
crypto isakmp key vpnpa55 address 10.1.1.2 <br>
! <br><br>

! <br>
crypto ipsec transform-set VPN-SET esp-aes esp-sha-hmac <br>
! <br>
crypto map VPN-MAP 10 ipsec-isakmp 
 description VPN connection to R1 <br>
 set peer 10.1.1.2 <br>
 set transform-set VPN-SET  <br>
 match address 110 <br>
!<br><br>

!
interface GigabitEthernet0/0 <br>
 ip address 192.168.3.1 255.255.255.0 <br>
 duplex auto <br>
 speed auto <br>
! <br>
!
interface Serial0/3/0 <br>
 ip address 10.2.2.2 255.255.255.252 <br>
 crypto map VPN-MAP <br>
! <br> <br>
! <br>
! <br>
ip classless <br>
ip route 0.0.0.0 0.0.0.0 10.2.2.1 <br>
! <br>
ip flow-export version 9 <br>
! <br>
! <br> 
access-list 110 permit ip 192.168.0.0 0.0.255.255 192.168.0.0 0.0.255.255 <br>
! <br>

------------------------------------------------------------------------------------------------------------------

# konffaus muistisääntö

mikäli jos tulee konffamaaan jotakin ipsec tunnelia ja määritystä löytyy usein sivustoilta niin usein antaa ne framework valmiiksi. HUOM tämä koskee cisco ympäristöä ja alussa pieni huomautus jotakin cisco ei tue crypto ikev1:stä tai vastaavaa ja jne. 

Yleensä ensimmäinen konffaus tapahtuu alemman pohjan mukaan, sitten vastapäässä oleva yhteys tai mihin reititimeen halutaan reitittää sitä vpn tunnelia niin tulemaan identtinen/peilikuvana.

Router(config)#crypto isakmp policy 10 <br>
Router(config-isakmp)#authentication pre-share <br>
Router(config-isakmp)#encryption aes 256 <br>

muita vaihtoehtoisia kuin (esp-aes, esp-sha-hmac) <br>
Router(config)#crypto ipsec transform-set ? <br><br>
  WORD  Transform set tag
Router(config)#crypto ipsec transform-set kirja ? <br>
  ah-md5-hmac   AH-HMAC-MD5 transform <br>
  ah-sha-hmac   AH-HMAC-SHA transform <br>
  esp-3des      ESP transform using 3DES(EDE) cipher (168 bits) <br>
  esp-aes       ESP transform using AES cipher <br>
  esp-des       ESP transform using DES cipher (56 bits) <br>
  esp-md5-hmac  ESP transform using HMAC-MD5 auth <br>
  esp-sha-hmac  ESP transform using HMAC-SHA auth <br>
Router(config)#crypto ipsec transform-set kirja esp-aes ? <br>
  128           128 bit keys. <br>
  192           192 bit keys. <br>
  256           256 bit keys. <br>
  esp-md5-hmac  ESP transform using HMAC-MD5 auth <br>
  esp-sha-hmac  ESP transform using HMAC-SHA auth <br><br>

<br>
Router(config-isakmp)#group 2 <br>
Router(config-isakmp)#lifetime 86400 <br>
Router(config-isakmp)#exit <br><br>

Reititimen mihin ollaan reititimässä niin sen menevä reititin portti IP-osoite <br>
Router(config)#crypto isakmp key avainsana address 10.0.0.1   <br>
Router(config)#crypto ipsec transform-set kirja esp-aes esp-sha-hmac <br>

Määritä reititimen acl, että mistä mihinkin asti vaikappa oiskin kaukana tai välissä on useampi reititin välitys <br>
Router(config)#access-list 101 permit ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255 <br>

aktivoidaan crypto kartta ja joku sana, sekä tuossa peer tarkoittaa mihin reititimeen vastapäähän ollaan reititimässä, jotta kahden reititimen välisen yhteys muodostuu se vpn ipsec tunneli. myös täsmennetään (match) acl extendedn id (101) <br><br>
Router(config)#crypto map cmap 10 ipsec-isakmp      <<<< 10 täsmäää isakmp polic num <br>
% NOTE: This new crypto map will remain disabled until a peer <br>
        and a valid access list have been configured. <br>
Router(config-crypto-map)#set peer 10.0.0.1   <br>
Router(config-crypto-map)#match address 101         <<< täsmää access-list numeron <br>
Router(config-crypto-map)#set transform-set kirja   <<<< "kirja" anna joku toinen sana & täsmää transform-set sanan <br>
Router(config-crypto-map)#exit <br>
<br>
viimeisenä aktivoidaan portti lähtö vaikappa ulkoverkkoon WAN ja se cryptatu kartta id <br>
Router(config)#int giga0/0 <br>
Router(config-if)#crypto map cmap <br>
*Jan  3 07:16:26.785: %CRYPTO-6-ISAKMP_ON_OFF: ISAKMP is ON <br>

<hr> ############################################################################## <br>
joku pien simppeli jos löytää mallia, että framework parametrejä syötettään
<br><br>
crypto ikev1 policy 1 <br>
authentication pre-share <br>
encryption aes <br>
hash sha <br>
group 2 <br>
lifetime 86400 <br>
exit <br>
!
crypto ikev1 enable outside <br><br>

tunnel-group 173.199.183.2 type ipsec-l2l <br>
tunnel-group 173.199.183.2 ipsec-attributes <br>
ikev1 pre-shared-key Cisc0 <br>
<br>
crypto ipsec ikev1 transform-set pfSense-AES128SHA esp-aes esp-sha-hmac <br>
! <br>
access-list outside_cryptomap_10 remark ACL to encrypt traffic from ASA to pfSense <br>
access-list outside_cryptomap_10 extended permit ip 192.168.1.0 255.255.255.0 10.0.0.0 255.255.255.0 <br>
! <br>
crypto map outside_map 10 match address outside_cryptomap_10 <br>
crypto map outside_map 10 set peer 173.199.183.2 <br>
crypto map outside_map 10 set ikev1 transform-set pfSense-AES128SHA <br>
crypto map outside_map interface outside <br>