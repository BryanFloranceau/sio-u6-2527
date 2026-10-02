---
titre: "Mission E1 — Architecture technique : héberger l'application de suivi des visites"
tags: [eleves, u6, mission, gsb, E1, web, dmz, https]
mission: E1
duree: "≈ 16 h"
origine: "Inspirée d'une fiche du réseau CERTA (2012), réécrite et actualisée"
public: étudiants
---

# 🌐 Mission E1 — Architecture technique : héberger l'application de suivi des visites

> Conventions : [[conventions-gsb]] · Contexte : [[fiche-gsb]] · Retour : [[README]]

## 🪪 Fiche d'identité de la mission

| | |
|---|---|
| **Intitulé** | Mise en place de l'architecture technique qui héberge en interne l'application de suivi des visites |
| **Présentation rapide** | Installer un **serveur web sécurisé**, une **base de données sur un autre serveur** et un **service de dépôt de fichiers** réservé à l'interne, le tout organisé autour d'une **DMZ** |
| **Durée** | ≈ **16 h** (3 lots) |
| **Origine** | Mission du réseau CERTA (2012), **réécrite** avec des outils actuels |
| **Modalités de réception** | Recette sur ton laboratoire + dossier technique + présentation orale |
| **Équipe** | Individuel ou binôme (précise ta part personnelle) |

---

## 1. 🎯 Le besoin de GSB

Les **visiteurs médicaux** vont saisir leurs comptes rendus et leurs frais dans une **application web**, produite par le service Développement. Il faut l'**héberger en interne**, la rendre joignable par Internet depuis `visite.gsb.coop`, et **protéger** les données qu'elle manipule.

Les données de l'application (praticiens, frais, personnel) sont **sensibles**. Seuls les **acteurs de l'entreprise** doivent y accéder, **après authentification**. Le service Développement doit pouvoir **mettre à jour le site** sans accéder au reste du système.

**Questions de ton analyse :** quelles données sont traitées ? Quel **cadre juridique** s'applique ? Qui accède à quoi ? Quel est le **risque principal** d'un serveur exposé sur Internet ?

---

## 2. 🧱 Ce qu'il faut mettre en place

### Lot 1 — Serveur web et base de données (≈ 6 h)
- Un **serveur web** en **HTTPS** (certificat à créer), qui exécute des scripts côté serveur.
- Une **base de données sur un serveur distinct** du serveur web.
- Chaque composant est installé **séparément** (pas de pile « tout-en-un » préconfigurée).
- L'application de référence fournie par le formateur est déployée et fonctionne.

### Lot 2 — Accès sécurisés et DMZ (≈ 6 h)
- Une **DMZ** pour le serveur web, la base restant sur le réseau interne, avec un **pare-feu** entre les deux.
- Un **service de dépôt de fichiers** (FTP sécurisé ou SFTP) **réservé à l'accès interne**, avec **authentification** (annuaire ou base de comptes).
- L'accès à l'application **réservé aux acteurs de l'entreprise** : **authentification préalable**, de préférence par **certificat**.
- Les données ne sont accessibles **que par le serveur web**, jamais directement.
- Un **nom de domaine** pertinent pour l'application (`visite.gsb.coop`) résolu par le DNS du laboratoire.

### Lot 3 — Exploitation, documentation et recette (≈ 4 h)
- Des **fichiers de configuration épurés et commentés**.
- Les **opérations répétitives dans des scripts** (création de la base, des utilisateurs, des certificats).
- Une **fiche de configuration** (adressage, comptes) **sans mot de passe** ; les secrets sont remis à part.
- Un **plan de tests** et son exécution.

---

## 3. ⚙️ Contraintes

- **Aucun accès direct** à la base depuis Internet ni depuis le serveur web autrement que par son port.
- **Le dépôt de fichiers n'est jamais ouvert** sur Internet.
- **Aucun mot de passe en clair** dans ton dossier ni dans ton dépôt Git.
- **Outils :** libres (Apache ou Nginx, MariaDB ou PostgreSQL, OpenSSL, pare-feu pfSense ou nftables).

---

## 3 bis. 🧰 Ton laboratoire et cette mission

*Tu pars de ce qui existe : **ton serveur web et ta base en grappe sont déjà là**. Remplis la table de correspondance de [[conventions-gsb]] §2 dans ton DAT.*

| Élément de la mission | Souvent déjà en place chez toi | Ce que tu construis |
|---|---|---|
| **Serveurs web** | Déjà installés | Les **intégrer à l'application de référence**, en **HTTPS** avec un certificat que tu crées |
| **Base de données** | Grappe (Galera) sur des serveurs distincts | **Déjà conforme** à « base distincte » : **documente-le** et **prouve** qu'elle n'est pas joignable depuis Internet |
| **Pare-feu et DMZ** | pfSense, zones | Des **règles justifiées** entre Internet, la DMZ et la base |
| **Dépôt de fichiers** | — | Un **SFTP réservé à l'interne**, avec authentification |
| **Authentification par certificat** | — | Une **autorité interne** et des certificats clients |
| **Scripts** | PowerShell pour l'annuaire | Des scripts pour la base, les utilisateurs et les certificats |

**Ta réalisation :** l'**application sécurisée de bout en bout** (HTTPS, authentification, dépôt interne, règles justifiées). Le simple fait d'avoir un serveur web et une base ne suffit pas.

---

## 4. ✅ Résultats attendus (tes tests de recette)

1. Je dois pouvoir **ouvrir l'application** en HTTPS et **prouver** que la liaison est chiffrée.
2. Je dois pouvoir **prouver** que la base de données est sur un **autre serveur** et qu'elle n'est **pas joignable** depuis Internet.
3. Je dois pouvoir **prouver** qu'un utilisateur **non authentifié** n'accède à aucune donnée.
4. Je dois pouvoir **déposer un fichier** depuis le réseau interne et **montrer** que la même opération échoue depuis Internet.
5. Je dois pouvoir **recréer la base et les certificats** en lançant mes scripts.
6. Je dois pouvoir **expliquer chaque règle du pare-feu** et la justifier.

---

## 5. 📤 Ce que tu fournis

Les livrables communs ([[conventions-gsb]] §4), plus :
- le **schéma d'architecture** (DMZ, réseau interne, flux) ;
- la **fiche de configuration** (sans secret) ;
- les **scripts** et les fichiers de configuration commentés ;
- le **mode opératoire de mise à jour** du site par l'équipe de développement.

---

## 6. 🎓 Ce que cette mission te permet de montrer

| Famille | Sous-compétences (n° → [[conventions-gsb]] §7) |
|---|---|
| **Concevoir** | 1, 3, 5, 6 ; 2 et 4 en partie |
| **Installer, tester, déployer** | 7, 10, 11 ; 12 en partie |
| **Exploiter, dépanner, superviser** | 13 et 14 en partie |

*Cette mission est **forte en conception et en installation**. Elle ne porte pas à elle seule l'exploitation (supervision, incident) : **associe-la à une seconde mission** qui la porte (par exemple [[N4-supervision-qualite-service]]).*

---

## 7. ⚠️ Pièges à éviter

- **Une base de données sur le même serveur que le web** : la mission l'interdit.
- **Un certificat auto-signé jamais expliqué** : dis pourquoi c'est acceptable en laboratoire et ce qu'il faudrait en production.
- **Un dépôt de fichiers accessible depuis l'extérieur** : c'est l'erreur la plus fréquente.
