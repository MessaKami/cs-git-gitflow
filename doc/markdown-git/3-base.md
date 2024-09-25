# Guide Git - Commandes de base

Ce guide présente les principales commandes Git utilisées dans la gestion de version et le suivi de projets.

## 3.1. Initialiser un dépôt Git (git init)

La commande `git init` permet d'initialiser un nouveau dépôt Git dans un répertoire existant. Elle crée un répertoire `.git` qui contient toutes les informations nécessaires à la gestion de version pour ce projet.

### Exemple :
```bash
git init
```

Après cette commande, Git commence à suivre les modifications dans ce dossier.

## 3.2. Cloner un dépôt (`git clone`)

`git clone` est utilisé pour copier un dépôt Git existant (local ou distant) vers votre machine. Cela inclut tout l'historique et les fichiers actuels du projet.

### Exemple :
```bash
git clone https://github.com/utilisateur/nom-du-repo.git
```

Cela crée un dossier local contenant les fichiers du dépôt, ainsi que son historique.
