# Configuration Switch de niveau 2

version 12.2  
no service pad  
service timestamps debug datetime msec  
service timestamps log datetime msec  
no service password-encryption  
\!  
hostname Switch  
\!  
boot-start-marker  
boot-end-marker  
\!  
\!  
username etudiant privilege 15 secret 5 $1$7v2z$LsWa45oQRVxxlczNWk9fL.  
\!  
\!  
no aaa new-model  
system mtu routing 1500  
\!  
\!  
ip domain-name btssio.lan  
\!  
\!  
\!  
\!  
\!  
\!  
spanning-tree mode pvst  
spanning-tree extend system-id  
\!  
vlan internal allocation policy ascending  
\!  
ip ssh version 2  
\!  
interface FastEthernet0/1  
 switchport access vlan 10  
\!  
interface FastEthernet0/2  
\!  
interface FastEthernet0/3  
\!  
interface FastEthernet0/4  
\!  
interface FastEthernet0/5  
\!  
interface FastEthernet0/6  
\!  
interface FastEthernet0/7  
\!  
interface FastEthernet0/8  
\!  
interface FastEthernet0/9  
\!  
interface FastEthernet0/10  
\!  
interface FastEthernet0/11  
\!  
interface FastEthernet0/12  
\!  
interface FastEthernet0/13  
 switchport access vlan 20  
\!  
interface FastEthernet0/14  
\!  
interface FastEthernet0/15  
\!  
interface FastEthernet0/16  
\!  
interface FastEthernet0/17  
\!  
interface FastEthernet0/18  
\!  
interface FastEthernet0/19  
\!  
interface FastEthernet0/20  
\!  
interface FastEthernet0/21  
\!  
interface FastEthernet0/22  
\!  
interface FastEthernet0/23  
\!  
interface FastEthernet0/24  
\!  
interface FastEthernet0/25  
\!  
interface FastEthernet0/26  
\!  
interface FastEthernet0/27  
\!  
interface FastEthernet0/28  
\!  
interface FastEthernet0/29  
\!  
interface FastEthernet0/30  
\!  
interface FastEthernet0/31  
\!  
interface FastEthernet0/32  
\!  
interface FastEthernet0/33  
\!  
interface FastEthernet0/34  
\!  
interface FastEthernet0/35  
\!  
interface FastEthernet0/36  
\!  
interface FastEthernet0/37  
\!  
interface FastEthernet0/38  
\!  
interface FastEthernet0/39  
\!  
interface FastEthernet0/40  
\!  
interface FastEthernet0/41  
\!  
interface FastEthernet0/42  
\!  
interface FastEthernet0/43  
\!  
interface FastEthernet0/44  
\!  
interface FastEthernet0/45  
\!  
interface FastEthernet0/46  
\!  
interface FastEthernet0/47  
\!  
interface FastEthernet0/48  
\!  
interface GigabitEthernet0/1  
 switchport mode trunk  
\!  
interface GigabitEthernet0/2  
\!  
interface Vlan1  
 ip address 192.168.3.1 255.255.255.0  
 no ip route-cache  
\!  
ip http server  
ip http secure-server  
\!  
line con 0  
line vty 0 4  
 login local  
 transport input ssh  
line vty 5 15  
 login  
\!  
end

