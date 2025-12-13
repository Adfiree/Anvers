# Situation n°5 Cybersécurité

**Auteur :** Matéo Beaugendre 
**Date de création :** 13/12/2025  

---
![Logo CUB](../../media/CUB.png)


 ### Question 1 : Rappeler la définition et les enjeux de la notion de moindre privilège pour les comptes d’administrations des serveurs. 

Le **principe du moindre privilège** stipule que :

Chaque utilisateur, application ou service doit disposer uniquement des privilèges (autorisations, accès, droits système) nécessaires pour exécuter ses fonctions légitimes.

Les enjeux du moindre privilège sont : 

- **Réduction de la surface d’attaque**  
Moins de privilèges signifie moins de possibilités d’exploitation en cas de compromission.

- **Limitation des dommages**  
Si un compte est compromis, l’impact est limité aux ressources auxquelles il a effectivement accès.

- **Conformité réglementaire**  
Principe souvent exigé par les normes de sécurité (ISO 27001, ANSSI, RGPD, NIST, etc.).

- **Traçabilité et responsabilité**  
Chaque action peut être attribuée à un utilisateur ou à un rôle précis, facilitant l’audit et la détection d’anomalies.

- **Réduction des erreurs humaines**  
Moins de droits signifie aussi moins de risques d’actions involontaires dangereuses

### Question 2 : Résumer ce qu’est une solution de gestion des accès à privilèges ou PAM en précisant les fonctionnalités de ces composantes. 

**Le PAM vise à appliquer le principe du moindre privilège en encadrant strictement l’accès aux ressources critiques. Il permet de réduire les risques liés aux comptes à privilèges : compromission, abus d’accès, erreurs humaines ou non-conformité réglementaire.**

1. **Gestion et rotation des identifiants privilégiés (Vaulting)**

- Stockage sécurisé des identifiants (coffre-fort chiffré).

- Rotation automatique et régulière des mots de passe.

- Suppression de la connaissance directe des mots de passe par les utilisateurs.

2. **Contrôle des accès privilégiés (Access Control)**

- Attribution temporaire ou à la demande des droits élevés (« *Just-in-Time Access* »).

- Gestion des autorisations selon les rôles et les contextes.

- Validation ou approbation préalable avant certaines opérations sensibles.

3. **Surveillance et enregistrement des sessions (Session Management & Recording)**

- Journalisation complète des connexions privilégiées.

- Enregistrement vidéo ou textuel des actions réalisées.

- Alertes en cas de comportement suspect ou non conforme.

4. **Audit et traçabilité (Audit & Reporting)**

- Rapports détaillés sur l’usage des comptes à privilèges.

- Aide à la conformité (ISO 27001, NIST, RGPD, ANSSI…).

- Analyse post-incident pour identifier les causes d’une faille.

5. **Élévation et délégation de privilèges (Privilege Elevation & Delegation Management)**

- Permet à un utilisateur d’obtenir temporairement des privilèges spécifiques sans utiliser un compte admin complet.

- Réduit l’usage de comptes partagés ou permanents.

### Question 3 : Préciser les bonnes pratiques à respecter lors de la mise en place d’une solution PAM.

Les bonnes pratiques à respecter lors de la mise en place d’une solution **PAM** sont : 

Dans un premier temps définir une politique claire de gestion des comptes à privilèges , Séparer les comptes et les usages ,Sécuriser la gestion des identifiants,  
Contrôler et limiter l’accès aux privilèges,Surveiller et auditer en continu,Intégrer le PAM dans l’écosystème de sécurité et il est important d’accompagner et former les utilisateurs.

### Question 4 : Expliquer le lien entre une solution PAM et la mise en place d’un SIEM/SOC

Une solution PAM, en contrôlant et en enregistrant toutes les actions réalisées via les comptes à privilèges, fournit au SIEM des journaux détaillés et horodatés permettant la corrélation avec d’autres événements de sécurité, ce qui offre au SOC une visibilité complète sur les activités sensibles, facilite la détection des comportements anormaux, renforce la traçabilité et la conformité, et permet ainsi une supervision proactive et une réaction rapide en cas d’incident.

### Question 5 : Retrouver dans la documentation de l’ANSSI sur “ les recommandations relatives à l'administration sécurisée des SI ” la partie consacrée à la mise en place d’un bastion. Relever la première mise en garde et indiquer en quoi la solution WALLIX est-elle une solution recommandée pour CUB. 

La solution WALLIX est recommandée car il a été certifié CSPN (Certification de Sécurité de Premier Niveau) par l’ANSSI, ce qui garantit que la solution a été évaluée sur plusieurs menaces notables et qu’elle répond à des exigences formelles de sécurité en matière de contrôle d’accès, cryptographie, intégrité des journaux, etc.  
Il permet de centraliser les accès à privilèges, d’en assurer la traçabilité et le renouvellement des secrets.

Ainsi que d’isoler le bastion dans une zone de confiance du SI (par exemple dans le SI administratif / infrastructure, non sur le réseau bureautique exposé) et de respecter le principe du moindre privilège, d’utiliser des accès temporaires ou limités selon les rôles, etc.

