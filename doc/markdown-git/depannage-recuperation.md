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