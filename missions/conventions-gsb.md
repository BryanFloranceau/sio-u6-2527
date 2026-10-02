---
titre: "Conventions communes aux missions GSB"
tags: [eleves, u6, missions, gsb, conventions]
public: étudiants
---

# 📐 Conventions communes aux missions GSB

> À lire **une fois**, avant ta première mission. Toutes les missions ([[E1-architecture-technique]] · [[E2-assistance-helpdesk]] · [[E3-backoffice]] · [[N1-acces-distant-securise]] · [[N2-segmentation-filtrage]] · [[N3-haute-disponibilite]] · [[N4-supervision-qualite-service]]) partagent ces règles.
> Contexte : [[fiche-gsb]] · Retour : [[README]]

---

## 1. 🏷️ Valeurs communes

| Élément | Valeur retenue |
|---|---|
| **Entreprise** | GSB (Galaxy Swiss Bourdin), siège administratif Europe à Paris |
| **Domaine** | **Ton domaine existant : ne le renomme pas.** Le nom de référence de GSB (`gsbeu.intra`) ne sert que si tu installes un environnement neuf |
| **Plan d'adressage** | **Le tien.** Aucun plan n'est imposé : tu relies **tes zones** à celles de GSB (§2) |
| **Visiteurs à équiper** | **480** en métropole (les 60 d'outre-mer sont hors périmètre) |
| **Application de référence** | Application de suivi des visites et des frais (`visite.gsb.coop`) : le **code fourni par le formateur sert de charge de travail** ; aucun développement n'est demandé |

---

## 2. 🌐 Ton réseau et celui de GSB : la table de correspondance

**Chacun a son propre laboratoire et son plan d'adressage.** Tu **ne le modifies pas** pour coller à GSB. À la place, tu remplis, dans le **DAT de ta mission**, une table qui relie **les zones de GSB** à **tes réseaux**.

| Zone de GSB | Rôle | Origine dans GSB | **Ton équivalent** (VLAN, réseau) |
|---|---|---|---|
| **Administration** | Postes des techniciens (réseau et système) | VLAN 10 · 192.168.10.0/24 | |
| **Utilisateurs** | Postes des services (commercial, etc.) | VLAN 60 · 192.168.60.0/24 | |
| **Visiteurs** | Invités et visiteurs, accès Internet seul | VLAN 150 · 192.168.150.0/24 | |
| **Serveurs** | Annuaire, bases de données, applications | VLAN 300 · 172.16.0.0/17 | |
| **Sortie** | Liaison vers le pare-feu et Internet | VLAN 400 · 172.18.0.0/30 | |
| **DMZ** *(ajout)* | Services joignables depuis Internet | absente du document d'origine | |
| **Site distant** *(ajout)* | Deuxième site (réplication, VPN site-à-site) | absent du document d'origine | |
| **Accès des visiteurs en déplacement** *(ajout)* | Clients VPN | absent du document d'origine | |

**Règles réseau d'origine de GSB** (à transposer sur tes zones) :
- chaque zone (sauf « Visiteurs ») accède uniquement aux zones **Serveurs** et **Sortie** ;
- la zone **Visiteurs** peut interroger le **DNS** et le **DHCP** et sortir sur Internet.

**Serveurs de référence de GSB et leur équivalent chez toi :**

| GSB | Rôle | **Ton équivalent** |
|---|---|---|
| REZOLAB | DHCP et DNS | |
| LABANNU | Annuaire et contrôleur de domaine | *(ton Active Directory)* |
| MESSAGLAB | Messagerie | |
| INTRALAB | Intranet | |
| ProxSILAB | Proxy et pare-feu | *(ton pfSense)* |
| MUTLAB | Routage entre zones, filtrage | *(ton pfSense ou ton commutateur)* |
| RTROUT | Routeur et NAT | |

---

## 3. 🧱 Ton laboratoire : environnement, réalisation, évolution

**Tu as déjà construit un laboratoire.** C'est l'**environnement** exigé par l'annexe II.E. Il ne remplace pas ta réalisation : voici la différence.

| Niveau | Ce que c'est | Où ça se trouve dans ton dossier |
|---|---|---|
| **Environnement** | L'infrastructure qui supporte tout : hyperviseur, pare-feu, zones, annuaire, bases de données, accès d'administration… | Ton **DAT d'environnement** (annexe) et le tableau [[mon-laboratoire]] |
| **Réalisation** | Une solution qui répond à **un besoin de GSB**, avec ses choix justifiés, ses tests, son incident et son exploitation | Ta **mission** : DAT propre, plan de tests, rapports, fiche descriptive |
| **Évolution** (phase 2 de l'épreuve) | Ce que la commission te demande de **modifier en 1 heure** sur ta réalisation | Ce que ta réalisation te permet de faire évoluer |

👉 **Une mission est une évolution de ton laboratoire existant**, pas une reconstruction. Chaque lettre de mission contient une section **« Ton laboratoire et cette mission »** qui t'indique ce qui existe souvent déjà et ce qui reste à construire.

| Élément | Généralement déjà en place | À vérifier avec [[mon-laboratoire]] |
|---|---|---|
| **Hyperviseur** | Proxmox VE | Sauvegarde, accès sécurisé |
| **Pare-feu et zones** | pfSense, réseaux en VLAN | Règles justifiées, journaux |
| **Annuaire** | Active Directory, administré par PowerShell | Habilitations, GPO |
| **Services** | Serveurs web, base en grappe | Répartition de charge, bascules testées |
| **Administration** | Bastion avec Guacamole | Accès par clé, journal des connexions |
| **Sécurité** | Détection d'intrusion (Wazuh) en cours | Alertes, scénario d'attaque |
| **Support** | Gestion des incidents (GLPI) à venir | Tickets, inventaire |
| **Packet Tracer** | — | Pour **comprendre**, jamais pour **réaliser** |

---

## 4. 📦 Fonctionnement d'une mission

- Une mission est découpée en **lots**.
- Le **socle** (obligatoire) fait ≈ 14 à 16 h. Les **extensions** (au choix) ajoutent ≈ 4 à 6 h chacune.
- **Réalisation 1** : le socle **plus** une extension. **Réalisation 2** : le socle, ou le socle réduit. Le formateur valide ton choix.
- Chaque lot a ses **résultats attendus**, écrits sous la forme « je dois pouvoir… » : ce sont aussi **tes tests de recette**.
- **Tu pars de ton laboratoire existant** : ce qui est déjà en place compte comme point de départ, pas comme livrable. **Ce que tu ajoutes ou fais évoluer** est ta réalisation.

### Ce que tu rends pour chaque mission
1. Le **DAT de la mission** (schéma cible, besoin de GSB, choix justifiés, plan de tests, **table de correspondance**)
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
