---
titre: "Mission E2 — Assistance : mettre en place la cellule d'assistance (helpdesk)"
tags: [eleves, u6, mission, gsb, E2, helpdesk, glpi, incident]
mission: E2
duree: "≈ 12 h"
origine: "Inspirée d'une fiche du réseau CERTA (2012), réécrite et actualisée"
public: étudiants
---

# 🎧 Mission E2 — Assistance : mettre en place la cellule d'assistance

> Conventions : [[conventions-gsb]] · Contexte : [[fiche-gsb]] · Retour : [[README]]

## 🪪 Fiche d'identité de la mission

| | |
|---|---|
| **Intitulé** | Mise en place d'une cellule d'assistance pour les visiteurs médicaux et les services du siège |
| **Présentation rapide** | Installer un **outil de gestion de parc et de tickets**, organiser la **prise en charge d'un incident** et fournir un **tableau de bord** de suivi |
| **Durée** | ≈ **12 h** (3 lots) |
| **Origine** | Mission du réseau CERTA (2012), **réécrite** avec des outils actuels |
| **Modalités de réception** | Recette sur ton laboratoire + dossier technique + présentation orale |
| **Équipe** | Individuel ou binôme (précise ta part personnelle) |

---

## 1. 🎯 Le besoin de GSB

Les **480 visiteurs médicaux** vont utiliser un nouvel outil sur leur ordinateur portable. Ils sont **éloignés du siège**, autonomes, et leur matériel **n'est pas uniformisé**. Quand un problème survient, ils ne savent pas **à qui s'adresser**, et le service informatique n'a **aucune vue d'ensemble** des pannes ni du parc.

GSB veut une **cellule d'assistance** : un point d'entrée unique, des **tickets** suivis de bout en bout, un **inventaire** du matériel et un **tableau de bord** pour piloter l'activité.

**Questions de ton analyse :** qui demande de l'aide, par quels canaux ? Quelles **informations personnelles** sont stockées dans les tickets et l'inventaire ? Qui peut les voir ? Quelle durée de conservation ?

---

## 2. 🧱 Ce qu'il faut mettre en place

### Lot 1 — Choix et installation de l'outil (≈ 4 h)
- Une **comparaison de deux outils** de gestion de parc et de tickets (dossier de choix).
- L'**installation** de l'outil retenu (par exemple GLPI) sur un serveur du laboratoire, avec sa base de données et son serveur web.
- La **sécurisation** de base : accès chiffré, comptes distincts, aucun compte par défaut conservé.

### Lot 2 — Parc, tickets et notifications (≈ 4 h)
- Un **inventaire automatique** d'au moins **trois machines** (agent d'inventaire).
- Les **catégories de demandes** et les **priorités**, avec des **délais de prise en charge**.
- Des **notifications par messagerie** : réception d'un ticket, changement d'état, clôture.
- Un **profil d'utilisateur** et un **profil de technicien** aux droits différents.

### Lot 3 — Incident, base de connaissances et tableau de bord (≈ 4 h)
- La **prise en charge complète d'un incident** : ouverture, qualification, résolution, clôture.
- Une **fiche d'incident** (modèle ci-dessous).
- Une **petite base de connaissances** (au moins trois articles de solutions).
- Un **tableau de bord** : nombre de tickets ouverts, délais, répartition par catégorie.
- Un **exercice d'incident** conduit par le formateur ([[conventions-gsb]] §5).

### Modèle de fiche d'incident
```markdown
**Date et heure :**        **Demandeur :**
**Équipement concerné :**
**Objet :**
**Niveau (urgence / impact) :**
**Technicien :**
**Cause :**
**Solution appliquée :**
**Durée de résolution :**
**Mesure préventive :**
```

---

## 3. ⚙️ Contraintes

- **Aucune donnée réelle** de visiteur : utilise des comptes et des machines fictifs.
- **L'outil est accessible par un nom** et en **HTTPS**.
- **Chaque ticket est traçable** de l'ouverture à la clôture.
- **Outils :** libres (GLPI avec son agent d'inventaire, ou un équivalent, comme Znuny ou iTop).

---

## 3 bis. 🧰 Ton laboratoire et cette mission

*Tu pars de ce qui existe. **GLPI est justement prévu dans ton laboratoire : cette mission en est le cœur.** Remplis la table de correspondance de [[conventions-gsb]] §2 dans ton DAT.*

| Élément de la mission | Souvent déjà en place chez toi | Ce que tu construis |
|---|---|---|
| **Outil de tickets et de parc** | **GLPI prévu** | Son **choix justifié** (comparé à un autre outil), son installation et sa **sécurisation** |
| **Annuaire** | Active Directory | L'**authentification des utilisateurs et des techniciens** par l'annuaire |
| **Machines à inventorier** | Tes serveurs | L'**inventaire automatique** d'au moins trois machines |
| **Messagerie** | — | Les **notifications** de chaque étape d'un ticket |
| **Processus** | — | Les **catégories, priorités, délais**, la **fiche d'incident**, la **base de connaissances** et le **tableau de bord** |

**Ta réalisation :** la **cellule d'assistance qui fonctionne**. ⚠️ **Installer GLPI ne suffit pas** : la mission se joue sur le **processus** (un ticket suivi de bout en bout) et sur ses **indicateurs**.

---

## 4. ✅ Résultats attendus (tes tests de recette)

1. Je dois pouvoir **ouvrir un ticket** en tant qu'utilisateur et **le traiter** en tant que technicien.
2. Je dois pouvoir **montrer l'inventaire** d'au moins trois machines remonté **automatiquement**.
3. Je dois pouvoir **montrer une notification** reçue à chaque étape d'un ticket.
4. Je dois pouvoir **prouver** qu'un utilisateur ne voit **que ses propres tickets**.
5. Je dois pouvoir **présenter un tableau de bord** avec trois indicateurs et **expliquer** ce qu'ils signifient.
6. Je dois pouvoir **rédiger la fiche d'un incident réel** que j'ai traité.

---

## 5. 📤 Ce que tu fournis

Les livrables communs ([[conventions-gsb]] §4), plus :
- le **dossier de choix** (deux outils comparés) ;
- le **guide d'utilisation** pour un visiteur et pour un technicien ;
- la **fiche d'incident** remplie et la **base de connaissances** ;
- les **captures** du tableau de bord.

---

## 6. 🎓 Ce que cette mission te permet de montrer

| Famille | Sous-compétences (n° → [[conventions-gsb]] §7) |
|---|---|
| **Concevoir** | 1, 3 et 6 en partie |
| **Installer, tester, déployer** | 7, 10 ; 9, 11 et 12 en partie |
| **Exploiter, dépanner, superviser** | **15** (tableau de bord), **16** (incident) ; 17 en partie |

*Mission **forte sur l'exploitation et les incidents**, plus légère en conception. **Associe-la à une mission de conception** (par exemple [[N2-segmentation-filtrage]] ou [[E1-architecture-technique]]).*

---

## 7. ⚠️ Pièges à éviter

- **Un outil installé mais sans processus** : un ticket qui reste sans suite ne prouve rien.
- **Un tableau de bord décoratif** : chaque indicateur doit répondre à une question de GSB.
- **Des données personnelles non protégées** dans les tickets.
