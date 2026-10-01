---
titre: "Mission N3 — Haute disponibilité de l'application de suivi des visites"
tags: [eleves, u6, mission, gsb, N3, haute-disponibilite, haproxy, replication]
mission: N3
duree: "≈ 22 h (socle 16 h + extension 6 h)"
public: étudiants
---

# 🛡️ Mission N3 — Haute disponibilité de l'application de suivi des visites

> Conventions : [[conventions-gsb]] · Contexte : [[fiche-gsb]] · Retour : [[README]]

## 🪪 Fiche d'identité de la mission

| | |
|---|---|
| **Intitulé** | Rendre l'application de suivi des visites tolérante aux pannes |
| **Présentation rapide** | **Répartir la charge** sur deux serveurs web, **répliquer la base de données** et **tester les bascules**, tout en **administrant les serveurs à distance** de façon sécurisée |
| **Durée** | **Socle** (lots 1, 2 et 4) ≈ 16 h · **Extension** (lot 3) ≈ 6 h |
| **Modalités de réception** | Recette sur ton laboratoire + dossier technique + présentation orale |
| **Équipe** | Individuel ou binôme (précise ta part personnelle) |

---

## 1. 🎯 Le besoin de GSB

L'application de suivi des visites et des frais devient **l'outil quotidien** de toute la force commerciale, sur l'ensemble du territoire. Une panne **immobilise des centaines de visiteurs** et retarde le remboursement de leurs frais. Les données de l'entreprise sont **stratégiques** : elles ne tolèrent **ni fuite ni destruction**, et l'entreprise met déjà en œuvre des redondances (RAID, alimentation, liens réseau, clustering) pour atteindre une **tolérance aux pannes maximale**.

La DSI demande que l'application **continue de fonctionner** si un serveur web tombe, et que la **base de données** soit **répliquée** pour pouvoir reprendre l'activité rapidement.

**Questions de ton analyse :** quelle **indisponibilité maximale** est acceptable (RTO) ? Combien de données peut-on perdre (RPO) ? Quel est l'**impact** de l'ajout d'un répartiteur sur l'architecture existante ? Les données personnelles sont-elles protégées sur les **copies** ?

---

## 2. 🧱 Ce qu'il faut mettre en place

### Lot 1 — Serveurs web et répartition de charge (socle, ≈ 8 h)
- **Deux serveurs web** identiques qui hébergent l'application de référence.
- Un **répartiteur de charge** (par exemple HAProxy) en **HTTPS**, avec **vérification de l'état** des serveurs.
- Le **maintien de session** si l'application l'exige.
- Une **administration à distance sécurisée** : connexion **par clé**, accès limité au VLAN d'administration, **journal des connexions**.

### Lot 2 — Base de données répliquée (socle, ≈ 6 h)
- Une **base de données** (MariaDB par exemple) avec **réplication** vers un second serveur.
- Une **procédure de bascule** vers le serveur répliqué, **écrite et testée**.
- La **mesure du délai** de reprise.

### Lot 4 — Plan de continuité (socle, ≈ 2 h)
- Les **objectifs** de reprise (RTO, RPO) et leur **justification**.
- Les **procédures** : panne d'un serveur web, panne de la base, retour à la normale.
- Un **tableau des pannes testées** et des résultats.

### Lot 3 — Redondance du répartiteur (extension, ≈ 6 h)
- **Deux répartiteurs** partageant une **adresse virtuelle** (VRRP, par exemple avec keepalived).
- Le **test de la panne du répartiteur principal** et la **mesure** du temps de bascule.

---

## 3. ⚙️ Contraintes

- **L'application doit rester accessible** pendant la panne d'un serveur web, **sans intervention humaine**.
- **Pas de simulation seule** : les services tournent sur des machines du laboratoire.
- **Aucune modification du code** de l'application : elle sert de **charge de travail**.
- **Chaque panne testée est documentée** : date, action, observation, délai de reprise.
- **Outils :** libres (HAProxy, Apache ou Nginx, MariaDB, keepalived, `ab` ou `hey` pour la charge).

---

## 4. ✅ Résultats attendus (tes tests de recette)

1. Je dois pouvoir **ouvrir l'application** en HTTPS à travers le répartiteur.
2. Je dois pouvoir **arrêter un serveur web** : l'application **reste accessible** et je peux le **prouver**.
3. Je dois pouvoir **montrer la répartition** des requêtes entre les deux serveurs.
4. Je dois pouvoir **arrêter la base principale**, **basculer** sur la réplique et **retrouver les données**.
5. Je dois pouvoir **annoncer le délai de reprise mesuré** et le comparer à l'objectif fixé.
6. Je dois pouvoir **me connecter à un serveur** uniquement par clé, depuis le réseau d'administration, et **montrer le journal**.
7. *(extension)* Je dois pouvoir **arrêter le répartiteur principal** : l'adresse virtuelle passe sur le second et le service reprend.

---

## 5. 📤 Ce que tu fournis

Les livrables communs ([[conventions-gsb]] §4), plus :
- le **schéma d'architecture** (serveurs, répartiteur, base, adresses) ;
- le **dossier de choix** (par exemple réplication simple ou grappe de bases) ;
- le **tableau des pannes testées** avec les délais mesurés ;
- les **procédures** de bascule et de retour à la normale ;
- le **test de charge** (nombre de requêtes, résultats).

---

## 6. 🎓 Ce que cette mission te permet de montrer

| Famille | Sous-compétences (n° → [[conventions-gsb]] §7) |
|---|---|
| **Concevoir** | 1, 2 (impact), 3, **4**, 5, 6 |
| **Installer, tester, déployer** | 7, **8** (continuité), **9** (qualité de service), 10, 11, 12 |
| **Exploiter, dépanner, superviser** | **13** (administration à distance), 16 (incident) ; 14, 15 et 17 en partie |

---

## 7. ⚠️ Pièges à éviter

- **Croire qu'une réplication est une sauvegarde** : une suppression se réplique aussi. Précise ce que la réplication protège et ce qu'elle ne protège pas.
- **Ne jamais tester la bascule** : une redondance non testée n'est pas une redondance.
- **Un répartiteur unique** : tu as déplacé le point de panne unique sans le supprimer (c'est l'objet de l'extension).
- **Des sessions perdues** à chaque bascule : vérifie le comportement vu par l'utilisateur.
