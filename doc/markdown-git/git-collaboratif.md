## 4. Travail collaboratif avec Git
---
### 4.1. Introduction aux branches
Git permet de gérer les branches pour travailler sur plusieurs fonctionnalités ou correctifs en parallèle. Chaque branche est un environnement indépendant où les développeurs peuvent effectuer des modifications sans perturber le travail des autres. La branche principale est souvent appelée `main` ou `master`, mais des branches spécifiques peuvent être créées pour développer de nouvelles fonctionnalités, corriger des bugs ou expérimenter.

---

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

---

## 4.3. Fusionner des branches (`git merge` et `git rebase`)
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

---

### 4.4. Gérer les conflits de merge
Un conflit de merge survient lorsque Git ne peut pas fusionner automatiquement deux branches en raison de modifications contradictoires dans les mêmes fichiers. Pour résoudre ces conflits :

- Git marquera les fichiers en conflit et vous demandera de les modifier manuellement. Les sections conflictuelles dans les fichiers seront marquées comme ceci :
  ```plaintext
  <<<<<<< HEAD
  // Votre version
  =======
  // La version fusionnée
  >>>>>>> branch-xyz
  ```

- Modifiez les fichiers pour choisir les changements à conserver, puis marquez-les comme résolus :
  ```bash
  git add <fichiers_conflits>
  ```

- Ensuite, terminez la fusion en créant un commit :
  ```bash
  git commit
  ```
  (Si vous aviez déjà fusionné tout sauf les conflits, ce commit finalisera la fusion après résolution.)

- **Astuce** : Utilisez des outils de merge graphique comme **`git mergetool`** pour faciliter la résolution des conflits.

---

### 4.5. Envoyer des modifications vers un dépôt distant (`git push`)
Une fois vos modifications localement prêtes et validées avec un commit, vous pouvez les partager avec les autres membres de l'équipe en les envoyant sur un dépôt distant.

- **Envoyer une branche spécifique** :
  ```bash
  git push origin <nom_branche>
  ```
  Cela envoie les commits de la branche `<nom_branche>` vers le dépôt distant associé à l'alias `origin` (par défaut, le dépôt distant que vous avez cloné).

- **Envoyer toutes les branches locales** :
  ```bash
  git push --all origin
  ```

- **Forcer un push (avec précaution)** :
  Si vous avez besoin de réécrire l’historique des commits (après un rebase par exemple), utilisez l’option `--force`, mais faites-le avec précaution :
  ```bash
  git push --force

  ---


### 4.6. Récupérer les modifications d'un dépôt distant (`git pull`)
Pour garder votre dépôt local synchronisé avec les modifications faites par les autres membres de l'équipe, vous devez régulièrement récupérer et fusionner les mises à jour du dépôt distant.

- **Récupérer et fusionner en une seule commande** :
  ```bash
  git pull
  ```
  Cette commande effectue un `git fetch` (pour récupérer les nouvelles données) suivi d'un `git merge` (pour fusionner ces nouvelles données dans votre branche locale).

- **Pull en fast-forward** : Si votre branche locale est derrière la branche distante, Git fera un fast-forward pour mettre à jour votre branche locale.

- **Pull avec conflits** : Si des modifications locales et distantes entrent en conflit, vous devrez résoudre les conflits manuellement avant de terminer le `git pull`.