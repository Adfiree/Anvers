# Situation n°2 Cybersécurité

**Auteur :** Andy REMY  
**Date de création :** 25/09/2025  

---
![Logo CUB](../../media/CUB.png)

## Administration des systèmes (Cybersécurité)

# Premier paramétrage d’un pare-feu sur un site de l’entreprise 

### Question 1 : Installer vos 3 VM et paramétrer correctement leurs cartes réseaux

J’ai donc créé une VM sous virtualBox Windows 10 puis 2 VM sous nutanix avec les adresses IP correspondant.

Voici l'adresse IP du serveur DNS

![1](../../media/Cybersécurité/S1-1.png)

Voici l’adresse IP du serveur WEB

![2](../../media/Cybersécurité/S1-2.png)

Voici l’adresse IP de mon Windows 10 dans le Vlan Administration

![3](../../media/Cybersécurité/S1-3.png)


### Question 2 : Renommer le pare-feu

Voici le pare-feu renommé correctement

![4](../../media/Cybersécurité/S1-4.png)

### Question 3 : Assurez-vous que la stratégie de complexité des mot de passe préconisée par l’ANSSI et est effective pour le compte administrateur.

J’ai modifié la longueur minimal du mot de passe qui était à 8 par défaut 

![5](../../media/Cybersécurité/S1-5.png)

### Question 4 : Assurez-vous que l’horodatage des événements est bien correct.

J’ai changer le fuseau horaires sur “Europe/Paris”

![6](../../media/Cybersécurité/S1-6.png)

### Question 5 : Pourquoi est-il primordial que l’ensemble des par-feu de l’entreprise CUB soit synchronisé sur les serveurs NTP de l’entreprise Stormshield

Les pare-feu génèrent en permanence des journaux d’événements (connexions, blocages, alertes). 
Si les horloges des différents pare-feu ne sont pas alignées, il devient quasiment impossible de corréler les événements entre eux.
Certains protocoles de sécurité et mécanismes de certificats (TLS/SSL, VPN, authentification Kerberos) reposent sur une horloge précise pour valider la durée de validité des clés et certificats.

Un décalage d’horloge peut empêcher une connexion sécurisée ou ouvrir des failles exploitables.
Utiliser les serveurs NTP de Stormshield garantit que tous les équipements de la gamme partagent la même référence temporelle fiable, réduisant les risques de désynchronisation entre sites et matériels.

### Question 6 : Configurer les interfaces réseaux de l’appliance afin que cela corresponde à ce que vous avez défini précédemment dans votre schéma réseau logique

Voici les interfaces réseaux de l'appliance correctement paramétrées

![7](../../media/Cybersécurité/S1-7.png)

### Question 7 : Dans le menu Filtrage et NAT, appliquer la politique de filtrage(10) Pass All afin d’éviter des blocages ou erreurs liés à cette dernière

Voici la politique de filtrage(10) Pass All

![8](../../media/Cybersécurité/S1-8.png)

### Question 8 : Réaliser une recette de la situation à l’aide de tests de connectivité entre le poste client et les serveurs présents en DMZ

Pour effectuer les tests mon poste a une IP sur le VLan 20 (Administration).
Mais pour effectuer les tests, j’ai utilisé donc ma VM Windows 10 sous VirtualBox dans le Vlan 20.

J'effectue un ping sur la DMZ sur le serveur DNS donc 192.36.1.11

![9](../../media/Cybersécurité/S1-9.png)

J’effectue un ping sur la DMZ sur le serveur WEB donc 192.36.1.21

![10](../../media/Cybersécurité/S1-10.png)