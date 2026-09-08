# Déconnecté

Une application Android qui fait respecter le **droit à la déconnexion** : elle
retient les notifications de vos applications de travail pendant vos périodes
de repos, et vous les rend quand vos horaires reprennent.

Rien n'est supprimé. Ce qui arrive pendant le repos est mis en sommeil, et
réapparaît dans le volet à l'heure de reprise.

- **Version actuelle : [0.3.0](https://github.com/exec-d/disconnected-dist/releases/latest)**
- Android 10 ou plus récent
- Gratuit, sans publicité, sans compte, sans traqueur
- Application **non officielle et hors magasin** : elle s'installe à la main

---

## Installer

1. Ouvrez **[la dernière version](https://github.com/exec-d/disconnected-dist/releases/latest)**
   depuis le téléphone et téléchargez le fichier `disconnected-vX.Y.Z.apk`.
2. Ouvrez le fichier téléchargé. Android va refuser et proposer un réglage :
   autorisez **« Installer des applications inconnues »** pour votre
   navigateur. C'est normal pour une application distribuée hors magasin, et
   vous pouvez retirer cette autorisation juste après.
3. Installez, puis ouvrez l'application. Elle vous guide en trois étapes :
   vos horaires, vos applications de travail, puis l'accès aux notifications.

**Les mises à jour se font toutes seules ensuite.** L'application vérifie
qu'une version plus récente existe, vous le dit, et l'installe si vous
acceptez. Vous n'aurez pas à revenir ici.

> ⚠️ **Une installation manuelle bloque le réglage clé sur Android 13 et plus.**
> Le bouton « Accès aux notifications » reste grisé tant que vous n'avez pas
> ouvert la fiche de l'application dans les réglages Android et choisi
> **« Autoriser les paramètres restreints »** dans le menu ⋮. L'application
> vous explique ce passage au moment où il se présente ; c'est le seul endroit
> où l'installation hors magasin coûte quelque chose.

---

## Ce qu'elle demande, et pourquoi

**L'accès aux notifications** est la seule chose importante, et c'est
beaucoup : Android ne permet pas de retenir une notification sans donner le
droit de les lire toutes. Sans cet accès, l'application ne peut rien faire.

Ce qu'elle en fait :

- elle regarde le paquet émetteur et l'heure d'arrivée, et met en sommeil ce
  qui vient des applications **que vous avez choisies**, pendant les périodes
  de repos **que vous avez déclarées** ;
- tout le reste — vos proches, vos rappels, vos alarmes — n'est jamais touché ;
- elle garde un compteur par jour, et les cent dernières retenues (application
  et heure, jamais le contenu), effaçables d'un bouton.

**Rien de tout cela ne quitte le téléphone.** L'application n'a qu'un seul
usage du réseau : télécharger un petit fichier qui dit s'il existe une version
plus récente. Aucune information sur vos notifications, vos horaires ou vos
correspondants n'est envoyée nulle part — il n'y a pas de serveur.

Les autres autorisations que la fiche Android affichera : installer des
applications (les mises à jour), démarrer au redémarrage (retrouver vos
horaires après un reboot), poster une notification (la ligne d'état pendant vos
repos), « Ne pas déranger » (facultatif, proposé dans les réglages), et trois
autorisations techniques venant de la bibliothèque de tâches de fond
(`FOREGROUND_SERVICE`, `WAKE_LOCK`, `ACCESS_NETWORK_STATE`).

---

## Un problème, une remarque

Écrivez à **k@levilainpetit.dev**. L'application propose aussi un formulaire :
**Réglages → (i) → Écrire**, qui pré-remplit la version installée et le modèle
du téléphone — utile pour comprendre un problème sans avoir à vous le demander.

C'est une bêta. Elle est utilisée quotidiennement par son auteur, elle n'a pas
encore été regardée par beaucoup d'autres, et les retours sur ce qui est
déroutant valent autant que ceux sur ce qui est cassé.

---

## Licence et code source

L'application est publiée sous **GPL-3.0-or-later**. Le texte de la licence est
inclus dans le dépôt du code.

Le dépôt du code n'est pas public aujourd'hui. **Offre écrite :** pendant au
moins trois ans à compter de la mise à disposition de chaque version, l'auteur
fournira à toute personne possédant un de ces APK le code source complet
correspondant à cette version, sous GPL-3.0-or-later, sur simple demande à
**k@levilainpetit.dev** et sans frais autres que le coût éventuel du support.

Les polices JetBrains Mono incluses dans l'application sont sous SIL Open Font
License 1.1.

---

## Ce dépôt

Il ne contient **pas de code**. Seulement le manifeste de mise à jour
(`app/latest.json`) que l'application consulte, et les APK signés en pièces
jointes des *releases*.

**Pourquoi séparé du code.** Les pièces jointes des releases d'un dépôt privé
ne sont pas téléchargeables sans identifiants, et une application qui
embarquerait un jeton pour aller chercher ses propres mises à jour publierait
ce jeton à toute personne l'ayant installée. La séparation a un second effet,
voulu : la visibilité du dépôt de code peut changer, dans un sens ou dans
l'autre, sans casser la mise à jour chez les personnes déjà équipées.

**Ce que l'application vérifie avant de télécharger.** Le manifeste est servi
en clair. L'application n'accepte donc un APK que s'il est servi en HTTPS,
depuis `github.com`, et depuis le chemin des releases de ce dépôt précisément.
Toute autre provenance est refusée : mieux vaut ne proposer aucune mise à jour
qu'une mise à jour dont on ignore d'où elle vient.

**Publication.** Automatique, à chaque tag `v*` : l'APK est publié ici, puis
`app/latest.json` est réécrit — dans cet ordre, pour que le manifeste
n'annonce jamais une version dont l'APK n'est pas encore téléchargeable. Les
APK sont signés par la clé de release du projet ; une empreinte différente
d'une version à l'autre serait refusée par Android à l'installation, ce qui est
la garantie que la mise à jour vient du même auteur que ce qui est déjà là.
