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
## 4.3. Fusionner des branches (`git merge`, `git rebase`)
Lorsque vous travaillez avec des branches, il existe deux manières principales d'intégrer les modifications d'une branche dans une autre : **merge** et **rebase**. Alors que `git merge` conserve l'historique de la branche séparée, `git rebase` réécrit l'historique pour donner l'apparence que toutes les modifications ont été faites en ligne droite, ce qui peut rendre l'historique plus propre.

- **Fusionner une branche avec `git rebase`** :
  ```bash
  git rebase <branche_source>
  ```
  Cela déplace vos commits locaux au sommet des derniers commits de la branche source, évitant ainsi la création d'un commit de merge.

- **Cas d'usage typique du rebase** : 
  Le rebase est utile pour maintenir une branche à jour avec la branche principale (`main`) sans polluer l’historique avec des commits de fusion. Par exemple, avant de fusionner votre branche de travail dans `main`, vous pouvez d'abord réappliquer vos commits au sommet de `main` en faisant :
  ```bash
  git checkout feature-branch
  git rebase main
  ```

- **Résolution des conflits pendant un rebase** : Comme avec `git merge`, des conflits peuvent survenir pendant un rebase. Si cela arrive :
  1. Résolvez les conflits manuellement dans les fichiers concernés.
  2. Une fois les conflits résolus, marquez-les comme résolus avec :
     ```bash
     git add <fichiers_conflits>
     ```
  3. Continuez le rebase avec :
     ```bash
     git rebase --continue
     ```
  4. Si vous voulez annuler un rebase en cours :
     ```bash
     git rebase --abort
     ```

- **Rebase vs Merge** : 
  - `git merge` préserve l'historique des branches parallèles et crée un commit de merge, ce qui est utile pour visualiser toutes les branches et leur relation.
  - `git rebase` réécrit l'historique en appliquant vos commits au sommet des nouveaux commits, créant un historique linéaire. Cela rend l'historique plus simple, mais vous perdez la trace des branches parallèles.
