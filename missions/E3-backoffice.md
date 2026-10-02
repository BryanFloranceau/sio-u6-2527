---
titre: "Mission E3 — BackOffice : fiabiliser l'environnement en production"
tags: [eleves, u6, mission, gsb, E3, backoffice, sauvegarde, annuaire, scripts]
mission: E3
duree: "≈ 16 h (lots à choisir)"
origine: "Inspirée d'une fiche du réseau CERTA (2012), réécrite et actualisée"
public: étudiants
---

# 🗄️ Mission E3 — BackOffice : fiabiliser l'environnement en production

> Conventions : [[conventions-gsb]] · Contexte : [[fiche-gsb]] · Retour : [[README]]

## 🪪 Fiche d'identité de la mission

| | |
|---|---|
| **Intitulé** | Fiabilisation de l'environnement mis en production pour l'application de suivi des visites et le matériel des visiteurs |
| **Présentation rapide** | **Comparer, choisir et mettre en œuvre** des outils d'inventaire, de gestion d'incidents, de **sauvegarde**, de **pré-production par scripts** et d'**annuaire**, puis les valider par une **recette** |
| **Durée** | ≈ **16 h** : tu choisis **3 lots** parmi 6 (voir §2) |
| **Origine** | Mission du réseau CERTA (2012) en 6 lots, **réécrite** avec des outils actuels |
| **Modalités de réception** | Recette sur ton laboratoire + dossier technique + présentation orale |
| **Équipe** | Individuel ou binôme (**précise tes lots**) |

---

## 1. 🎯 Le besoin de GSB

L'application de suivi des visites et le **matériel déployé auprès des visiteurs** sont mis en production. GSB demande de **fiabiliser** l'environnement : savoir **ce qu'on a** (inventaire), **traiter les incidents**, pouvoir **remonter le système** après un sinistre, **tester les changements** avant la production et **gérer les comptes** des visiteurs.

Le cadrage est volontairement **léger** : tu dois **comparer** des solutions, **choisir** et **justifier**, puis **mettre en œuvre** et **prouver** que ça répond au besoin.

**Questions de ton analyse :** que perd GSB si le système est indisponible ? Combien de temps peut-il l'être ? Quelles **données personnelles** contiennent les comptes et l'inventaire ?

---

## 2. 🧱 Les six lots

*Tu choisis **trois lots**, dont **le lot 6 (recette)** obligatoire. Le formateur valide ton choix.*

| Lot | Contenu | Durée | Ce que tu dois produire |
|---|---|---|---|
| **1 — Inventaire et gestion de parc** | Comparer **trois outils**, installer celui que tu retiens, remonter l'inventaire de plusieurs machines | ≈ 5 h | Tableau de comparaison, note de conseil, mode opératoire |
| **2 — Gestion des incidents** | Comparer **deux outils**, installer et paramétrer la gestion des tickets | ≈ 4 h | Comparatif, mode opératoire, tickets de test |
| **3 — Sauvegarde et restauration** | Mettre en place une sauvegarde, **remonter le système en moins de trois heures**, mesurer simplicité, rapidité, automatisation et restauration | ≈ 6 h | Procédure, **temps de restauration mesuré**, alternative éventuelle |
| **4 — Plateforme de pré-production** | Un environnement **identique à la production**, alimenté par des **scripts** de copie des configurations, avec conservation des versions | ≈ 6 h | Scripts versionnés, procédure de reconstruction |
| **5 — Annuaire des visiteurs** | Un domaine, une **nomenclature** (secteur → région → visiteur), des unités d'organisation, la **création de comptes par script** | ≈ 5 h | Scripts, procédure, comptes de test |
| **6 — Intégration et recette** *(obligatoire)* | Des machines propres avec l'**adressage conforme**, un **plan de tests**, les résultats et la **documentation de déploiement** | ≈ 3 h | Plan de tests, rapport de tests, documentation |

### Combinaisons conseillées

| Objectif | Lots |
|---|---|
| **Continuité et automatisation** | 3 + 4 + 6 |
| **Exploitation et incidents** | 1 + 2 + 6 |
| **Gestion des accès** | 5 + 4 + 6 |

---

## 3. ⚙️ Contraintes

