Current configuration : 9931 bytes !
! Last configuration change at 07:26:54 UTC Thu Nov 20 2025 by admin !
version 17.6
service timestamps debug datetime msec service timestamps log datetime
msec service call-home
platform punt-keepalive disable-kernel-core !
hostname Switch !
!
vrf definition Mgmt-vrf !
address-family ipv4 exit-address-family !
address-family ipv6 exit-address-family
! 
! 
! 
!
!
aaa new-model !
!
aaa group server radius radius_group server name RADIUS-SERVER
!
aaa authentication login default group radius_group local aaa
authorization exec default group radius_group local
! ! ! ! ! !
aaa session-id common
switch 1 provision c9200l-24t-4g !
! ! ! ! ! ! ! !
ip routing !
ip domain name sio.local !
! !
login on-success log !
crypto pki trustpoint SLA-TrustPoint revocation-check crl
!
crypto pki trustpoint TP-self-signed-1241688237 enrollment selfsigned
subject-name cn=IOS-Self-Signed-Certificate-1241688237
revocation-check none
rsakeypair TP-self-signed-1241688237 !
!
crypto pki certificate chain SLA-TrustPoint certificate ca 01
30820321 30820209 A0030201 02020101 300D0609 2A864886 F70D0101
0B050030 32310E30 0C060355 040A1305 43697363 6F312030 1E060355
04031317 43697363 6F204C69 63656E73 696E6720 526F6F74 20434130
1E170D31 33303533 30313934 3834375A 170D3338 30353330 31393438
34375A30 32310E30 0C060355 040A1305 43697363 6F312030 1E060355
04031317 43697363 6F204C69 63656E73 696E6720 526F6F74 20434130
82012230 0D06092A 864886F7 0D010101 05000382 010F0030 82010A02
82010100 A6BCBD96 131E05F7 145EA72C 2CD686E6 17222EA1 F1EFF64D
CBB4C798 212AA147 C655D8D7 9471380D 8711441E 1AAF071A 9CAE6388
8A38E520 1C394D78 462EF239 C659F715 B98C0A59 5BBB5CBD 0CFEBEA3
700A8BF7 D8F256EE 4AA4E80D DB6FD1C9 60B1FD18 FFC69C96 6FA68957
A2617DE7 104FDC5F EA2956AC 7390A3EB 2B5436AD C847A2C5 DAB553EB
69A9A535 58E9F3E3 C0BD23CF 58BD7188 68E69491 20F320E7 948E71D7
AE3BCC84 F10684C7 4BC8E00F 539BA42B 42C68BB7 C7479096 B4CB2D62
EA2F505D C7B062A4 6811D95B E8250FC4 5D5D5FB8 8F27D191 C55F0D76
61F9A4CD 3D992327 A8BB03BD 4E6D7069 7CBADF8B DF5F4368 95135E44
DFC7C6CF 04DD7FD1 02030100 01A34230 40300E06 03551D0F 0101FF04
04030201 06300F06 03551D13 0101FF04 05300301 01FF301D 0603551D
0E041604 1449DC85 4B3D31E5 1B3E6A17 606AF333 3D3B4C73 E8300D06
092A8648 86F70D01 010B0500 03820101 00507F24 D3932A66 86025D9F
E838AE5C 6D4DF6B0 49631C78 240DA905 604EDCDE FF4FED2B 77FC460E
CD636FDB DD44681E 3A5673AB 9093D3B1 6C9E3D8B D98987BF E40CBD9E
1AECA0C2 2189BB5C 8FA85686 CD98B646 5575B146 8DFC66A8 467A3DF4
4D565700 6ADF0F0D CF835015 3C04FF7C 21E878AC 11BA9CD2 55A9232C
7CA7B7E6 C1AF74F6 152E99B7 B1FCF9BB E973DE7F 5BDDEB86 C71E3B49
1765308B 5FB0DA06 B92AFE7F 494E8A9E 07B85737 F3A58BE1 1A48A229
C37C1E69 39F08678

80DDCD16 D6BACECA EEBC7CF9 8428787B 35202CDC 60E4616A B623CDBD
230E3AFB 418616A9 4093E049 4D10AB75 27E86F73 932E35B5 8862FDAE
0275156F 719BB2F0 D697DF7F 28

quit

crypto pki certificate chain TP-self-signed-1241688237 certificate
self-signed 01

