# 2.1. Installation et Configuration de Git sur Windows, macOS et Linux

## Introduction

Git est un système de contrôle de version distribué qui permet de suivre les modifications apportées aux fichiers et de coordonner le travail entre plusieurs personnes. Ce guide vous aidera à installer et configurer Git sur les principaux systèmes d'exploitation : **Windows**, **macOS** et les distributions **Linux** les plus populaires.

---

## Installation de Git

### Windows

#### Méthode 1 : Utiliser Git for Windows

1. **Télécharger l'installateur :**
   - Rendez-vous sur le site officiel : [git-scm.com/download/win](https://git-scm.com/download/win).
   - Le téléchargement devrait commencer automatiquement.

2. **Installer Git :**
   - Exécutez le fichier téléchargé (`.exe`).
   - Suivez les instructions de l'assistant d'installation.
   - Vous pouvez généralement laisser les options par défaut, sauf si vous avez des préférences spécifiques.

#### Méthode 2 : Utiliser le Gestionnaire de Packages Chocolatey

1. **Installer Chocolatey :**
   - Ouvrez **PowerShell** en tant qu'administrateur.
   - Exécutez la commande suivante :

     ```powershell
     Set-ExecutionPolicy Bypass -Scope Process -Force; `
     [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; `
     iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
     ```

2. **Installer Git via Chocolatey :**

   ```powershell
   choco install git -y
   ```

### macOS

#### Méthode 1 : Utiliser Homebrew

1. **Installer Homebrew** (si ce n'est pas déjà fait) :

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. **Installer Git :**

   ```bash
   brew install git
   ```

#### Méthode 2 : Télécharger l'Installateur Git

1. **Télécharger l'installateur :**
   - Rendez-vous sur : [git-scm.com/download/mac](https://git-scm.com/download/mac).
   - Cliquez sur le lien pour télécharger l'installateur.

2. **Installer Git :**
   - Ouvrez le paquet `.dmg` téléchargé.
   - Suivez les instructions pour installer Git.

#### Méthode 3 : Utiliser les Outils de Ligne de Commande Xcode

- **Ouvrez le Terminal** et tapez :

  ```bash
  git --version
  ```

- Si Git n'est pas installé, une invite s'affichera pour installer les outils de ligne de commande.

### Linux

#### Ubuntu / Debian

```bash
sudo apt update
sudo apt install git
```

#### Fedora

```bash
sudo dnf install git
```

#### CentOS / RHEL

```bash
sudo yum install git
```

#### Arch Linux

```bash
sudo pacman -S git
```

#### openSUSE

```bash
sudo zypper install git
```

---

## 2.2. Configuration Initiale de Git

Après l'installation, configurez Git avec votre nom et votre adresse e-mail pour associer vos commits à votre identité.

### Configurer le Nom d'Utilisateur et l'Adresse E-mail

```bash
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@example.com"
```

### Configurer l'Éditeur de Texte par Défaut

Définissez l'éditeur qui s'ouvrira pour écrire vos messages de commit.

- **Pour Visual Studio Code :**

  ```bash
  git config --global core.editor "code --wait"
  ```

- **Pour Vim :**

  ```bash
  git config --global core.editor "vim"
  ```

### Configurer le Diff Viewer (Optionnel)

Améliorez la lisibilité des diffs avec un outil comme **Delta**.

#### Installer Delta

- **macOS (Homebrew) :**

  ```bash
  brew install git-delta
  ```

- **Ubuntu/Debian :**

  ```bash
  sudo apt install git-delta
  ```

- **Arch Linux :**

  ```bash
  sudo pacman -S git-delta
  ```

#### Configurer Git pour Utiliser Delta

```bash
git config --global core.pager "delta --line-numbers --dark"
git config --global delta.navigate true
```

### Créer des Alias Utiles

Simplifiez vos commandes Git avec des alias.

```bash
git config --global alias.st status
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.last "log -1 HEAD"
```

### Vérifier la Configuration

Pour afficher toutes vos configurations :

```bash
git config --list
```

---

## Première Utilisation de Git

### Cloner un Dépôt

```bash
git clone https://github.com/utilisateur/nom-du-depot.git
```

### Initialiser un Nouveau Dépôt

```bash
git init
```

### Ajouter des Fichiers au Suivi

```bash
git add nom-du-fichier
```

Ou pour ajouter tous les fichiers :

```bash
git add .
```

### Valider les Modifications

```bash
git commit -m "Message de commit"
```

### Pousser les Modifications vers le Dépôt Distant

```bash
git push origin branche
```

---

## 2.3. Générer et Ajouter une Clé SSH

Pour sécuriser vos interactions avec les plateformes Git telles que GitHub, GitLab ou Bitbucket, il est recommandé d'utiliser une clé SSH. Cela permet une authentification sécurisée sans avoir à saisir votre mot de passe à chaque opération.

#### Générer une Clé SSH

##### Sous Windows

1. **Ouvrez Git Bash** (installé avec Git for Windows).
2. **Générez une nouvelle clé SSH** en exécutant la commande suivante :

   ```bash
   ssh-keygen -t ed25519 -C "votre.email@example.com"
   ```

   > **Note :** Si vous utilisez une version de Windows antérieure ou si `ed25519` n'est pas pris en charge, vous pouvez utiliser :

   ```bash
   ssh-keygen -t rsa -b 4096 -C "votre.email@example.com"
   ```

3. **Appuyez sur Entrée** pour accepter l'emplacement par défaut du fichier (`/c/Users/VotreNom/.ssh/id_ed25519`).
4. **Saisissez une phrase de passe** (optionnel mais recommandé) ou appuyez sur Entrée pour aucune phrase de passe.

##### Sous macOS et Linux

1. **Ouvrez le Terminal**.
2. **Générez une nouvelle clé SSH** :

   ```bash
   ssh-keygen -t ed25519 -C "votre.email@example.com"
   ```

   > **Note :** Si `ed25519` n'est pas disponible :

   ```bash
   ssh-keygen -t rsa -b 4096 -C "votre.email@example.com"
   ```

3. **Appuyez sur Entrée** pour accepter l'emplacement par défaut (`/home/votre_nom/.ssh/id_ed25519`).
4. **Entrez une phrase de passe** (optionnel).

#### Ajouter la Clé SSH à l'Agent SSH

##### Démarrer l'Agent SSH

- **Sous Windows (Git Bash) :**

  ```bash
  eval "$(ssh-agent -s)"
  ```

- **Sous macOS :**

  ```bash
  eval "$(ssh-agent -s)"
  ```

- **Sous Linux :**

  L'agent SSH est généralement déjà en cours d'exécution. Sinon, démarrez-le :

  ```bash
  eval "$(ssh-agent -s)"
  ```

##### Ajouter la Clé Privée à l'Agent SSH

- **Commande universelle :**

  ```bash
  ssh-add ~/.ssh/id_ed25519
  ```

  > Si vous avez utilisé une clé RSA, utilisez :

  ```bash
  ssh-add ~/.ssh/id_rsa
  ```

##### Sous macOS : Ajouter la Configuration

Pour que l'agent SSH charge automatiquement les clés, créez ou modifiez le fichier `~/.ssh/config` :

```bash
touch ~/.ssh/config
```

Ajoutez les lignes suivantes :

```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

#### Ajouter la Clé SSH à votre Compte GitHub

1. **Copiez la clé publique** dans votre presse-papiers :

   - **Sous Windows (Git Bash) :**

     ```bash
     clip < ~/.ssh/id_ed25519.pub
     ```

   - **Sous macOS :**

     ```bash
     pbcopy < ~/.ssh/id_ed25519.pub
     ```

   - **Sous Linux :**

     ```bash
     xclip -sel clip < ~/.ssh/id_ed25519.pub
     ```

     > **Note :** Si `xclip` n'est pas installé, vous pouvez l'installer avec :

     ```bash
     sudo apt install xclip
     ```

     Ou afficher la clé et la copier manuellement :

     ```bash
     cat ~/.ssh/id_ed25519.pub
     ```

2. **Connectez-vous à votre compte GitHub**.
3. **Allez dans les Paramètres** (Settings).
4. **Sélectionnez "SSH and GPG keys"** dans le menu de gauche.
5. **Cliquez sur "New SSH key"** ou "Add SSH key".
6. **Donnez un titre** à votre clé (par exemple, "Ordinateur Portable").
7. **Collez la clé publique** dans le champ "Key".
8. **Cliquez sur "Add SSH key"**.

#### Vérifier la Connexion SSH

Pour tester si tout fonctionne correctement, exécutez :

```bash
ssh -T git@github.com
```

Vous devriez recevoir un message similaire à :

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## Ressources Supplémentaires

- [Documentation Officielle de Git](https://git-scm.com/doc)
- [Pro Git Book (français)](https://git-scm.com/book/fr/v2)
- [Cheat Sheet Git](https://education.github.com/git-cheat-sheet-education.pdf)
