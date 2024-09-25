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

## 3.3. Suivi des fichiers (`git add`)

La commande `git add` permet d'ajouter des modifications dans la "staging area", c’est-à-dire de préparer les fichiers pour un commit. Vous pouvez ajouter des fichiers individuels ou tous les fichiers modifiés.

### Ajouter un fichier spécifique :
```bash
git add monfichier.txt
```

### Ajouter tous les fichiers modifiés :
```bash
git add .
```

## 3.4. Committer des changements (`git commit`)

Une fois que les modifications sont ajoutées à la staging area avec `git add`, vous pouvez utiliser `git commit` pour enregistrer ces changements dans l'historique du projet. Chaque commit doit inclure un message descriptif.

### Exemple :
```bash
git commit -m "Ajout de la fonctionnalité X"
```

Cela enregistre un instantané des fichiers suivis dans Git avec le message fourni.

## 3.5. Vérifier l'état du dépôt (`git status`)

La commande `git status` montre l'état actuel du projet. Elle liste les fichiers modifiés, non suivis, ou en attente de commit, et donne un aperçu de ce qui se passe dans votre dépôt.

### Exemple :
```bash
git status
```

Cela vous aide à savoir quels fichiers sont prêts à être commités, lesquels ne sont pas encore suivis, et s'il y a des conflits à résoudre.