30820330 30820218 A0030201 02020101 300D0609 2A864886 F70D0101
05050030 31312F30 2D060355 04031326 494F532D 53656C66 2D536967
6E65642D 43657274 69666963 6174652D 31323431 36383832 3337301E
170D3235 31313138 30393134 31395A17 0D333531 31313830 39313431
395A3031 312F302D 06035504 03132649 4F532D53 656C662D 5369676E
65642D43 65727469 66696361 74652D31 32343136

38383233 37308201 22300D06 092A8648 86F70D01 01010500 0382010F
00308201 0A028201 0100AB96 850F4388 B0E30974 14B4193A 6C313E5F
193305BA D05DAAB6 686FB1DC 0AA293EB 38C700D8 37D0C6F3 71B3B033
85814FF1 3A7C8857 7B39AE0A 006FEC33 5199B23C 00DDF6A2 906DCE4D
F3CFE079 A238766E 4A3920AE 18B6A66F B8B5C4C3 0F431D51 654E950C
2D0AFC59 1E6EE613 2872C2B4 80152A2E 9F6B4D19 54AA1444 01148DAB
2C7571E5 362D7F26 C021BDD1 3D5AE729 0312A413 CCD08431 6C102980
601753C9 0011787E EDFABC85 E6D7FA3A 59B26093 71680418 6CF41514
CC28974B C5F6B8F8 A7DB96F3 4BF491F5 1400B712 2E678C8D 90506BEB
41867FDD 1C4206E7 82ABE95A C27DEC01 4D9F31A8 ECC8E311 FB633117
82752ECD 014E946B C313EB2E 31310203 010001A3 53305130 0F060355
1D130101 FF040530 030101FF 301F0603 551D2304 18301680 14C2966C
627DE5E9 9622F729 5556EA47 62194FCB 07301D06 03551D0E 04160414
C2966C62 7DE5E996 22F72955 56EA4762 194FCB07 300D0609 2A864886
F70D0101 05050003 82010100 664C67F4 7087A720 5C3BE3EC C3D27BEB
076A7027 0B4D54DE 62F5C00B 64A5D17E 35BF0DE2 6517342D 6151D986
45A6CCCD 221AEC4B F9A605E8 7C916338 E7B27708 7F6C63DD 0111A97C
B1E94C2B D4281E87 CCB3DAA6 BBF00F96 B4D5A96A 4F82D330 3B049AF9
17036B1E 70A58C04 ECB5F9DF B8EA6998 7F4365F8 8D09C19A 05760129
8032276C 0DA489BD 0AAA87BC B1FAE9BE C0EA32FD 69D53F26 07140D5C
3AC51D5D 6E42E49F 6B7D8C33 17746AE7 2A570B10 A2663B1A 66926E98
B9AE2E95 EE307EDE E939185D 91CE4849 877822C3 2933593A F91F75AD
65A30824 2DDD0D9B 7D6CCE1A D623E746 6DE2B787 61FE16D4 30B9864C
CE3C034A 442B7BA5 FD7E4AD9 580D8BC5
quit !

