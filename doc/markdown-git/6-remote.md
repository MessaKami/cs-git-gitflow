# 6. Gestion des Dépôts Distants

Ce document couvre les commandes Git liées à la gestion des dépôts distants. Les dépôts distants permettent de collaborer avec d'autres développeurs et de partager votre code sur des plateformes comme GitHub, GitLab, etc. Une bonne compréhension de ces commandes est essentielle pour le travail en équipe et le développement de logiciels.

### 6.1. Ajouter un Dépôt Distant

Pour ajouter un dépôt distant à votre projet Git, utilisez la commande suivante :

```bash
git remote add <nom> <url>
```

- **`<nom>`** : Un alias pour le dépôt distant. Par convention, le premier dépôt distant est souvent appelé `origin`, mais vous pouvez utiliser n'importe quel nom.
- **`<url>`** : L'URL du dépôt distant, qui peut être sous forme HTTPS ou SSH. Par exemple :
  - HTTPS : `https://github.com/votre-utilisateur/votre-depot.git`
  - SSH : `git@github.com:votre-utilisateur/votre-depot.git`

**Exemple :**

```bash
git remote add origin https://github.com/votre-utilisateur/votre-depot.git
```

**Vérification de l’ajout d’un dépôt distant :**

Après avoir ajouté un dépôt distant, vous pouvez vérifier qu'il a bien été ajouté en exécutant :

```bash
git remote -v
```

Cette commande affichera la liste des dépôts distants associés à votre projet, avec leurs URL respectives.

