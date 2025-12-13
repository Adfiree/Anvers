# Situation n°6 Cybersécurité

**Auteur :** Matéo Beaugendre  
**Date de création :** 13/12/2025  

---
![Logo CUB](../../media/CUB.png)



| N° | interface | sens | @ ip  source | port S | @ ip destination | Port D | Proto | statut | Action |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | :---: | ----- |
| Section 1 \- règles d’autorisation à destination du pare feu |  |  |  |  |  |  |  |  |  |
| 6 règle 4 | 192.168.11.254 | entré | 192.168.1.192/28 | \* | 192.168.11.254 | 443 | TCP | nouvelle | Auto |
| Section 3 \- Règles de protection du pare feu |  |  |  |  |  |  |  |  |  |
| 3 | 192.36.253.10 | entré | \* | \* | 192.36.253.10 | \* | \* | nouvelle | Bloquer |
| 3 | 192.36.1.254 | entré | \* | \* | 192.36.1.254 | \* | \* | nouvelle | Bloquer |
| 6 règle 4 | 192.168.11.254 | entré | 192.168.1.128 /26 | \* | 192.168.11.254 | \* | \* | nouvelle | Bloquer |
| Section 4 \- Règles d’autorisation des flux métiers |  |  |  |  |  |  |  |  |  |
| 3 règle 1 | 192.168.11.254 | entré | 192.168.1.0/24 | \* | 192.36.1.20/24 | 80,443 | tcp | nouvelle | autoriser |
| 4 règle 2 | 192.168.11.254 | entré | 192.168.1.192/28 | \* | 192.36.1.0/24 | \* | \* | nouvelle | autoriser |
| 5 règle 3 | 192.168.11.254 | entré | 192.168.1.0/24 | \* | \* | 123 | UDP | nouvelle | autoriser |
| 6 règle 5 | 192.168.11.254 | entré | 192.168.1.10 192.168.1.11 | \* | \* | 53 | UDP | nouvelle | autoriser |
| 7 règle 6 | 192.168.11.254 | entré | 192.168.1.0/24 | \* | 192.36.0.0/16 | 80,443 | TCP | nouvelle | autoriser |
| 8 règle 9 | 192.168.11.254 | entré | 192.168.1.0/24 192.168.1.128/26 | \* | internet | 80,443 | TCP | nouvelle | autoriser |
| 4 règle 6 | 192.36.253.10 | entré | 192.36.0.0/16 | \* | 192.36.1.20/24 | 80,443 | TCP | nouvelle | autoriser |
| 5 règle 7 | 192.36.253.10 | entré | 192.36.0.0/16 | \* | 192.36.1.20/24 | 80,443,20,21 | TCP | nouvelle | autoriser |
| 6 règle 8 | 192.36.253.10 | entré | internet | \* | 192.36.1.10/24 192.36.1.11/24 | 53 | UDP | nouvelle | autoriser |
| Section 6 \- Règle d’interdiction finale |  |  |  |  |  |  |  |  |  |
| 9 | \* | entré | \* | \* | \* | \* | \* | nouvelle | Bloquer |

Question A à C  
