**8. Dépannage et récupération**

Dans cette section, nous approfondirons les techniques de dépannage et de récupération dans Git. Vous apprendrez à annuler des commits indésirables, à récupérer des fichiers supprimés accidentellement, à résoudre des conflits complexes lors des fusions ou rebasages, et à sauvegarder et restaurer vos projets Git pour assurer la continuité de votre travail.

---

**8.1. Annuler un commit (git reset, git revert)**

Il est fréquent de commettre des changements que vous souhaitez annuler ou modifier. Git fournit plusieurs commandes pour gérer ces situations, notamment `git reset` et `git revert`. Comprendre la différence entre ces deux commandes est crucial pour manipuler l'historique de votre projet de manière sûre.

---

**git reset**

La commande `git reset` est utilisée pour réécrire l'historique local du dépôt. Elle modifie l'état de l'index (staging area), du répertoire de travail et du pointeur de la branche actuelle. Il existe trois principaux modes d'utilisation : `--soft`, `--mixed` et `--hard`.

- **Syntaxe générale** :
  
  ```bash
  git reset [options] [commit]
  ```

- **Options** :

  - `--soft` : Réinitialise le pointeur HEAD vers le commit spécifié, mais conserve les modifications dans l'index et le répertoire de travail. Les changements restent prêts à être commis.
  - `--mixed` (par défaut) : Réinitialise le HEAD et l'index. Les modifications restent dans le répertoire de travail, mais sont désindexées.
  - `--hard` : Réinitialise le HEAD, l'index et le répertoire de travail. **Attention : les modifications non sauvegardées seront perdues.**

- **Exemples pratiques** :

  - **Annuler le dernier commit tout en conservant les modifications dans l'index** :

    Supposons que vous avez commis un changement par erreur.

    ```bash
    git reset --soft HEAD~1
    ```

    - Cela déplace le HEAD vers le commit précédent (`HEAD~1`).
    - Les modifications du commit annulé restent indexées, prêtes à être recommises.

  - **Annuler le dernier commit et désindexer les modifications** :

    ```bash
    git reset HEAD~1
    ```

    - Équivalent à `git reset --mixed HEAD~1`.
    - Les modifications restent dans le répertoire de travail mais ne sont plus dans l'index.

  - **Annuler le dernier commit et supprimer les modifications associées** :

    ```bash
    git reset --hard HEAD~1
    ```

    - Le dépôt est remis à l'état du commit précédent.
    - **Toutes les modifications non commises seront perdues**.

- **Attention** :

  - L'utilisation de `git reset` pour réécrire l'historique peut causer des problèmes si vous avez déjà poussé les commits sur un dépôt distant partagé avec d'autres. Dans ce cas, préférez `git revert`.

---

**git revert**

La commande `git revert` est utilisée pour annuler les modifications introduites par un commit spécifique en créant un nouveau commit. Contrairement à `git reset`, elle ne réécrit pas l'historique, ce qui la rend plus sûre pour les dépôts partagés.

- **Syntaxe générale** :

  ```bash
  git revert [commit]
  ```

- **Exemples pratiques** :

  - **Annuler un commit spécifique** :

    Supposons que vous souhaitez annuler le commit `a1b2c3d`.

    ```bash
    git revert a1b2c3d
    ```

    - Git crée un nouveau commit qui inverse les changements introduits par `a1b2c3d`.
    - Si le commit cible modifie plusieurs fichiers, Git peut ouvrir un éditeur pour que vous confirmiez le message du commit de revert.

  - **Annuler plusieurs commits** :

    Pour annuler une série de commits, vous pouvez utiliser une plage :

    ```bash
    git revert a1b2c3d..d4e5f6g
    ```

    - Cela annule les commits de `a1b2c3d` (exclu) à `d4e5f6g` (inclus).
    - **Note** : L'ordre des commits dans la plage est important.

- **Gestion des conflits lors du revert** :

  - Si le revert entraîne des conflits, Git vous en informera.
  - Vous devrez résoudre les conflits de la même manière que pour une fusion.

---

**Scénario d'exemple :**

Supposons que vous avez commis un mot de passe sensible dans votre dépôt et que vous souhaitez l'enlever.

1. **Identifier le commit fautif** :

   ```bash
   git log --oneline
   ```

   - Notez l'ID du commit à annuler (par exemple, `b7c8d9e`).

2. **Utiliser git revert** :

   ```bash
   git revert b7c8d9e
   ```

   - Git crée un nouveau commit qui annule les changements.

