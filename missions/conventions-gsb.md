---
titre: "Conventions communes aux missions GSB"
tags: [eleves, u6, missions, gsb, conventions]
public: étudiants
---

# 📐 Conventions communes aux missions GSB

> À lire **une fois**, avant ta première mission. Toutes les missions ([[N1-acces-distant-securise]] · [[N2-segmentation-filtrage]] · [[N3-haute-disponibilite]] · [[N4-supervision-qualite-service]]) partagent ces règles.
> Contexte : [[fiche-gsb]] · Retour : [[README]]

---

## 1. 🏷️ Valeurs communes

| Élément | Valeur retenue pour le laboratoire |
|---|---|
| **Entreprise** | GSB (Galaxy Swiss Bourdin), siège administratif Europe à Paris |
| **Domaine interne** | `gsbeu.intra` |
| **Visiteurs à équiper** | **480** en métropole (les 60 d'outre-mer sont hors périmètre) |
| **Application de référence** | Application de suivi des visites et des frais (`visite.gsb.coop`) : le **code fourni par le formateur sert de charge de travail** ; aucun développement n'est demandé |

---

## 2. 🌐 Plan d'adressage du laboratoire

*Sous-ensemble du réseau de GSB. Les lignes marquées « ajout » n'existent pas dans le document d'origine : elles sont propres au laboratoire.*

| VLAN | Service | Adressage |
|---|---|---|
| 10 | Réseau et système | 192.168.10.0/24 |
| 60 | Commercial | 192.168.60.0/24 |
| 150 | Visiteurs | 192.168.150.0/24 |
| 300 | Serveurs | 172.16.0.0/17 (le laboratoire utilise 172.16.0.0/24) |
| 400 | Sortie | 172.18.0.0/30 |
| 350 | **DMZ** *(ajout)* | 172.20.0.0/24 |
| — | **Site distant** *(ajout)* | 172.22.0.0/24 |
| — | **VPN des visiteurs** *(ajout)* | 10.99.0.0/24 |

**Règles réseau d'origine :**
- chaque VLAN (sauf « Visiteurs ») accède uniquement aux VLAN **Serveurs** et **Sortie** ;
- le VLAN **Visiteurs** peut interroger le **DNS** et le **DHCP** et sortir sur Internet.

**Serveurs de référence :** REZOLAB (DHCP / DNS, 172.16.0.10) · LABANNU (annuaire, 172.16.0.30) · MESSAGLAB (messagerie, 172.16.0.20) · INTRALAB (intranet, 172.16.0.100) · ProxSILAB (proxy / pare-feu) · MUTLAB (commutateur de niveau 3) · RTROUT (routeur / NAT).

---

## 3. 🧱 Environnement de travail

| Élément | Choix |
|---|---|
| **Hyperviseur** | Proxmox VE |
| **Systèmes** | Debian, **au moins une machine Windows Server** (pour l'annuaire ou les postes) |
| **Pare-feu / routeur** | pfSense ou OPNsense |
| **Outils** | Libres, sauf contrainte justifiée dans ton dossier de choix |
| **Packet Tracer** | Pour **comprendre**, jamais pour **réaliser** : la réalisation tourne sur le laboratoire |

---

## 4. 📦 Fonctionnement d'une mission

- Une mission est découpée en **lots**.
- Le **socle** (obligatoire) fait ≈ 14 à 16 h. Les **extensions** (au choix) ajoutent ≈ 4 à 6 h chacune.
- **Réalisation 1** : le socle **plus** une extension. **Réalisation 2** : le socle, ou le socle réduit. Le formateur valide ton choix.
- Chaque lot a ses **résultats attendus**, écrits sous la forme « je dois pouvoir… » : ce sont aussi **tes tests de recette**.

### Ce que tu rends pour chaque mission
1. Le **DAT** (schéma cible, choix justifiés, plan de tests)
2. La **réalisation opérationnelle** sur ton laboratoire
3. Les **procédures** d'installation et d'exploitation (réutilisables par un tiers)
4. Le **rapport de tests** et le **rapport d'incident** (voir §5)
5. Les **scripts et configurations** dans ton dépôt Git
6. Ta **fiche descriptive** (avec ta **part personnelle** si tu travailles en équipe)

---

## 5. 🚨 L'exercice d'incident

Pendant une séance prévue (S7 pour la réalisation 1, S13 pour la réalisation 2), le formateur **provoque une panne** sur ta réalisation. Tu dois **identifier**, **qualifier**, **résoudre ou escalader**, puis écrire un **rapport d'incident** (symptôme → cause → correction → mesure préventive). Tu ne connais pas la panne à l'avance.

---

## 6. 🔐 Règles de sécurité de ton dossier

- **Aucun mot de passe en clair** dans ton dossier ni dans ton dépôt Git.
- Les secrets (clés, mots de passe) restent **hors du dépôt** ; tu les remets au formateur par un autre canal si besoin.
- Les données utilisées sont **fictives** : aucune donnée réelle de patient, de médecin ou de salarié.

---

## 7. 🔢 Les 17 compétences, en clair

| # | Ce que tu dois savoir faire |
|---|---|
| **Concevoir** | |
| 1 | Analyser un besoin et son cadre juridique |
| 2 | Étudier l'**impact** d'une évolution sur le système existant |
| 3 | **Justifier un choix** de solution (dossier de choix, spécifications) |
| 4 | Choisir ce qui assure la **qualité et la disponibilité** d'un service |
| 5 | **Maquetter** une solution |
| 6 | **Préparer les tests** de validation |
| **Installer, tester, déployer** | |
| 7 | **Installer et configurer** des éléments d'infrastructure |
| 8 | Assurer la **continuité** d'un service |
| 9 | Assurer la **qualité de service** |
| 10 | **Documenter** (technique et utilisateur) |
| 11 | **Tester** l'intégration et l'acceptation |
| 12 | **Déployer** une solution |
| **Exploiter, dépanner, superviser** | |
| 13 | **Administrer** sur place et à distance |
| 14 | **Automatiser** des tâches d'administration |
| 15 | Exploiter des **indicateurs et des journaux** |
| 16 | Gérer un **incident** |
| 17 | **Maintenir et améliorer** la qualité d'un service |
