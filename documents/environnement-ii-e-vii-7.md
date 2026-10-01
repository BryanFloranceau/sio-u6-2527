---
titre: "Environnement technologique (annexe II.E) — outil d'appréciation VII-7 : 26 lignes à justifier pour le laboratoire"
tags: [projet-u6, annexe-ii-e, annexe-vii-7, environnement, penalite, checklist, laboratoire, sisr]
statut: "📝 Trame prête — colonne « implantation » à renseigner avec le laboratoire réel"
source: "Annexe VII-7 d'un dossier de la session 2026 (AFTEC Caen) · annexe II.E de l'arrêté du 8 juillet 2024"
date_creation: 2026-10-01
---

# 🧱 L'outil d'appréciation de l'environnement technologique (annexe VII-7)

> **Pourquoi ce document compte :** la grille nationale prévoit une **pénalité jusqu'à 15 points** si l'environnement technologique mis en œuvre n'est pas conforme à l'annexe II.E, et renvoie à un « outil d'aide à l'appréciation de l'environnement technologique (**annexe 8**) ». Le dossier reçu contient exactement un tel outil, **intitulé de façon identique** (« Outil d'aide à l'appréciation de l'environnement technologique mobilisé par la personne candidate »), numéroté **VII-7**. L'identité entre « annexe 8 » et « VII-7 » est **très probable** ; à confirmer sur la circulaire de la session 2027.
> Liens : [[grille-evaluation-e6]] §2 · [[modeles-dossier-e6]] · [[croisement-referentiel]] §5 · [[progression-68h]]

---

## 1. 🔍 Nature du document

