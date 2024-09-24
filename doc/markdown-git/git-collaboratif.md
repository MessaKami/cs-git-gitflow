## 4. Travail collaboratif avec Git

### 4.1. Introduction aux branches
Git permet de gérer les branches pour travailler sur plusieurs fonctionnalités ou correctifs en parallèle. Chaque branche est un environnement indépendant où les développeurs peuvent effectuer des modifications sans perturber le travail des autres. La branche principale est souvent appelée `main` ou `master`, mais des branches spécifiques peuvent être créées pour développer de nouvelles fonctionnalités, corriger des bugs ou expérimenter.

### 4.2. Créer et basculer entre les branches (`git branch`, `git checkout`, `git switch`)
- **Créer une nouvelle branche** : 
  ```bash
  git branch <nom_branche>
  ```
  Cela crée une nouvelle branche, mais vous restez sur la branche actuelle.
  
- **Basculer sur une branche** :
  - **Ancienne méthode** (encore utilisée, surtout dans les versions plus anciennes de Git) :
    ```bash
    git checkout <nom_branche>
    ```
    Cela change votre branche actuelle à `<nom_branche>`.

  - **Nouvelle méthode** (préférée depuis Git 2.23) :
    ```bash
    git switch <nom_branche>
    ```
    Cette commande est plus explicite et intuitive pour changer de branche.

- **Créer et basculer en même temps** : 
  Si vous souhaitez créer une nouvelle branche et y basculer directement :
  ```bash
  git checkout -b <nom_branche>
  ```
  ou
  ```bash
  git switch -c <nom_branche>
  ```
### 4.3. Fusionner des branches (`git merge`)
Une fois que vous avez terminé de travailler sur une fonctionnalité dans une branche, vous voudrez probablement fusionner cette branche dans une autre (souvent la branche principale). La fusion permet d’intégrer les modifications de la branche source dans la branche cible.

- **Fusionner une branche** :
  Assurez-vous d’être sur la branche où vous voulez fusionner (par exemple, la branche `main`), puis exécutez :
  ```bash
  git merge <nom_branche>
  ```
  Cela fusionnera les modifications de `<nom_branche>` dans la branche actuelle.

- **Fusion en fast-forward** :
  Si la branche que vous fusionnez n'a pas de commits intermédiaires qui diffèrent de la branche actuelle, Git peut effectuer une fusion "fast-forward", ce qui signifie qu'il avance simplement la tête de la branche actuelle vers le dernier commit de la branche fusionnée.

- **Fusion avec commit de merge** :
  Si la branche a des commits différents, Git créera un commit de fusion pour enregistrer l'historique de la fusion.