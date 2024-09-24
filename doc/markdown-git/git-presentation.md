# 1. Présentation et utilisation de Git

![logo de git](https://git-scm.com/images/logos/2color-lightbg@2x.png)

### 1.1 Qu'est-ce que Git ?

Git est un outil de versionning, il est utilisé principalement pour suivre les modifications apportées à des fichiers (souvent du code), mais il peut être utilisé pour gérer n'importe quel type de fichiers. Plus précisement c'est un logiciel de gestion de versions dit décentralisé, ce qui signifie que chaque utilisateur a une copie complète du projet.

### 1.2 Pourquoi utiliser Git ?

Git permet donc à plusieurs personnes de travailler simultanément sur le même projet, sans avoir à se soucier de perdre ou d'écraser les modifications de l'un ou de l'autre. Il enregistre chaque modification et permet de retracer l'historique de tout le projet, de revenir à une version précédente, de voir qui a fait quoi, et de fusionner des changements venant de différentes sources.

### 1.3 Git dans la pratique

Git suit les modifications sous forme de commits. Chaque commit est une sorte de "photo" de l'état de ton projet à un moment donné. Ces commits sont organisés de manière à pouvoir reconstruire l'historique complet du projet.

Voici un aperçu du fonctionnement de Git :

- Dépôt local et dépôt distant :
  Un dépôt Git (repository ou repo) est l'endroit où Git stocke les fichiers du projet et l'historique des modifications. Chaque utilisateur a une copie locale du dépôt.
  Les équipes partagent souvent un dépôt distant (comme sur GitHub ou GitLab), qui est une version centralisée du projet.

- Travail local :
  Travailler localement signifie que tu peux apporter des modifications à ton dépôt sans être connecté à un dépôt distant.
  Une fois que tu es satisfait de tes changements, tu les commits pour sauvegarder tes modifications dans l'historique local.

- Synchronisation avec le dépôt distant :
  Une fois les changements commis localement, tu peux utiliser des commandes comme git push pour envoyer tes modifications au dépôt distant.
  Tu peux aussi utiliser git fetch ou git pull pour récupérer les modifications faites par d'autres contributeurs depuis le dépôt distant.

### 1.4 Différence entre Git et GitHub

![logo de GitHub](https://devops.ruicoelho.pt/assets/images/github/github-logo.png)

Git est le logciel de versionning alors que GitHub est un service d'hébergement de dépôts Git.
Il permet aux développeurs de collaborer sur des projets Git de manière centralisée en fournissant des outils pour gérer, partager et visualiser les dépôts.