3. **Pousser les modifications sur le dépôt distant** :

   ```bash
   git push origin main
   ```

   - Les modifications sont partagées avec l'équipe sans réécrire l'historique.

---

**8.2. Récupérer des fichiers supprimés**

Il peut arriver de supprimer accidentellement un fichier suivi par Git. Heureusement, Git conserve l'historique de vos fichiers, ce qui facilite leur récupération.

---

**Restaurer un fichier supprimé avant le commit**

Si vous avez supprimé un fichier, mais n'avez pas encore commis la suppression :

- **Commande** :

  ```bash
  git checkout -- [chemin/du/fichier]
  ```

- **Exemple** :

  Supposons que vous avez supprimé `src/app.js` par erreur.

  ```bash
  git checkout -- src/app.js
  ```

  - Le fichier est restauré à sa dernière version indexée.

---

**Restaurer un fichier supprimé après le commit**

Si vous avez déjà commis la suppression du fichier, vous devez récupérer une version antérieure du fichier depuis l'historique.

1. **Trouver le commit où le fichier existait** :

   ```bash
   git log -- [chemin/du/fichier]
   ```

   - Cela affiche l'historique des commits concernant ce fichier.
   - Notez l'ID du dernier commit où le fichier était présent (par exemple, `f1e2d3c`).

2. **Récupérer le fichier depuis ce commit** :

   ```bash
   git checkout [commit_id] -- [chemin/du/fichier]
   ```

   - **Exemple** :

     ```bash
     git checkout f1e2d3c -- src/app.js
     ```

     - Le fichier `src/app.js` est restauré à l'état qu'il avait dans le commit `f1e2d3c`.

3. **Valider la restauration** :

   - Ajoutez le fichier restauré à l'index :

     ```bash
     git add src/app.js
     ```

   - Commettez la restauration :

     ```bash
     git commit -m "Restauration de src/app.js supprimé par erreur"
     ```

---

**Astuce : Restauration rapide depuis le dernier état connu**

Si vous savez que vous voulez la dernière version du fichier avant sa suppression, vous pouvez utiliser :

```bash
git checkout HEAD~1 -- [chemin/du/fichier]
```

- Cela récupère le fichier depuis le commit précédent.

---

**8.3. Gérer les conflits complexes**

Lors de la fusion de branches ou du rebasage, des conflits peuvent survenir lorsque des modifications concurrentes sont apportées aux mêmes lignes de code. Gérer ces conflits de manière efficace est essentiel pour maintenir la stabilité du code.

---

**Étapes pour résoudre les conflits :**

1. **Identifier les fichiers en conflit**

   - Après une tentative de fusion ou de rebasage, Git vous avertira des conflits.
   - **Commande** :

     ```bash
     git status
     ```

     - Les fichiers en conflit seront marqués comme "unmerged".

2. **Analyser les conflits**

   - Ouvrez chaque fichier en conflit dans votre éditeur.
   - Les conflits sont marqués avec :

     ```text
     <<<<<<< HEAD
     Votre version du code
     =======
     Version du code de la branche fusionnée
     >>>>>>> [nom_de_la_branche]
     ```

3. **Résoudre les conflits manuellement**

   - Décidez quelle version du code conserver.
   - Vous pouvez choisir l'une des deux versions, ou combiner les deux.
   - Supprimez les marqueurs `<<<<<<<`, `=======`, `>>>>>>>`.

   - **Exemple** :

     Avant résolution :

     ```javascript
     function greet() {
       <<<<<<< HEAD
       console.log("Bonjour le monde");
       =======
       console.log("Hello world");
       >>>>>>> feature_branch
     }
     ```

     Après résolution :

     ```javascript
     function greet() {
       console.log("Bonjour le monde");
       console.log("Hello world");
     }
     ```

4. **Utiliser des outils de fusion**

   - Les outils graphiques peuvent faciliter la résolution des conflits, surtout pour les fichiers volumineux.

   - **Commande** :

     ```bash
     git mergetool
     ```

     - Configurez un outil de fusion dans votre configuration Git (par exemple, Meld, KDiff3).

   - **Configuration d'un outil de fusion** :

     - **Exemple avec Meld** :

       ```bash
       git config --global merge.tool meld
       ```

       - Puis lancez `git mergetool`.

5. **Valider la résolution des conflits**

   - Après avoir résolu les conflits dans un fichier, ajoutez-le à l'index :

     ```bash
     git add [chemin/du/fichier]
     ```

   - Vérifiez que tous les conflits sont résolus :

     ```bash
     git status
     ```

     - Il ne devrait plus y avoir de fichiers en conflit.

