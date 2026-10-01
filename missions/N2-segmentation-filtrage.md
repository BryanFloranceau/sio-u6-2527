---
titre: "Mission N2 — Segmentation et filtrage du réseau du siège"
tags: [eleves, u6, mission, gsb, N2, vlan, pare-feu, ids]
mission: N2
duree: "≈ 20 h (socle 14 h + extension 6 h)"
public: étudiants
---

# 🧱 Mission N2 — Segmentation et filtrage du réseau du siège

> Conventions : [[conventions-gsb]] · Contexte : [[fiche-gsb]] · Retour : [[00-lisez-moi]]

## 🪪 Fiche d'identité de la mission

| | |
|---|---|
| **Intitulé** | Faire évoluer la segmentation et le filtrage du réseau du siège de GSB |
| **Présentation rapide** | **Étudier l'impact** de l'ouverture d'une **DMZ** sur les règles existantes, la mettre en place sur le laboratoire, puis la **protéger** par une détection d'intrusion |
| **Durée** | **Socle** (lots 1, 2 et 4) ≈ 14 h · **Extension** (lot 3) ≈ 6 h |
| **Modalités de réception** | Recette sur ton laboratoire + dossier technique + présentation orale |
| **Équipe** | Individuel ou binôme (précise ta part personnelle) |

---

## 1. 🎯 Le besoin de GSB

Le réseau du siège est segmenté en **VLAN** et sa règle de base est simple : **chaque VLAN, sauf « Visiteurs », n'accède qu'aux VLAN « Serveurs » et « Sortie »**. Le VLAN « Visiteurs » ne peut interroger que le DNS et le DHCP et sortir sur Internet. Un commutateur de niveau 3 (**MUTLAB**) fait le routage entre VLAN avec des **listes de contrôle d'accès** ; un pare-feu et un routeur assurent la sortie (**ProxSILAB**, **RTROUT**).

GSB doit héberger en interne l'**application de suivi des visites**, accessible par **Internet** depuis `visite.gsb.coop`. Il faut donc créer une **zone démilitarisée (DMZ, VLAN 350)**. Cette évolution **modifie les règles actuelles** : de nouveaux flux apparaissent (Internet → DMZ, DMZ → base de données) et la règle générale « tout VLAN → Serveurs » doit être revue.

**Questions de ton analyse :** quels **flux nouveaux** ? Quels flux existants sont **touchés** ? Quels **risques de régression** (un service qui ne répond plus) ? Quel cadre juridique pour des **données sur des praticiens** exposées par une application web ?

---

## 2. 🧱 Ce qu'il faut mettre en place

### Lot 1 — Étude d'impact et conception (socle, ≈ 4 h)
- La **matrice des flux** avant et après l'évolution (qui parle à qui, sur quel port).
- L'**analyse d'impact** : flux ajoutés, règles modifiées, risques, **plan de retour arrière**.
- Le **plan de tests d'acceptation** : flux **autorisés** et flux **interdits** à vérifier.

### Lot 2 — Mise en œuvre : VLAN, routage et filtrage (socle, ≈ 8 h)
- Un réseau virtuel avec les **VLAN 10, 60, 150, 300, 400 et 350** ([[conventions-gsb]] §2).
- Le **routage entre VLAN** et le **filtrage** conformes à la matrice de flux, sur un pare-feu (pfSense ou OPNsense).
- Un **DHCP** et un **DNS** pour chaque zone ; le **NAT** de sortie.
- Un **serveur web de test** en DMZ et une **base** dans le VLAN Serveurs, **seul le serveur web** pouvant l'interroger.

### Lot 4 — Recette et bascule (socle, ≈ 2 h)
- L'**exécution du plan de tests** avec résultats.
- Une **procédure de bascule** (mise en service) et de **retour arrière**.

### Lot 3 — Détection d'intrusion (extension, ≈ 6 h)
- Une **sonde de détection d'intrusion** (par exemple Suricata sur le pare-feu) sur le trafic de la DMZ et du VLAN Visiteurs.
- Un **scénario d'attaque** simple (balayage de ports depuis le VLAN Visiteurs) qui **déclenche une alerte**.
- L'**analyse d'une capture réseau** (Wireshark) pour **expliquer** l'alerte.

---

## 3. ⚙️ Contraintes

- **La règle d'origine** (« Serveurs » et « Sortie » uniquement, « Visiteurs » → DNS, DHCP, Internet) doit **rester vraie** pour tout ce qui n'est pas explicitement modifié.
- **Pas de simulation seule** : le filtrage tourne sur un pare-feu réel ou virtualisé.
- **Principe du moindre privilège** : chaque règle ouverte est justifiée dans le DAT.
- **Outils :** libres (pfSense ou OPNsense, Suricata, Wireshark, `nmap` pour tes tests).

---

## 4. ✅ Résultats attendus (tes tests de recette)

1. Je dois pouvoir **dessiner la matrice des flux** et **expliquer chaque règle**.
2. Je dois pouvoir **prouver** qu'un poste du VLAN Commercial atteint le VLAN Serveurs **et** qu'il n'atteint **pas** le VLAN Visiteurs.
3. Je dois pouvoir **prouver** qu'un poste du VLAN Visiteurs ne peut **interroger que** le DNS, le DHCP et Internet.
4. Je dois pouvoir **prouver** que depuis Internet, **seul le port HTTPS** de la DMZ répond, et que la base n'est **pas joignable** de l'extérieur.
5. Je dois pouvoir **revenir à l'état initial** en suivant ma procédure.
6. Je dois pouvoir **montrer l'impact** de l'évolution : quelle règle ancienne a été modifiée, et pourquoi.
7. *(extension)* Je dois pouvoir **montrer une alerte** déclenchée par un balayage de ports et **l'expliquer** à partir d'une capture.

---

## 5. 📤 Ce que tu fournis

Les livrables communs ([[conventions-gsb]] §4), plus :
- la **matrice des flux** (avant et après) ;
- l'**analyse d'impact** et le **plan de retour arrière** ;
- le **plan de tests** et ses **résultats** ;
- l'**export de la configuration du pare-feu**, sans secret ;
- les **captures** de tes tests (autorisés et interdits).

---

## 6. 🎓 Ce que cette mission te permet de montrer

| Famille | Sous-compétences (n° → [[conventions-gsb]] §7) |
|---|---|
| **Concevoir** | 1, **2** (impact), 3, 4, 5, 6 |
| **Installer, tester, déployer** | 7, 10, 11, 12 (bascule) |
| **Exploiter, dépanner, superviser** | 15 (journaux du pare-feu), 16 (incident) ; 13 et 14 en partie |

---

## 7. ⚠️ Pièges à éviter

- **Une règle « tout autoriser » provisoire** qui reste en place : à proscrire.
- **Ne tester que les flux autorisés** : la moitié de la recette consiste à prouver que ce qui doit être **interdit l'est**.
- **Oublier la base de données** : la DMZ ne doit jamais ouvrir un accès direct à la base depuis Internet.
- **Un plan de retour arrière écrit mais jamais essayé**.
