---
titre: "Mission N1 — Accès distant et interconnexion sécurisés"
tags: [eleves, u6, mission, gsb, N1, vpn, bastion]
mission: N1
duree: "≈ 20 h (socle 14 h + extension 6 h)"
public: étudiants
---

# 🔐 Mission N1 — Accès distant et interconnexion sécurisés

> Conventions : [[conventions-gsb]] · Contexte : [[fiche-gsb]] · Retour : [[README]]

## 🪪 Fiche d'identité de la mission

| | |
|---|---|
| **Intitulé** | Mise en place des accès distants sécurisés du système informatique de GSB |
| **Présentation rapide** | Permettre aux **visiteurs médicaux** de se connecter en toute sécurité depuis l'extérieur, **protéger la liaison** entre le siège et un site distant, et **administrer les serveurs à distance** sans les exposer |
| **Durée** | **Socle** (lots 1 et 3) ≈ 14 h · **Extension** (lot 2) ≈ 6 h |
| **Modalités de réception** | Recette sur ton laboratoire + dossier technique + présentation orale |
| **Équipe** | Individuel ou binôme (précise ta part personnelle) |

---

## 1. 🎯 Le besoin de GSB

Les **480 visiteurs médicaux** travaillent en déplacement : hôtels, salles de congrès, cabinets. Ils doivent atteindre l'application de suivi des visites et les informations de l'intranet, aujourd'hui **limités au site parisien**. La **messagerie et l'intranet ne sont pas ouverts** depuis Internet : des services externalisés servent de relais.

Par ailleurs, les données de l'entreprise sont **stratégiques** et **répliquées chaque jour vers les États-Unis** par un lien dédié. La DSI veut un **canal chiffré** pour cette réplication et un moyen d'**administrer les serveurs à distance sans exposer leur accès** sur Internet.

**Questions de ton analyse :** quelles données traversent ces liens ? Un **transfert hors de l'Union européenne** est-il encadré ? Quels risques en cas de perte ou de vol d'un poste de visiteur ?

---

## 2. 🧱 Ce qu'il faut mettre en place

### Lot 1 — VPN pour les visiteurs (socle, ≈ 8 h)
- Un **serveur VPN** (client-à-site) sur le pare-feu ou sur un serveur dédié, avec **authentification** (comptes d'un annuaire ou clés individuelles).
- Une **séparation des droits** : un visiteur connecté n'atteint que l'**application de suivi** (DMZ, VLAN 350) ; il n'a accès ni aux autres serveurs ni aux autres VLAN.
- Un **script** qui génère le **profil de connexion** d'un nouveau visiteur et un moyen de **révoquer** un accès.
- Un **test depuis un terminal mobile** (smartphone ou tablette) et depuis un poste portable.

### Lot 3 — Administration à distance sécurisée (socle, ≈ 6 h)
- Un **bastion** : seul point d'entrée pour administrer les serveurs, avec connexion **par clé** (pas de mot de passe), accès **réservé** aux membres du service Réseau et Système, et **journal des connexions**.
- **Aucun accès direct** aux serveurs depuis Internet : tout passe par le bastion.
- Des **journaux exploités** : repérer les tentatives échouées et déclencher une alerte simple (par exemple blocage temporaire après plusieurs échecs).

### Lot 2 — Liaison siège ↔ site distant (extension, ≈ 6 h)
- Un **tunnel chiffré** entre le pare-feu du siège (Paris) et celui d'un **site distant** (172.22.0.0/24, simulé).
- Une **réplication de données** (par exemple un dossier synchronisé chaque nuit) qui **passe dans le tunnel**.
- La **vérification** que le trafic de réplication est bien chiffré (capture réseau).

---

## 3. ⚙️ Contraintes

- **Sécurité :** aucun accès administrateur exposé directement sur Internet ; mots de passe interdits pour le bastion.
- **Disponibilité :** un visiteur doit pouvoir se **reconnecter** après une coupure sans intervention d'un technicien.
- **Droit :** les données traitées (visiteurs, praticiens) sont **personnelles** : justifie la protection retenue.
- **Outils :** libres de préférence (WireGuard, OpenVPN, IPsec, OpenSSH ; Apache Guacamole accepté pour le bastion). Compare **au moins deux** technologies de VPN dans ton dossier de choix.

---

## 4. ✅ Résultats attendus (tes tests de recette)

1. Je dois pouvoir **connecter un visiteur** depuis l'extérieur et **ouvrir l'application** de suivi.
2. Je dois pouvoir **prouver** qu'un visiteur connecté **n'atteint aucun autre serveur** que l'application.
3. Je dois pouvoir **créer un accès** en une commande (script) et le **révoquer** : l'ancien accès ne fonctionne plus.
4. Je dois pouvoir **me connecter depuis un smartphone ou une tablette**.
5. Je dois pouvoir **administrer un serveur uniquement via le bastion** ; une connexion directe depuis l'extérieur est refusée.
6. Je dois pouvoir **montrer le journal** d'une connexion réussie et d'une tentative échouée.
7. *(extension)* Je dois pouvoir **montrer que la réplication est chiffrée** (capture) et qu'elle **reprend** après une coupure du tunnel.

---

## 5. 📤 Ce que tu fournis

Les livrables communs ([[conventions-gsb]] §4), plus :
- le **dossier de choix** (comparaison de deux technologies de VPN) ;
- le **script de création et de révocation** des accès ;
- les **captures** (connexion, refus, journaux) ;
- une **procédure** « intégrer un nouveau visiteur » lisible par un tiers.

---

## 6. 🎓 Ce que cette mission te permet de montrer

| Famille | Sous-compétences (n° → [[conventions-gsb]] §7) |
|---|---|
| **Concevoir** | 1 (cadre juridique), 3 (choix de VPN), 5 (maquette), 6 (tests) |
| **Installer, tester, déployer** | 7, 10, 11, 12 (déploiement des profils) |
| **Exploiter, dépanner, superviser** | **13** (bastion), **14** (script d'accès), **15** (journaux), 16 (incident) |

---

## 7. ⚠️ Pièges à éviter

- **Un VPN qui donne accès à tout le réseau** : c'est le défaut le plus fréquent. Prouve le **filtrage**.
- **Une clé ou un mot de passe dans le dépôt Git** : interdit.
- **Tester uniquement depuis la machine qui héberge le serveur** : teste depuis un client réellement extérieur.
- **Oublier la révocation** : un accès qu'on ne sait pas retirer est un risque.
