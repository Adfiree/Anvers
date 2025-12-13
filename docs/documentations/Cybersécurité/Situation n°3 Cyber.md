# Situation n°3 Cybersécurité

**Auteur :** Matéo Beaugendre  
**Date de création :** 13/12/2025  

---
![Logo CUB](../../media/CUB.png)


### Question 1 : Rédiger la table de routage du par-feu Stormshield de votre agence.

## par feu stormshield 

| Type | Destination | Masque | Passerelle | Interface |
| ----- | ----- | ----- | ----- | ----- |
| Par défaut | 0.0.0.0 | 0.0.0.0 | 192.36.253.254 | 192.36.253.10 |
| C | 192.168.11.0 | 255.255.255.0 | 192.168.11.254 | 192.168.11.254 |
| C | 192.36.253.0 | 255.255.255.0 | 192.36.253.10 | 192.36.253.10 |
| C | 192.36.1.0 | 255.255.255.0 | 192.36.1.254 | 192.36.1.254 |
| S | 192.168.1.0 | 255.255.255.0 | 192.168.11.253 | 192.168.11.254 |



### Question 2 : Déterminer quelle adresse IP du WAN doit servir de passerelle pour aller sur internet ? Puis créer un objet réseau afin que cette adresse IP soit représentée dans l’interface d’administration.

L’ip du WAN qui doit servir de passerelle sur internet est l’ip 192.36.253.254/24

l’objet a été créé : 

![S3-1](../../media/Cybersécurité/S3-1.png)



### Question 3 : Utiliser cet objet afin de pouvoir implémenter la table de routage sur votre par-feu.  

![S3-2](../../media/Cybersécurité/S3-2.png)



### Question 4 : Proposer et paramétrer une solution technique permettant aux adresses IP privées de votre site de pouvoir communiquer sur le réseau WAN public et internet 

![S3-3](../../media/Cybersécurité/S3-3.png)



### Question 5 : Peut-on joindre le par-feu général CUB puis les serveurs présents dans sa DMZ. 

Oui nous pouvons joindre le par-feu ainsi que les serveurs sur la DMZ vous que sur le par-feu nous avons renseigné la table de routage avec les routes connecter et les route statique. Cela a permit de pouvoir joindre les serveurs sur la DMZ.

Réponse du Par-feu depuis un poste dans le vlan client

![S3-4](../../media/Cybersécurité/S3-4.png)


Réponse du serveur DNS depuis un poste dans le vlan client

![S3-5](../../media/Cybersécurité/S3-5.png)


Réponse du serveur WEB depuis un poste dans le vlan client

![S3-6](../../media/Cybersécurité/S3-6.png)


### Question 6 : Proposer et paramétrer une solution technique permettant aux services WEB et FTP de votre DMZ d'être interrogés par le réseau WAN. 

la solution est d’effectuer un ping d’un client vers la passerelle de la DMZ

![S3-7](../../media/Cybersécurité/S3-7.png)



### Question 7 : Réaliser une recette permettant de valider les objectifs de la situation 3. 

Les objectifs de la situation 3 est d’avoir accès à internet avec notre agence et pouvoir réussir à interroger notre service WEB depuis le réseau public.

- Avoir accès à internet via un client

![S3-8](../../media/Cybersécurité/S3-8.png)


- Réponse de notre serveur WEB via le réseau public client

![S3-9](../../media/Cybersécurité/S3-9.png)


### Question 8 : Pour conclure, lister les objets réseaux implicites et explicites dont vous avez eu besoin de mobiliser précédemment.

Les objets implicites sont : 

![S3-10](../../media/Cybersécurité/S3-10.png)


Les objets explicite sont : 

Internet

![S3-11](../../media/Cybersécurité/S3-11.png)