6. **Finaliser l'opération**

   - **Pour une fusion** :

     - Commettez les changements :

       ```bash
       git commit
       ```

       - Git utilisera par défaut le message de fusion.

   - **Pour un rebasage** :

     - Continuez le rebasage :

       ```bash
       git rebase --continue
       ```

     - Si vous souhaitez abandonner le rebasage :

       ```bash
       git rebase --abort
       ```

---

**Scénario d'exemple : Conflit lors d'une fusion**

Supposons que vous travaillez sur la branche `main` et que vous souhaitez fusionner la branche `feature` :

```bash
git checkout main
git merge feature
```

Git indique un conflit dans `src/app.js`.

1. **Vérifiez l'état** :

   ```bash
   git status
   ```

   - Le fichier `src/app.js` est en conflit.

2. **Ouvrez le fichier et résolvez le conflit**

3. **Ajoutez le fichier résolu** :

   ```bash
   git add src/app.js
   ```

4. **Terminez la fusion** :

   ```bash
   git commit
   ```

   - La fusion est maintenant complète.

---

**8.4. Sauvegarde et restauration de projets Git**

La sauvegarde régulière de votre dépôt Git est une bonne pratique pour prévenir la perte de données et faciliter la collaboration. Git offre plusieurs méthodes pour sauvegarder et restaurer vos projets.

---

**Cloner le dépôt vers un autre emplacement**

Le clonage du dépôt crée une copie complète de l'historique.

- **Commande** :

  ```bash
  git clone [url/chemin_du_dépôt] [chemin_de_destination]
  ```

- **Exemple** :

  - Sauvegarder le dépôt localement :

    ```bash
    git clone /path/to/your/repo /path/to/backup/repo_backup
    ```

- **Note** : Le clone contient tout l'historique du dépôt.

---

**Créer une archive du dépôt avec git bundle**

La commande `git bundle` permet de créer un fichier unique contenant l'intégralité du dépôt.

- **Créer un bundle** :

  ```bash
  git bundle create [nom_du_fichier.bundle] --all
  ```

- **Exemple** :

  ```bash
  git bundle create my_project.bundle --all
  ```

  - Le fichier `my_project.bundle` contient tout le dépôt.

- **Stockez le bundle** :

  - Vous pouvez copier le bundle sur un disque externe, un serveur distant ou le stocker dans le cloud.

---

**Restaurer un dépôt à partir d'un bundle**

- **Cloner le bundle** :

  ```bash
  git clone my_project.bundle /path/to/new_repo
  ```

- **Vérifier le dépôt restauré** :

  - Le nouveau dépôt contient tout l'historique et les branches du dépôt original.

- **Mettre à jour les remotes** :

  - Si vous souhaitez pousser vers un dépôt distant, ajoutez un remote :

    ```bash
    git remote add origin [url_du_dépôt_distant]
    git push -u origin --all
    ```

---

**Exporter une archive du dernier état du code**

Si vous avez besoin d'une copie du code sans le suivi Git (par exemple, pour livrer une version à un client) :

- **Commande** :

  ```bash
  git archive -o [nom_du_fichier.zip] [révision]
  ```

- **Exemple** :

  - Exporter le dernier état du code :

    ```bash
    git archive -o latest_code.zip HEAD
    ```

  - Exporter une version spécifique :

    ```bash
    git archive -o v1.0.0.zip v1.0.0
    ```

    - Où `v1.0.0` est le tag de la version.

---

**Sauvegarde automatisée avec des scripts**

Pour automatiser les sauvegardes, vous pouvez créer un script bash ou utiliser des outils comme `cron` pour exécuter régulièrement les commandes de sauvegarde.

- **Exemple de script de sauvegarde quotidienne** :

  ```bash
  #!/bin/bash

  BACKUP_DIR="/path/to/backup"
  DATE=$(date +%Y-%m-%d)
  REPO_PATH="/path/to/your/repo"

  cd $REPO_PATH
  git bundle create $BACKUP_DIR/backup_$DATE.bundle --all
  ```

- **Planifier le script avec cron** :

  - Éditez la crontab :

    ```bash
    crontab -e
    ```

  - Ajoutez une ligne pour exécuter le script tous les jours à 2h du matin :

    ```bash
    0 2 * * * /path/to/backup_script.sh
    ```

---