# Serveur DNS Recursif ANDY

**Auteurs :** Andy REMY
**Date de création :** 09/10/2025

---

![Logo CUB](../../media/CUB.png)

## Administration et exploitation des services

## Activité 1 - Mise en place du serveur DNS faisant Autorité au sein de l’entreprise CUB

---

### Partie 1 : Réaliser un nouveau schéma logique

![](../../media/a1.png)

### Partie 2 : Installation et paramétrage du serveur DNS faisant Autorité

#### 1 - Vérification préalable

Mettez à jour votre serveur

- sudo apt update && sudo apt upgrade

![](../../media/a2.png)

Sur votre serveur Debian 12, installez le service de journalisation rsyslog à la place de journalctl. Cela vous permettra de disposer de fichiers de log clairs au format texte situés dans /var/log.

- sudo apt install rsyslog

![](../../media/a3.png)

Installez le service Bind9 et les outils diagnostics DNS

- sudo apt install bind9 dnsutils

![](../../media/a4.png)

#### 2 - Définir les paramètres réseaux du serveur

- sudoedit /etc/network/interfaces

![](../../media/a5.png)

#### 3 - Définir le serveur DNS récursif à utiliser

- sudoedit /etc/resolv.conf

![](../../media/a6.png)

#### 4 - Prendre en compte les modifications des paramètres réseaux

- sudo systemctl restart networking

![](../../media/a7.png)

#### 5 - Configurer correctement les fichiers /etc/hostname et /etc/hosts

Le fichier **hostname** sert à donner un nom à votre serveur.

- sudoedit /etc/hostname

![](../../media/a8.png)

- sudoedit /etc/hosts

![](../../media/a9.png)

Il est nécessaire de redémarrer le serveur pour prendre en compte le changement de nom.

- sudo shutdown \-r now

![](../../media/a10.png)

#### 6 - Exemple de configuration d'un serveur DNS maître faisant autorité

- sudo cat /etc/bind/named.conf

![](../../media/a11.png)

- sudo nano /etc/bind/named.conf.options

![](../../media/a12.png)

- sudoedit /etc/bind/named.conf.local

![](../../media/a13.png)

Ce fichier sert à déclarer les zones que vous aurez à gérer. Votre serveur peut-être maître sur une zone ou esclave. La directive file sert à déclarer le fichier de zone contenant les enregistrements liés (SOA, NS, A…). La directive allow-transfer permet de déclarer les serveurs esclaves habilités.

- sudoedit /var/cache/bind/db.anvers.cub.sioplc.fr

![](../../media/a14.png)

- sudo chown bind:bind /var/cache/bind/db.anvers.cub.sioplc.fr

![](../../media/a15.png)

Mise en place d’une journalisation des événements du service DNS

- sudoedit /etc/bind/named.conf.log

![](../../media/a16.png)

Ce fichier permet d'activer la journalisation des évènements pour le service DNS. Vous pouvez préciser le niveau de verbosité avec la directive severity mais aussi la taille maximale du fichier de log. Comme pour le fichier de zone esclave, il est nécessaire de créer un fichier vide de log avec les bonnes permissions au préalable

- sudo touch /var/log/bind.log

![](../../media/a17.png)

- sudo chown bind:bind /var/log/bind.log

![](../../media/a18.png)

Enfin, on n’oublie pas de déclarer ce nouveau fichier de configuration dans /etc/bind/named.conf.

- sudoedit /etc/bind/named.conf

![](../../media/a19.png)

- sudoedit /etc/apparmor.d/usr.sbin.named

![](../../media/a20.png)

On vérifie que le nouveau fichier de configuration de AppArmor ne contient pas d’erreurs puis on redémarre le service.

- sudo apparmor\_parser \-r /etc/apparmor.d/usr.sbin.named  
- sudo systemctl restart apparmor

![](../../media/a21.png)

- sudo named-checkconf \-z  
- sudo systemctl restart bind9  
- sudo systemctl status bind9

![](../../media/a22.png)

Voilà, notre serveur DNS faisant autorité maître est opérationnel \!\!

### Partie 3 : Test du serveur DNS faisant Autorité (maître)

Test de la résolution DNS

- dig 192.36.1.10 anvers.cub.sioplc.fr

![]![](../../media/a23.png)

Test du Sérial SOA

- dig 192.36.1.10 [anvers.cub.sioplc.fr](http://anvers.cub.sioplc.fr) SOA \+short

Cette commande permet de voir le numéro SERIAL de votre DNS, le but est que le DNS esclave ai le même SERIAL que le maître comme ci dessous :  
![](../../media/a24.png)

![](../../media/a25.png)

![](../../media/a26.png)

![](../../media/a27.png)

![](../../media/a28.png)

Test pour les serveur DNS Récursif :

![](../../media/a29.png)

![](../../media/a30.png)

Nos serveurs DNS Maître et esclave sont maintenant opérationnels.