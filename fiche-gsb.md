---
titre: "Fiche d'identité — GSB, laboratoire Galaxy Swiss Bourdin"
tags: [eleves, u6, contexte, gsb, seance-2]
public: étudiants
---

# 💊 GSB — Laboratoire Galaxy Swiss Bourdin

> **Fiche de lecture pour la séance 2.** Elle **résume** le contexte pédagogique GSB du réseau CERTA : le document officiel reste ta référence.
> Retour : [[README]] · Séance : [[S02]]

---

## 1. 🏭 Qui est GSB ?

| | |
|---|---|
| **Activité** | Laboratoire pharmaceutique, issu de la **fusion** (2009) de **Galaxy** (États-Unis, maladies virales) et de **Swiss Bourdin** (Europe, médicaments conventionnels) |
| **Sièges** | Siège social à Philadelphie ; siège administratif Europe à **Paris** (la France sert de « témoin » pour améliorer le suivi de l'activité de visite) |
| **Force commerciale** | **480 visiteurs médicaux** en métropole et **60** en outre-mer, répartis en secteurs géographiques, avec une hiérarchie secteur → région → visiteurs |
| **Situation** | Deux ans de réorganisations après la fusion ; l'entreprise veut **moderniser la visite médicale** |

**Point clé :** les visiteurs sont des **acteurs mobiles et autonomes**. Aujourd'hui leur matériel n'est **pas uniformisé** : une indemnité pour s'équiper (politique Swiss-Bourdin) ou une dotation (politique Galaxy).

---

## 2. 🖥️ Le système informatique du siège parisien

| Élément | Description |
|---|---|
| **Salle serveur** | 6ᵉ étage, accès très restreint (clé sécurisée, badge, gardien 24h/24) |
| **Services de base** | DHCP, DNS, annuaire, gestion centralisée des environnements |
| **Communication** | Intranet, messagerie, agenda partagé |
| **Applications métier** | Base d'information pharmaceutique, serveurs de recherche, base des produits, base des licences, **PGI** (RH, comptabilité, GRC) |
| **Équipement** | 350+ postes ; 45 serveurs physiques (en 2012) et plus de 100 serveurs virtuels |
| **Données** | **Stratégiques**, sans tolérance à la fuite ni à la destruction : **réplication quotidienne vers les États-Unis** par lien dédié |
| **Tolérance de panne** | RAID, alimentation redondante, lien réseau redondant, spanning-tree, clustering |

---

## 3. 🌐 Le réseau

| VLAN | Service | Adressage |
|---|---|---|
| 10 | Réseau et système | 192.168.10.0/24 |
| 20 | Direction / DSI | 192.168.20.0/24 |
| 30 | RH / Compta / Juridique / Secrétariat | 192.168.30.0/24 |
| 40 | Communication / Rédaction | 192.168.40.0/24 |
| 50 | Développement | 192.168.50.0/24 |
| 60 | Commercial | 192.168.60.0/24 |
| 70 | Labo-Recherche | 192.168.70.0/24 |
| 100 | Accueil | 192.168.100.0/24 |
| 150 | **Visiteurs** | 192.168.150.0/24 |
| 200 | Démonstration | 192.168.200.0/24 |
| 300 | **Serveurs** | 172.16.0.0/17 |
| 400 | **Sortie** | 172.18.0.0/30 |

**Règles actuelles :**
- chaque VLAN (sauf « Visiteurs ») ne peut accéder qu'aux VLAN **Serveurs** et **Sortie** ;
- le VLAN **Visiteurs** ne peut interroger que le **DNS** et le **DHCP** et sortir sur Internet.

**Organisation :** une baie de brassage par étage, reliée par **fibre** à la baie centrale ; un commutateur de niveau 3 (**MUTLAB**) fait le routage inter-VLAN avec des **ACL** ; un proxy / pare-feu (**ProxSILAB**) et un routeur / NAT (**RTROUT**) assurent la sortie.

---

## 4. 🗄️ Les serveurs principaux

| Serveur | Rôle |
|---|---|
| REZOLAB | DHCP / DNS |
| LABANNU | Annuaire et contrôleur de domaine |
| MESSAGLAB | Messagerie |
| INTRALAB | Intranet |
| JURILAB | Documents juridiques |
| NOTICELAB | Notices des produits |
| PGILAB | PGI : RH, comptabilité, GRC |
| BDMEDOCLAB | Base des produits GSB |
| BDPHARMA | Base pharmaceutique |
| BDMED | Données sur les médecins |

La messagerie et l'intranet sont limités au site parisien : des services **externalisés** permettent aux visiteurs d'y accéder.

---

## 5. 🎯 Ce que veut GSB

- **Mieux suivre l'activité de terrain** et uniformiser le suivi des visites ;
- **une gestion unique des frais** pour tous les visiteurs ;
- des **remontées d'information** plus régulières des visiteurs vers le siège ;
- un **accès plus direct aux données du personnel** pour les responsables de secteur.

**Qui fait quoi :** le service **développement** produit les applications (enregistrement des visites, frais) ; le service **réseau et système** fournit les équipements, la configuration réseau et les serveurs pour les héberger.

---

## 6. 🧰 Les missions SISR possibles

| Mission | En bref | Ce que tu y montres |
|---|---|---|
| **Équipement des visiteurs** | Définir un poste mobile, préparer des **procédures** de préparation et de récupération, proposer une charte d'usage. À l'origine : **étude uniquement** | Analyse et choix ; à **compléter par une mise en œuvre** (masteriser et déployer une image) |
| **Architecture technique** | Mettre en place l'**application web de suivi** : serveur web HTTPS, **base de données sur un autre serveur**, FTP authentifié en accès interne, **DMZ** et pare-feu | Installation, sécurisation, tests de recette, documentation |
| **Assistance (helpdesk)** | Installer un outil de **gestion de parc et de tickets** avec tableau de bord et mails de notification | Gestion d'un incident, indicateurs |
| **BackOffice** | **Six lots** : gestion de projet, inventaire, incidents, **sauvegarde (remise en service en moins de trois heures)**, plateforme de pré-test par **scripts**, annuaire, intégration et recette | Comparaisons, sauvegarde, automatisation, plan de tests. **Chaque élève choisit 2 ou 3 lots** |
| **Dépannage à distance** | Prise en main à distance des postes mobiles, règles de filtrage et de translation | Administration à distance sécurisée |

*Les projets de développement (frais, comptes rendus, service web) relèvent du développement (SLAM). Les énoncés détaillés te seront remis en séance. Les outils cités dans les documents d'origine datent de 2012 : on les remplace par des outils libres actuels.*

---

## 7. ❓ Six questions pour comprendre GSB

1. **Qui** sont les acteurs et les utilisateurs ?
2. **Que fait** l'organisation, et de quoi dépend son activité ?
3. **Quelles données** circulent, et lesquelles sont sensibles ?
4. **Quel cadre juridique** s'applique (données sur les médecins, données RH, transfert de données hors Union européenne) ?
5. **Quelle infrastructure existe** (VLAN, serveurs, redondances) ?
6. **Quels sont les points faibles** (visiteurs mobiles, accès extérieurs, supervision) ?

*Réponds avec tes mots dans ton journal de bord : ce travail alimente ta matrice de la séance 2.*
