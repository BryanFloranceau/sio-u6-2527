---
titre: "Mon laboratoire — la checklist de l'environnement (annexe II.E)"
tags: [eleves, u6, laboratoire, environnement, annexe-ii-e, checklist]
public: étudiants
---

# 🧱 Mon laboratoire — checklist de l'environnement

> **Pourquoi c'est important :** à l'épreuve, la commission vérifie que l'environnement de travail respecte l'**annexe II.E** du référentiel. Un environnement **non conforme** peut coûter **jusqu'à 15 points**. Une solution réduite à une **simulation** logicielle n'est pas acceptée.
> Retour : [[mon-parcours]] · Utilisée à partir de : [[S03]]

---

## 🧭 Comment l'utiliser

1. **Copie ce fichier** dans ton espace et remplis-le.
2. Pour chaque ligne, note **l'outil que tu utilises**, **qui le fournit** (l'école ou toi), et **la preuve** que tu peux montrer (capture, schéma, configuration).
3. **Ce n'est pas à toi seul de tout construire** : l'école fournit une partie de l'environnement. Ton rôle : **savoir ce qui existe, savoir le montrer et savoir expliquer ce que tu as construit toi-même**.
4. Repère ce qui **manque** et dis-le au formateur.

> ⚠️ **Une ligne que tu déclares mais que tu ne sais pas montrer est plus risquée qu'une ligne laissée vide.**

*Légende : ✅ présent et démontrable · 🟠 présent mais je ne sais pas encore le montrer · 🔴 absent*

---

## A. Les bases (8 lignes obligatoires)

| # | Ce que le laboratoire doit avoir | Idées d'outils | Mon outil | Fourni par | Preuve | État |
|---|---|---|---|---|---|---|
| 1 | Un **service d'authentification** (annuaire) | Active Directory | | | | |
| 2 | Une **base de données** | MariaDB, MySQL | | | | |
| 3 | Un **accès sécurisé à Internet** | Pare-feu / NAT (pfSense) | | | | |
| 4 | Un **outil de travail collaboratif** | Nextcloud, Git, Mattermost | | | | |
| 5 | **Deux serveurs** sous **deux systèmes différents**, dont un open source | Debian + Windows Server | | | | |
| 6 | Une **sauvegarde** | BorgBackup, Proxmox Backup Server | | | | |
| 7 | Des **ressources à accès restreint** (habilitations) | Droits Active Directory, VPN | | | | |
| 8 | **Deux types de terminaux** dont **un mobile** | Poste + smartphone ou tablette | | | | |

## B. Les outils de sécurité (4 lignes obligatoires)

| # | Ce que le laboratoire doit avoir | Idées d'outils | Mon outil | Fourni par | Preuve | État |
|---|---|---|---|---|---|---|
| 9 | La **gestion des incidents** | GLPI | | | | |
| 10 | La **détection / prévention d'intrusions** | Wazuh, Suricata | | | | |
| 11 | Le **chiffrement** | Certificats (autorité de certification), HTTPS, VPN | | | | |
| 12 | L'**analyse de trafic** | Wireshark | | | | |

## C. Spécifique à SISR (10 lignes obligatoires)

| # | Ce que le laboratoire doit avoir | Idées d'outils | Mon outil | Fourni par | Preuve | État |
|---|---|---|---|---|---|---|
| 13 | Un réseau avec **plusieurs zones de sécurité** | VLAN + pare-feu | | | | |
| 14 | Un **service rendu à l'utilisateur** avec un **contrat de service** (sécurité, disponibilité) | Un SLA écrit, des tests | | | | |
| 15 | Un logiciel d'**analyse de trames** | Wireshark, tcpdump | | | | |
| 16 | Une **gestion des configurations** | Git, Ansible, GPO | | | | |
| 17 | Une **administration à distance sécurisée** | SSH, bastion (Guacamole), RDP | | | | |
| 18 | Une **supervision** avec **alertes** | Prometheus + Grafana, Zabbix | | | | |
| 19 | Des **accès sécurisés** à un service (interne ou externe) | Reverse proxy HTTPS, VPN | | | | |
| 20 | Une solution de **continuité** d'un service | Cluster de base de données, HAProxy | | | | |
| 21 | Une **tolérance de panne** | CARP / VRRP, Proxmox HA | | | | |
| 22 | Une **répartition de charge** | HAProxy | | | | |

## D. Au moins **une** de ces quatre solutions

| # | Solution | Idées d'outils | Mon choix (oui/non) | Preuve | État |
|---|---|---|---|---|---|
| 23 | **Connexion sécurisée entre deux sites** | WireGuard, IPsec | | | |
| 24 | **Déploiement** de solutions techniques d'accès | GPO, déploiement automatisé | | | |
| 25 | Solution gérée par des **scripts** | Ansible, Bash, PowerShell | | | |
| 26 | **Détection d'intrusions** ou de comportements anormaux | Wazuh, Suricata | | | |

---

## 📌 Mon bilan à la séance 3

- **Nombre de lignes ✅ :** ___ / 22
- **Lignes 🟠 (à apprendre à montrer) :** ___
- **Lignes 🔴 (absentes) :** ___
- **La solution (23 à 26) que je vise :** ___

**Les 3 lignes les plus urgentes à traiter :**
1.
2.
3.

*Tu mettras cette checklist à jour à la séance 10, puis une dernière fois à la séance 14.*
