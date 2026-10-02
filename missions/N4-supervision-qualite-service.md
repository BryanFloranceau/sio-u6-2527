---
titre: "Mission N4 — Supervision et qualité de service du système d'information"
tags: [eleves, u6, mission, gsb, N4, supervision, qos, sla]
mission: N4
duree: "≈ 20 h (socle 16 h + extension 4 h)"
public: étudiants
---

# 📈 Mission N4 — Supervision et qualité de service du système d'information

> Conventions : [[conventions-gsb]] · Contexte : [[fiche-gsb]] · Retour : [[00-lisez-moi]]

## 🪪 Fiche d'identité de la mission

| | |
|---|---|
| **Intitulé** | Superviser le système d'information de GSB et garantir un niveau de service |
| **Présentation rapide** | **Définir un contrat de service**, **superviser** serveurs et services avec **alertes**, **gérer un incident**, puis **maîtriser le trafic** pour protéger la qualité de service |
| **Durée** | **Socle** (lots 1, 2 et 3) ≈ 16 h · **Extension** (lot 4) ≈ 4 h |
| **Modalités de réception** | Recette sur ton laboratoire + dossier technique + présentation orale |
| **Équipe** | Individuel ou binôme (précise ta part personnelle) |

---

## 1. 🎯 Le besoin de GSB

Les serveurs du siège rendent des services **à toute l'entreprise** (annuaire, DHCP / DNS, messagerie, intranet, bases de données, application de suivi des visites). Les **visiteurs répartis sur le territoire** ont besoin d'un **service continu**. Aujourd'hui, c'est l'équipe Réseau et Système qui **apprend les pannes par les utilisateurs**.

La DSI veut **voir avant les utilisateurs** : mesurer la disponibilité, être **alertée** quand un seuil est dépassé, **réagir** selon la gravité et **protéger** les services essentiels lorsque le réseau est chargé (par exemple par les visiteurs connectés en Wi-Fi).

**Questions de ton analyse :** quel **niveau de service** promettre aux utilisateurs ? Quels **indicateurs** le mesurent vraiment ? Qui est **alerté**, à quel moment, par quel canal ? Que **perd-on** quand le service est dégradé ?

---

## 2. 🧱 Ce qu'il faut mettre en place

### Lot 1 — Contrat de service et indicateurs (socle, ≈ 4 h)
- Un **contrat de service** simple : disponibilité visée, temps de réponse acceptable, délai de reprise.
- Le **choix des indicateurs** et de leurs **seuils** (alerte, critique) pour chaque service.
- Un **dossier de choix** de l'outil de supervision (**au moins deux** outils comparés).

### Lot 2 — Installation de la supervision (socle, ≈ 8 h)
- Un **outil de supervision** (Zabbix, ou Prometheus avec Grafana, par exemple).
- La supervision d'**au moins six éléments** : le pare-feu, deux serveurs Linux, un serveur Windows, et **trois services** (web, DNS, base de données).
- Un **tableau de bord** lisible pour un non-technicien.
- Le **déploiement des agents par un script** (ou un outil de configuration), pas à la main.

### Lot 3 — Alertes et gestion d'incident (socle, ≈ 4 h)
- Des **alertes** envoyées par messagerie, avec **plusieurs niveaux** de gravité.
- Une **procédure d'escalade** : qui est prévenu, quand, qui décide.
- La **vérification du mode dégradé** : que se passe-t-il quand un service tombe ?
- Un **exercice d'incident** conduit par le formateur ([[conventions-gsb]] §5).

### Lot 4 — Qualité de service et amélioration (extension, ≈ 4 h)
- Une **limitation de débit** du VLAN « Visiteurs » et une **priorité** pour le trafic de l'application de suivi (mise en forme du trafic sur le pare-feu).
- Des **mesures avant et après** (par exemple avec `iperf3`) pour **prouver l'effet**.
- Un **rapport d'amélioration** : trois recommandations chiffrées pour garder le niveau de service.

---

## 3. ⚙️ Contraintes