- **Chaque outil est justifié** par une comparaison (au moins deux ou trois candidats, selon le lot).
- **La sauvegarde est testée par une restauration réelle** : une sauvegarde jamais restaurée ne prouve rien.
- **Les scripts sont versionnés** dans ton dépôt Git, sans secret.
- **Aucune donnée réelle** : comptes et machines fictifs.
- **Outils :** libres (GLPI avec son agent d'inventaire, Znuny, BorgBackup ou Proxmox Backup Server, Samba AD ou OpenLDAP, Bash et Git).

---

## 3 bis. 🧰 Ton laboratoire et cette mission

*Tu pars de ce qui existe : **ton annuaire Active Directory est déjà administré en PowerShell**. Pour ne pas refaire ce que tu as, **les lots 3 et 4 sont ceux qui t'apportent du neuf**. Remplis la table de correspondance de [[conventions-gsb]] §2 dans ton DAT.*

| Lot | Souvent déjà en place chez toi | Ce que tu construis |
|---|---|---|
| **5 — Annuaire** | **AD administré en PowerShell** | Les **preuves** : nomenclature secteur → région → visiteur, **vingt comptes créés par script**, procédure. Lot rapide si c'est déjà fait |
| **3 — Sauvegarde** | **Absente en général** | La sauvegarde, la **restauration réelle** et le **délai mesuré** |
| **4 — Pré-production** | — | Les **scripts**, leur **versionnement** et la **reconstruction** |
| **1 — Inventaire** et **2 — Incidents** | GLPI à venir | Peuvent s'appuyer sur GLPI, **sans dupliquer** la mission [[E2-assistance-helpdesk]] |
| **6 — Recette** | — | Le **plan de tests** et le **rapport de recette** |

**Combinaison conseillée pour ton laboratoire :** les lots **3 + 4 + 6** (sauvegarde, pré-production, recette), qui complètent ce que tu as déjà.

---

## 4. ✅ Résultats attendus (tes tests de recette)

*Selon les lots choisis :*

1. *(lot 1)* Je dois pouvoir **montrer l'inventaire** de trois machines et **justifier** mon choix d'outil.
2. *(lot 2)* Je dois pouvoir **traiter un incident** de bout en bout et **le retrouver** dans l'outil.
3. *(lot 3)* Je dois pouvoir **détruire un serveur de test** et le **remonter en moins de trois heures**, en **mesurant** le délai.
4. *(lot 4)* Je dois pouvoir **reconstruire l'environnement de pré-production** à partir de mes scripts, et **revenir à une version précédente**.
5. *(lot 5)* Je dois pouvoir **créer vingt comptes de visiteurs** par un script, rangés dans la bonne nomenclature.
6. *(lot 6)* Je dois pouvoir **dérouler mon plan de tests** et **présenter les résultats** (réussi, échoué, corrigé).

---

## 5. 📤 Ce que tu fournis

Les livrables communs ([[conventions-gsb]] §4), plus :
- les **comparatifs** et la **note de conseil** de chaque lot ;
- les **modes opératoires** ;
- les **scripts** ;
- le **plan de tests** et le **rapport de recette** (lot 6).

---

## 6. 🎓 Ce que cette mission te permet de montrer

| Lot | Sous-compétences (n° → [[conventions-gsb]] §7) |
|---|---|
| **1** | 3, 6, 15 |
| **2** | 3, **16** |
| **3** | 4, **8**, 11, 17 |
| **4** | 5, 12, **14** |
| **5** | 1, 7, **14** |
| **6** | 6, 10, **11**, 12 |

*Avec **trois lots**, tu couvres un bon tiers des 17 sous-compétences. **Associe cette mission à une autre** qui complète ce que tes lots ne portent pas (par exemple [[N3-haute-disponibilite]] ou [[N4-supervision-qualite-service]]).*

---

## 7. ⚠️ Pièges à éviter

- **Une sauvegarde jamais testée** : prouve la restauration, avec le temps réel mesuré.
- **Une comparaison de façade** : les critères doivent venir du besoin de GSB.
- **Un script qui marche seulement chez toi** : rejoue-le sur une machine propre.
- **Trop de lots superficiels** : mieux vaut trois lots bien menés que six survolés.
