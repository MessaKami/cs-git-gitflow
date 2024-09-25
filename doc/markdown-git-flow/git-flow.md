# Git Flow : Workflow avancé de gestion des branches

## 1. Introduction à Git Flow
Git Flow est une méthodologie de gestion de branches conçue pour organiser le développement logiciel de manière claire et structurée. Elle est particulièrement adaptée aux projets avec plusieurs contributeurs et des versions régulières. Git Flow propose plusieurs types de branches pour différents rôles dans le cycle de développement : développement de fonctionnalités, préparation des versions, correctifs urgents, etc.

## 2. Installation de Git Flow

#### Sur macOS :
Installez Git Flow via Homebrew :
```bash
brew install git-flow-avh
```

#### Sur Linux (Ubuntu/Debian) :
Utilisez la commande apt-get pour installer Git Flow :
```bash
sudo apt-get install git-flow
```

#### Sur Windows :
Git Flow peut être installé via **Git for Windows** ou **Scoop** :
- **Via Git for Windows** : Téléchargez et installez [Git for Windows](https://gitforwindows.org/), qui inclut une option pour installer Git Flow.
- **Via Scoop** :
  ```bash
  scoop install git-flow
  ```

## 3. Initialisation de Git Flow
Une fois que Git Flow est installé, vous devez l'initialiser dans votre dépôt Git existant. Cette étape configure les branches principales (`main` et `develop`) et définit les conventions de nommage pour les autres types de branches.

- **Initialiser Git Flow** :
  ```bash
  git flow init
  ```
  Lors de l'initialisation, Git Flow vous demandera de confirmer les noms des branches (`main`, `develop`, etc.) et vous proposera des valeurs par défaut que vous pouvez accepter ou personnaliser.