- **Chaque indicateur est justifié** par un besoin du contrat de service (pas de tableau de bord décoratif).
- **Pas de fausse alerte permanente** : tes seuils doivent être réglés pour que les alertes **signifient quelque chose**.
- **Aucun secret** (jeton, mot de passe de messagerie) dans le dépôt.
- **Outils :** libres (Zabbix, Prometheus, Grafana, `iperf3`, pare-feu avec limitation de débit).

---

## 3 bis. 🧰 Ton laboratoire et cette mission

*Tu pars de ce qui existe. **Cette mission est celle qui apporte le plus à ton laboratoire** : la supervision avec alertes n'y figure pas encore. Remplis la table de correspondance de [[conventions-gsb]] §2 dans ton DAT.*

| Élément de la mission | Souvent déjà en place chez toi | Ce que tu construis |
|---|---|---|
| **Machines à superviser** | Pare-feu, annuaire, serveurs web, base en grappe, bastion | **Au moins six éléments réels** de ton laboratoire, dont trois services |
| **Supervision** | Rien en général | **Tout** : contrat de service, indicateurs, outil, tableau de bord, alertes |
| **Détection d'intrusion (Wazuh)** | En cours | **Complémentaire, pas équivalent** : Wazuh surveille la **sécurité** ; la supervision surveille la **disponibilité et la performance**. Explique la différence dans ton dossier |
| **Gestion des incidents (GLPI)** | À venir | *(option)* Une alerte qui **ouvre un ticket** automatiquement |
| **Pare-feu** | pfSense | La **limitation de débit** et la **priorité** du trafic (lot 4) |

**Ta réalisation :** le **contrat de service**, la **supervision avec alertes**, la **gestion d'un incident** et, en extension, la **qualité de service** mesurée avant et après.

---

## 4. ✅ Résultats attendus (tes tests de recette)

1. Je dois pouvoir **présenter le contrat de service** et dire quel **indicateur** mesure chaque engagement.
2. Je dois pouvoir **montrer le tableau de bord** avec les six éléments supervisés.
3. Je dois pouvoir **arrêter un service** et **montrer l'alerte** reçue, avec son niveau de gravité.
4. Je dois pouvoir **déployer l'agent de supervision sur une nouvelle machine** avec un script.
5. Je dois pouvoir **expliquer le mode dégradé** : ce qui continue de marcher, ce qui s'arrête, comment le rétablir.
6. Je dois pouvoir **rédiger un rapport d'incident** à partir des journaux et du tableau de bord.
7. *(extension)* Je dois pouvoir **montrer, chiffres à l'appui**, que la limitation de débit protège l'application lorsque le VLAN « Visiteurs » sature la liaison.

---

## 5. 📤 Ce que tu fournis

Les livrables communs ([[conventions-gsb]] §4), plus :
- le **contrat de service** et le **tableau des indicateurs** (seuils, justification) ;
- la **procédure d'escalade** ;
- le **script de déploiement** des agents ;
- les **captures** du tableau de bord et des alertes ;
- *(extension)* le **rapport d'amélioration** avec les mesures avant et après.

---

## 6. 🎓 Ce que cette mission te permet de montrer

| Famille | Sous-compétences (n° → [[conventions-gsb]] §7) |
|---|---|
| **Concevoir** | 3 (choix d'outil), **4** (disponibilité), 6 (tests) |
| **Installer, tester, déployer** | 7, **9** (qualité de service), 10 |
| **Exploiter, dépanner, superviser** | **14** (déploiement par script), **15** (indicateurs), **16** (incident), **17** (maintien et amélioration) |

---

## 7. ⚠️ Pièges à éviter

- **Superviser « tout »** sans objectif : une supervision qui sonne tout le temps finit par être ignorée.
- **Des seuils jamais testés** : provoque réellement la panne pour voir l'alerte arriver.
- **Confondre « le serveur répond au ping » et « le service rend le service »** : supervise le **service**, pas seulement la machine.
- **Une limitation de débit sans mesure** : sans « avant / après », tu ne prouves rien.