license boot level network-essentials addon dna-essentials !
!
diagnostic bootup level minimal !
spanning-tree mode rapid-pvst spanning-tree extend system-id
memory free low-watermark processor 10626 !
username etudiant privilege 15 secret 9
\$9\$xdviR7PGKO/CuE\$4eifVfvXhUFtbV9iJuR9L1Ox8tSn5bkbG6RyvSBfRNk
username admin privilege 15 secret 9
\$9\$ofJEE./LtvJgtU\$5RcYRYXC5N/D7pcMYs3M.Pcvhmv7IJP6zt9qIQsF9pM !
redundancy mode sso
! 
!
transceiver type all monitoring
! 
!
class-map match-any system-cpp-police-ewlc-control description EWLC
Control
class-map match-any system-cpp-police-topology-control description
Topology control
class-map match-any system-cpp-police-sw-forward
description Sw forwarding, L2 LVX data packets, LOGGING, Transit Traffic
class-map match-any system-cpp-default
description EWLC data, Inter FED Traffic
class-map match-any system-cpp-police-sys-data
description Openflow, Exception, EGR Exception, NFL Sampled Data, RPF
Failed class-map match-any system-cpp-police-punt-webauth
description Punt Webauth
class-map match-any system-cpp-police-l2lvx-control description L2 LVX
control packets
class-map match-any system-cpp-police-forus description ForusAddress
resolution and Forus traffic
class-map match-any system-cpp-police-multicast-end-station description
MCAST END STATION
class-map match-any system-cpp-police-high-rate-app description High
RateApplications
class-map match-any system-cpp-police-multicast description MCAST Data
class-map match-any system-cpp-police-l2-control description L2 control
class-map match-any system-cpp-police-dot1x-auth description DOT1XAuth
class-map match-any system-cpp-police-data
description ICMP redirect, ICMP_GEN and BROADCAST class-map match-any
system-cpp-police-stackwise-virt-control
description Stackwise Virtual OOB class-map match-any
non-client-nrt-class
class-map match-any system-cpp-police-routing-control description
Routing control and Low Latency
class-map match-any system-cpp-police-protocol-snooping description
Protocol snooping
class-map match-any system-cpp-police-dhcp-snooping description DHCP
snooping
class-map match-any system-cpp-police-ios-routing
description L2 control, Topology control, Routing control, Low Latency
class-map match-any system-cpp-police-system-critical
description System Critical and Gold Pkt
class-map match-any system-cpp-police-ios-feature description
ICMPGEN,BROADCAST,ICMP,L2LVXCntrl,ProtoSnoop,PuntWebauth,MCASTData,Transit,DO
T1XAuth,Swfwd,LOGGING,L2LVXData,ForusTraffic,ForusARP,McastEndStn,Openflow,Excepti
on,EGRExcption,NflSampled,RpfFailed
!
policy-map system-cpp-policy !
! ! ! ! ! ! ! ! ! !
! ! !
interface GigabitEthernet0/0 vrf forwarding Mgmt-vrf no ip address
!
interface GigabitEthernet1/0/1 !
interface GigabitEthernet1/0/2 !
interface GigabitEthernet1/0/3 !
interface GigabitEthernet1/0/4 !
interface GigabitEthernet1/0/5 !
interface GigabitEthernet1/0/6 !
interface GigabitEthernet1/0/7 !
interface GigabitEthernet1/0/8 !
interface GigabitEthernet1/0/9 !
interface GigabitEthernet1/0/10 !
interface GigabitEthernet1/0/11 switchport access vlan 51 switchport
mode access
!
interface GigabitEthernet1/0/12 !
interface GigabitEthernet1/0/13 switchport access vlan 33 switchport
mode access
!
interface GigabitEthernet1/0/14 !
interface GigabitEthernet1/0/15 !
interface GigabitEthernet1/0/16 !
interface GigabitEthernet1/0/17 !
interface GigabitEthernet1/0/18 !
interface GigabitEthernet1/0/19 !
interface GigabitEthernet1/0/20 !
interface GigabitEthernet1/0/21
!
interface GigabitEthernet1/0/22 !
interface GigabitEthernet1/0/23 !
interface GigabitEthernet1/0/24 switchport mode trunk
!
interface GigabitEthernet1/1/1 !
interface GigabitEthernet1/1/2 !
interface GigabitEthernet1/1/3 !
interface GigabitEthernet1/1/4 !
interface Vlan1
ip address 192.168.2.1 255.255.255.0 !
interface Vlan10
ip address 192.168.1.190 255.255.255.192 ip helper-address 192.168.1.1
ip helper-address 192.168.1.2 !
interface Vlan20
ip address 192.168.1.206 255.255.255.240 ip helper-address 192.168.1.1
ip helper-address 192.168.1.2 !
interface Vlan33
ip address 192.168.11.253 255.255.255.240 !
interface Vlan51
ip address 192.168.1.126 255.255.255.128 !
ip forward-protocol nd ip http server
ip http secure-server
ip route 0.0.0.0 0.0.0.0 192.168.11.254 ip ssh version 2
! ! ! !
radius server RADIUS1
address ipv4 192.168.1.120 auth-port 1812 acct-port 1813 key
motdepasse
! ! !
control-plane
service-policy input system-cpp-policy
! !
line con 0 stopbits 1
line aux 0 line vty 0 4
transport input ssh line vty 5 15
transport input ssh !
call-home
! If contact email address in call-home is configured as
sch-smart-licensing@cisco.com
! the email address configured in Cisco Smart License Portal will be
used as contact email address to send SCH notifications.
contact-email-addr sch-smart-licensing@cisco.com profile "CiscoTAC-1"

active

destination transport-method http
! ! ! ! ! !
end
