# Situation n°4 Cybersécurité

**Auteur :** Andy REMY  
**Date de création :** 1/10/2025  

---
![Logo CUB](../../media/CUB.png)

## Administration des systèmes (Cybersécurité)

# Cryptographie

### Question 1 : Vérifier la connexion via SSH du pare-feu, switch de niveau 2 et 3

Voici la connexion SSH sur le Stormshield : 

![1](../../media/Cybersécurité/S4-1.png)

![2](../../media/Cybersécurité/S4-2.png)

Nous voyons bien que nous avons accès en SSH depuis PUTTY.
Pour cela, il suffit d’activer l’accès par SSH sur le pare-feu depuis son interface.

![3](../../media/Cybersécurité/S4-3.png)

Ensuite, sur PUTTY, il suffit de renseigner l’adresse IP du pare-feu afin de s’y connecter en SSH.

Pour la Switch de niveau 2 et 3 c’est le même principe pour s’y connecter.
Il suffit de paramétrer le SSH, puis de lancer PUTTY et d’accéder en SSH grâce à leurs adresses IP définies sur le VLAN 1.

Switch 2 : 192.168.3.1
Switch 3 : 192.168.2.1

Exemple pour le Switch 3 : 

![4](../../media/Cybersécurité/S4-4.png)

### Question 2 : Démontrer pour RDP et SSH le respect des critères de sécurité sur la cryptographie

SSH (Secure Shell)

- Confidentialité : le flux est chiffré avec un algorithme symétrique négocié (souvent AES ou ChaCha20), ce qui protège les données contre l’interception.
- Intégrité : l’échange utilise des fonctions de hachage (HMAC-SHA2) pour vérifier que les paquets n’ont pas été altérés.
- Authenticité : le serveur s’identifie grâce à sa clé publique (RSA, ECDSA, Ed25519). Le client peut aussi utiliser une clé publique pour s’authentifier. L’échange de clé (Diffie-Hellman ou  Curve25519) empêche toute interception (attaque de type « man-in-the-middle »).

RDP (Remote Desktop Protocol)

- Confidentialité : les sessions sont protégées par TLS (Transport Layer Security), avec chiffrement symétrique (AES 128 ou 256 bits). Cela garantit que l’écran, le clavier et les données envoyées sont illisibles pour un attaquant.
- Intégrité : TLS assure la vérification des messages grâce à des fonctions de hachage sécurisées (SHA-256).
- Authenticité : le serveur RDP présente un certificat (souvent signé par une autorité de certification). Cela permet au client de vérifier qu’il se connecte bien au bon serveur.

### Question 3 : Vérifier en prouvant l’intégrité de l’identité des matériels lors d’une liaison SSH

Afin de vérifier l’intégrité lors d’une liaison SSH, je vais vérifier ma clé Publique et ma clé Privé qu’elle soit bien identique.

Nous voyon ci dessous la clé publique de mon switch en me connectant en SSH

![5](../../media/Cybersécurité/S4-5.png)

Nous voyons ci-dessous la clé Publique de PUTTY en me connectant en SSH 

![6](../../media/Cybersécurité/S4-12.png)

En comparant les deux, nous voyons bien que les deux clé Publique sont les mêmes et donc assure l’intégrité de l’identité des matériels.

### Question 4 : Préciser l’algorithme de chiffrement utilisé par le serveur SSH.

Le serveur SSH n’utilise pas un seul algorithme fixe. 
Lors de la connexion, le client et le serveur négocient ensemble celui qu’ils vont employer. 
En pratique, les plus courants aujourd’hui sont AES (en mode CTR), ChaCha20-Poly1305 pour le chiffrement symétrique, Diffie-Hellman ou Curve25519 pour l’échange de clés, et SHA 2 pour l’intégrité.

### Question 5 : Schématiser à l’aide d’un diagramme l’échange entre le client et le serveur lors d’une connexion SSH.

![6](../../media/Cybersécurité/S4-6.png)

Pour résumer, le client réalise une connexion SSH au Switch 2 ou 3 ou pare-feu.
Il envoie donc une requête TCP puis le Switch lui donne la Clé Publicue.
Le client, une fois cette clé reçue, il pourra alors chiffrer ses données qu’il envoie sur le Switch grâce à cette clé publique.

Voici une écoute réalisé sur Wireshark

![6](../../media/Cybersécurité/S4-7.png)

### Question 6 : Réaliser une connexion HTTPS sur l’interface d’administration du pare-feu Stormshield.

Pour se connecter en HTTPS sur l’interface du Stormshield, il suffit d’ouvrir votre navigateur Web, puis de taper dans l’url : https://192.168.11.254/

![6](../../media/Cybersécurité/S4-8.png)

Maintenant, il suffit de mettre l’identifiant et le mot de passe suivant : admin et admin.

Voici les éléments présent dans le certificat TLS/SSL

![6](../../media/Cybersécurité/S4-9.png)

![6](../../media/Cybersécurité/S4-10.png)

### Question 7 : Préciser pourquoi lors de la première connexion à l’interface d’administration du pare-feu, un message d’alerte est stipulé

Lors de la première connexion à l’interface d’administration du pare-feu Stormshield, un message d’alerte apparaît parce que le certificat utilisé par le pare-feu pour chiffrer la connexion HTTPS est un certificat auto-signé. Le navigateur ne peut donc pas vérifier son authenticité auprès d’une autorité de certification reconnue, ce qui entraîne un avertissement de sécurité.

### Question 8 : Après avoir rappelé le rôle d’une autorité de certification, préciser la différence entre une autorité de certification reconnue et non-reconnue. Quels sont les avantages et les inconvénients de l’une et l’autre ?

Une autorité de certification (CA) a pour rôle de garantir l’identité d’un serveur ou d’une entité en délivrant des certificats numériques. Ces certificats permettent d’établir une connexion sécurisée et de prouver que le serveur contacté est bien celui qu’il prétend être.
Une CA reconnue est une autorité dont le certificat racine est déjà intégré dans les navigateurs et systèmes d’exploitation. Les certificats qu’elle émet sont automatiquement considérés comme fiables.

Une CA non-reconnue n’est pas incluse dans ces listes de confiance. Le navigateur affiche donc un avertissement tant qu’on n’a pas ajouté manuellement son certificat dans les autorités de confiance locales.

Voici les avantages et les inconvénients : 

![6](../../media/Cybersécurité/S4-11.png)
