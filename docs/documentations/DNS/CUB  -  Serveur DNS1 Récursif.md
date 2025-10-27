# Serveur DNS Recursif Matéo

**Auteurs :** Matéo Beaugendre
**Date de création :** 15/10/2025

---

![Logo CUB](../../media/CUB.png)

## Administration et exploitation des services

## Activité 1 - Mise en place de serveur DNS au sein de l’entreprise CUB

### Partie 1 : Réaliser un nouveau schéma logique

![Logo Schéma Logique](../../media/SchémaLogique2.png)

---

### Partie 2 : Installation et paramétrage du serveur DNS(1) récursif

#### 1. Mise a jour de son serveur 

***Mettez à jour notre serveur***

 - sudo apt update && sudo apt upgrade

***Sur votre serveur Debian 12, installez le service de journalalisation rsyslog à la place de journalctl. Cela vous permettra de disposer de fichiers de log clairs au format texte situés dans /var/log.***

- sudo apt install rsyslog 

#### 2. Définir les paramètres réseaux du serveur 

- sudoedit /etc/network/interfaces

*\# This file describes the network interfaces available on your system*  
*\# and how to activate them. For more information, see interfaces(5).*

*source /etc/network/interfaces.d/\**

*\# The loopback network interface*  
*auto lo*  
*iface lo inet loopback*

*\# The primary network interface*  
*allow-hotplug ens192*  
*auto ens192*  
*iface ens192 inet static*  
*address 192.168.1.10*  
*netmask 255.255.255.0*  
*gateway 192.168.1.254*

#### 3. Définir le serveur DNS récursif à utiliser


- sudoedit /etc/resolv.conf

Puis mettre 8.8.8.8

- nameserver 8.8.8.8 

***Lorsque le service Unbound sera opérationnel, remplacer 8.8.8.8 par 127.0.0.1 et ajouter ensuite le second serveur récursif produit par votre binôme. ***

#### 4. Prendre en compte les modifications des paramètres réseaux

- sudo systemctl restart networking

#### 5. Configurer correctement les fichiers /etc/hostname et /etc/hosts 

***Le fichier hostname sert à donner un nom à votre serveur.***

- sudoedit /etc/hostname

***Mettre le nom que l’on veut***

- dns0 

- sudoedit /etc/hosts

***Changer la deuxième ligne en mettant le nom de domaine***

*127.0.0.1   localhost*  
*127.0.1.1   dns1.local.agence.cub.sioplc.fr    dns1*

*\# The following lines are desirable for IPv6 capable hosts*  
*::1     localhost ip6-localhost ip6-loopback*  
*ff02::1 ip6-allnodes*  
*ff02::2 ip6-allrouters*

***Il est nécessaire de redémarrer le serveur pour prendre en compte le changement de nom.***

- sudo shutdown -r now

#### 6. Installer Unbound et les outils d'administration appropriés

- sudo apt install unbound dnsutils tcpdump tmux curl

#### 7. Configurer Unbound 

- sudoedit /etc/unbound/unbound.conf

***Il est important de vérifier ensuite que la syntaxe des lignes contenues dans le fichier de configuration est correcte. Pour cela, il existe la commande (unbound-checkconf).***

- sudo unbound-checkconf

***Notre serveur récursif va nativement s’adresser aux serveurs faisant autorité sur Internet en sollicitant en premier l’un des serveurs racines. Dans le cas où le serveur récursif serait amené à devoir traiter des domaines locaux qui se trouvent en dehors de l’arborescence DNS réelle (ex : btssio.lan ou epoka.local), il est important de l’indiquer dans le fichier de configuration (/etc/unbound/unbound.conf) de la manière suivante : ***

*\# Comme le domaine btssio.lan est local et en dehors de l’arborescence officielle, il est indispensable*  
*\# d'indiquer au récursif qu'il doit contacter les serveurs internes faisant autorité*  
*\# sur cette zone plutot que l'un des serveurs racines.*

*\# On precise ici que le domaine local ne gère pas DNSSEC et qu’il faut donc desactiver la verification*   
*\# realisee par Unbound*  
*domain-insecure: "btssio.lan."*  
*private-domain: btssio.lan.*

*stub-zone:*  
*name: "btssio.lan."*  
*stub-addr: 172.16.20.10*  
*stub-addr: 172.16.20.11*

***On récupère les adresses des serveurs racines et nous les stockons dans le fichier /var/lib/unbound/root.hints. Ce fichier est indispensable et permet au service Unbound de savoir comment contacter le serveur racine le plus proche ou rapide.***

- sudo curl \--output /var/lib/unbound/root.hints 
- sudo chown \-R unbound:unbound /var/lib/unbound/*

***On crée le fichier de log spécifique à Unbound.***

- sudo touch /var/log/unbound.log
- chown unbound:unbound /var/log/unbound.log
- sudo systemctl restart unbound 
- sudo systemctl status unbound


***Sur les systèmes Debian récents, un logiciel de sécurité de type MAC (Mandatory Access Control) nommé AppArmor est activé par défaut. Il surveille entre autres les droits d’accès des différents processus lancés sur le système. Par défaut, AppArmor empêche le service unbound de lire et d’écrire dans le répertoire /var/log/. Il est donc indispensable de changer ces permissions.***

- sudoedit /etc/apparmor.d/usr.sbin.unbound

***On vérifie que le nouveau fichier de configuration de AppArmor ne contient pas d’erreurs puis on redémarre le service.***

- sudo apparmor_parser -r /etc/apparmor.d/usr.sbin.unbound  
- sudo systemctl restart apparmor

***Si l’on souhaite observer les événements journalisés : ***

- sudo cat /var/log/unbound.log

***Si l’on souhaite observer les derniers évènements enregistrés dans le fichier de log en temps réel :***

- sudo  tail -f /var/log/unbound.log

### Partie 3 : test du serveur DNS Récursif

***Pour réaliser les commandes afin de tester le DNS il faudra etre placer sur le vlan production ou sont placer les serveur DNS Récursif.***

Les commandes a utiliser : 

- dig dns
- dig 192.168.1.10
- dig 192.168.1.11
- dig @192.168.1.10 google.com

Une fois les commandes réussi votre DNS récursif sera opérationnel.