| Élément | Contenu |
|---|---|
| **Intitulé** | Outil d'aide à l'appréciation de l'environnement technologique mobilisé par la personne candidate — Épreuve E6 (option SISR) |
| **Référence** | Annexe II.E « Environnement technologique pour la certification » du référentiel |
| **Identification** | Centre d'examen (nom et adresse) ou candidat individuel (numéro, nom, prénom) |
| **Structure** | Tableau à **trois colonnes** : **Éléments** · **Description de l'implantation dans le centre d'examen** (nom du service ou de l'outil, caractéristiques techniques) · **Remarques de la commission d'interrogation** |
| **Sections** | 1.1 environnement commun (8 lignes) · 1.2 outils de sécurité (4 lignes) · 2.1 spécifique SISR (10 lignes) · 2.2 solution d'infrastructure opérationnelle (4 lignes, **au moins une**) |
| **Rappels imprimés** | Les logiciels de simulation ou d'émulation ne peuvent **pas** se substituer complètement à des équipements réels · **« Une solution d'infrastructure réduite à une simulation par un logiciel ne peut être acceptée »** |
| **Qui remplit quoi** | L'**établissement** décrit l'implantation ; la **commission** annote la dernière colonne lors de l'interrogation |

> Dans l'exemple reçu, le tableau décrit **l'infrastructure du centre** (annuaire, hyperviseur, pare-feu, supervision, haute disponibilité…), pas seulement la réalisation du candidat. C'est donc **le laboratoire de l'établissement** qui doit pouvoir justifier chaque ligne.

---

## 2. ✅ Les 26 lignes, avec pistes tirées du cursus

*Colonnes « exemple 2026 » = ce qu'a déclaré l'établissement de l'exemple (AFTEC Caen) ; colonnes « pistes » = suggestions fondées sur ton cursus (vault) et à **valider sur le laboratoire réel**. Préférence **open source** appliquée aux pistes proposées.*

### 1.1 — Environnement commun (8 lignes, obligatoires)

| # | Élément exigé | Exemple déclaré en 2026 | Pistes (cursus) | Preuve à prévoir |
|---|---|---|---|---|
| 1 | Service d'authentification | Active Directory, LDAP | [[31-windows-active-directory]] | Capture de la console, schéma du domaine |
| 2 | SGBD | MariaDB et MySQL | [[52-bases-de-donnees]] | Capture d'une base opérationnelle |
| 3 | Accès sécurisé à internet | pfSense du centre, NAT, pare-feu, pfSense personnel | [[47-pfsense]] | Règles de pare-feu, schéma |
| 4 | Environnement de travail collaboratif | GitHub, VS Code, Notion, Discord, OneDrive, serveur de fichiers SMB | Nextcloud, Mattermost ou Plane (projet U5) ; dépôt Git auto-hébergé | Capture d'un espace de travail |
| 5 | Deux serveurs sur des OS différents, dont un open source | Proxmox VE, Debian/Ubuntu, Windows Server, Windows 11 | [[20-linux-utilisateurs]] · [[30-windows-intro]] | Liste des VM avec leur OS |
| 6 | Solution de sauvegarde | Sauvegardes intégrées à Proxmox | [[63-sauvegarde]] (BorgBackup, Proxmox Backup Server) | Capture d'une restauration réussie |
| 7 | Ressources à accès sécurisé et habilitation | Proxmox, VPN, Active Directory | [[45-vpn-wireguard]] · [[46-pki-adcs]] | Matrice des habilitations |
| 8 | Deux types de terminaux dont un mobile | Un téléphone et une tablette | Client VPN ou accès à un service depuis un smartphone ou une tablette | Capture d'écran du terminal mobile |

### 1.2 — Outils de gestion de la sécurité (4 lignes, obligatoires)

| # | Élément exigé | Exemple déclaré en 2026 | Pistes (cursus) | Preuve à prévoir |
|---|---|---|---|---|
| 9 | Gestion des incidents | GLPI (première année) | [[51-glpi-support]] | Ticket d'incident traité |
| 10 | Détection et prévention d'intrusions | Wazuh | [[76-analyse-incidents]] (Wazuh, Suricata) | Alerte déclenchée sur le laboratoire |
| 11 | Chiffrement | Autorité de certification et GPO de demande de certificat automatique | [[46-pki-adcs]] · HTTPS sur les services | Certificat émis et déployé |
| 12 | Analyse de trafic | Wireshark | Cours de réseau et d'analyse de trames *(à localiser dans le cursus)* | Capture réseau commentée |

### 2.1 — Spécifique SISR (10 lignes, obligatoires)

| # | Élément exigé | Exemple déclaré en 2026 | Pistes (cursus) | Preuve à prévoir |
|---|---|---|---|---|
| 13 | Réseau à **plusieurs périmètres de sécurité** | VLAN utilisateurs et serveurs, filtrage par routeurs | [[43-vlans-switching]] · [[47-pfsense]] | Schéma des zones et matrice de flux |
| 14 | Service rendu avec **contrat de service** (sécurité, haute disponibilité) | Postes Windows dans le domaine, accès au serveur de fichiers, GPO | [[65-qualite-service]] · [[64-haute-disponibilite]] | Document de SLA, tests de service |
| 15 | **Analyse de trames** | Wireshark | Wireshark / tcpdump | Capture annotée |
| 16 | **Gestion des configurations** | Contrôleur de domaine (GPO) | Git, Ansible : [[00b-git-avance]] · [[23-linux-automatisation]] | Dépôt de configurations versionné |
| 17 | **Administration à distance sécurisée** | RDP, SSH, bastion (Guacamole) | [[48-bastion-guacamole]] | Journal de connexion via le bastion |
| 18 | **Supervision** (qualité, sécurité, disponibilité) **avec remontée d'alertes** | Zabbix | [[62-supervision-grafana]] (Prometheus, Alertmanager, Grafana) ou Zabbix | Tableau de bord + alerte reçue |
| 19 | **Accès sécurisés** à un service (intranet ou extranet) | Services internes filtrés, accès garanti par redondance de routeurs | Reverse proxy HTTPS, VPN ([[45-vpn-wireguard]]) | Règles de filtrage, test d'accès |
| 20 | Solution garantissant la **continuité** d'un service | Cluster Galera, HAProxy, Docker Swarm | [[52b-galera-cluster]] · [[64-haute-disponibilite]] | Bascule testée |
| 21 | Solution de **tolérance de panne** | Redondance des équipements réseau par HSRP | [[64-haute-disponibilite]] · CARP ou VRRP avec pfSense / keepalived | Panne simulée, service maintenu |
| 22 | **Répartition de charge** | HAProxy | HAProxy *(à placer dans le cursus HA)* | Statistiques de répartition |

### 2.2 — Au moins **une** solution d'infrastructure opérationnelle (4 lignes)

| # | Élément | Exemple déclaré en 2026 | Pistes (cursus) | Preuve à prévoir |
|---|---|---|---|---|
| 23 | Connexion sécurisée entre **deux sites** distants | pfSense, VPN IKEv2 IPsec site-à-site | [[45-vpn-wireguard]] · [[47-pfsense]] | Tunnel monté, flux testés |
| 24 | **Déploiement** de solutions techniques d'accès | Contrôleur de domaine | [[32-windows-utilisateurs-gpo]] | Déploiement d'un poste |
| 25 | Solution gérée par **procédures automatisées en langage de scripting** | Terraform, Ansible | [[23-linux-automatisation]] · [[34-windows-powershell]] · [[61b-cicd]] | Scripts versionnés, exécution |
| 26 | **Détection d'intrusions** ou de comportements anormaux | Wazuh | [[76-analyse-incidents]] | Détection d'un scénario d'attaque |

**Total : 22 lignes obligatoires (1 à 22) + 1 parmi 4 (23 à 26).**

---

## 3. 🧭 Comment l'utiliser dans la progression

| Séance | Action | Livrable |
|---|---|---|
| **S3** | Audit du laboratoire par rapport aux 26 lignes : colonne « implantation » v1, repérage des **manques** | Checklist II.E v1 |
| **S10** | Mise à jour après R1 ; **R2 choisie aussi pour combler les lignes encore vides** | Checklist v2 |
| **S14** | Vérification finale, **preuves jointes** (captures, schémas) | Checklist v3, tableau VII-7 complété par l'établissement |
| **S16-S17** | Contrôle sur le **poste d'examen** : tout ce qui est déclaré fonctionne | Fiche de contrôle du poste |

> **Règle de prudence :** une ligne « déclarée mais non démontrable » est plus dangereuse qu'une ligne vide, car la commission peut vérifier l'implantation et appliquer la **pénalité d'environnement non conforme** (jusqu'à 15 points).

