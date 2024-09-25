### 7.3 Gestion des conflits

# Gestion des Conflits Git - Cheat Sheet

Les conflits Git se produisent lorsque des modifications concurrentes sont effectuées sur les mêmes lignes d'un fichier ou lorsqu'un fichier est supprimé dans une branche et modifié dans une autre. Ce cheat sheet fournit un guide rapide pour identifier, résoudre et prévenir les conflits Git.

---

## Sommaire

- [Identification des Conflits](#identification-des-conflits)
- [Visualisation des Fichiers en Conflit](#visualisation-des-fichiers-en-conflit)
- [Résolution des Conflits](#résolution-des-conflits)
- [Abandonner une Opération en Cours](#abandonner-une-opération-en-cours)
- [Utilisation d'Outils de Fusion](#utilisation-doutils-de-fusion)
- [Prévention des Conflits](#prévention-des-conflits)
- [Commandes Utiles](#commandes-utiles)
- [Astuces](#astuces)

---

## Identification des Conflits

Lors d'une opération `git merge`, `git rebase` ou `git cherry-pick`, Git peut signaler des conflits :

```bash
$ git pull
Auto-merging fichier.txt
CONFLICT (content): Merge conflict in fichier.txt
Automatic merge failed; fix conflicts and then commit the result.
```

## Visualisation des Fichiers en Conflit

Liste des fichiers en conflit :

```bash
$ git status
```

Les fichiers en conflit apparaîtront sous la section **"Unmerged paths"**.

## Résolution des Conflits

1. **Ouvrir les fichiers en conflit** : Les marqueurs de conflit ressemblent à ceci :

   ```diff
   <<<<<<< HEAD
   Contenu de la branche actuelle.
   =======
   Contenu de la branche fusionnée.
   >>>>>>> nom-de-la-branche
   ```

2. **Éditer les fichiers** : Choisissez quelles modifications conserver ou combinez-les.

3. **Marquer les conflits comme résolus** :

   ```bash
   $ git add fichier.txt
   ```

4. **Valider les modifications** :

   ```bash
   $ git commit -m "Résolution des conflits sur fichier.txt"
   ```

## Abandonner une Opération en Cours

- **Annuler une fusion** :

  ```bash
  $ git merge --abort
  ```

- **Annuler un rebase** :

  ```bash
  $ git rebase --abort
  ```

