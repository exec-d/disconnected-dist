# disconnected-dist

Le canal de distribution de [Disconnected](https://github.com/exec-d/disconnected) —
une application Android qui fait respecter le droit à la déconnexion.

Ce dépôt ne contient **pas de code**. Il ne contient que :

- `app/latest.json` — le manifeste que l'application consulte à son ouverture
  pour savoir s'il existe une version plus récente ;
- les APK signés, en pièces jointes des *releases*.

## Pourquoi un dépôt séparé

Le dépôt du code est privé, et les pièces jointes de ses releases ne sont donc
pas téléchargeables sans identifiants. Une application qui embarquerait un
jeton pour aller chercher ses propres mises à jour publierait ce jeton à toute
personne l'ayant installée.

Séparer les deux a un second effet, voulu : la visibilité du dépôt de code peut
changer plus tard, dans un sens ou dans l'autre, sans casser la mise à jour
chez les personnes qui ont déjà installé l'application.

## Ce que l'application vérifie avant de télécharger

Le manifeste est un fichier servi en clair. L'application n'accepte donc de
télécharger un APK que s'il est servi en HTTPS, depuis `github.com`, et depuis
le chemin des releases de ce dépôt précisément. Toute autre provenance est
refusée : mieux vaut ne proposer aucune mise à jour qu'une mise à jour dont on
ignore d'où elle vient.

## Publication

Automatique. La CI de `exec-d/disconnected` publie ici sur chaque tag `v*`,
puis réécrit `app/latest.json` — dans cet ordre, pour que le manifeste
n'annonce jamais une version dont l'APK n'est pas encore téléchargeable.

Les APK sont signés par la clé de release du projet. Une empreinte différente
d'une version à l'autre serait refusée à l'installation par Android : c'est la
garantie que la mise à jour vient bien du même auteur que ce qui est déjà
installé.

## Licence

L'application est publiée sous GPL-3.0-or-later. Les APK distribués ici le sont
sous cette licence ; le code source est dans `exec-d/disconnected`.