---

## 4. 📋 Tableau de suivi à compléter (laboratoire de la promotion)

| # | Élément | Outil retenu | État (✅ 🟠 🔴) | Preuve | Séance de contrôle |
|---|---|---|---|---|---|
| 1 | Service d'authentification | | | | S3 |
| 2 | SGBD | | | | S3 |
| 3 | Accès sécurisé à internet | | | | S3 |
| 4 | Environnement collaboratif | | | | S3 |
| 5 | Deux serveurs, OS différents | | | | S3 |
| 6 | Sauvegarde | | | | S3 |
| 7 | Accès sécurisé et habilitation | | | | S3 |
| 8 | Deux types de terminaux (un mobile) | | | | S3 |
| 9 | Gestion des incidents | | | | S3 |
| 10 | Détection / prévention d'intrusions | | | | S10 |
| 11 | Chiffrement | | | | S3 |
| 12 | Analyse de trafic | | | | S3 |
| 13 | Plusieurs périmètres de sécurité | | | | S3 |
| 14 | Service avec contrat de service | | | | S10 |
| 15 | Analyse de trames | | | | S3 |
| 16 | Gestion des configurations | | | | S10 |
| 17 | Administration à distance sécurisée | | | | S3 |
| 18 | Supervision avec alertes | | | | S10 |
| 19 | Accès sécurisés à un service | | | | S10 |
| 20 | Continuité d'un service | | | | S10 |
| 21 | Tolérance de panne | | | | S10 |
| 22 | Répartition de charge | | | | S10 |
| 23-26 | Au moins une solution (VPN site-à-site, déploiement, scripting, détection) | | | | S10 |

---

## 5. ❓ Points à confirmer

- [ ] **Annexe 8 = VII-7 ?** à vérifier sur la circulaire de la session 2027
- [ ] **Qui remplit** le tableau pour l'établissement (responsable de formation, formateur E6) et à quelle date
- [ ] **Quels éléments** sont fournis par l'établissement et lesquels doivent être apportés par l'étudiant (le référentiel précise que le candidat est seul responsable de ses outils s'il passe hors du centre)
- [ ] **Lignes 12, 15 et 22** (analyse de trafic, analyse de trames, répartition de charge) : où les couvre le cursus actuel ?
- [ ] **Terminal mobile (ligne 8)** : disposer d'un smartphone et d'une tablette de laboratoire ou d'un usage autorisé de terminaux personnels
