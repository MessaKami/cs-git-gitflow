# Les fonctionnalités avancées de Git

### 5.1. Git Stash : Sauvegarder des modifications temporaires

Concrètement le git stash va te permettre de mettre en attente des changements sans les commits.\
Puisqu'il est utilisable plusieurs fois, il est possible d'accéder à l'historique avec :

`git stash list`

Tu peux ainsi abandonner des modifications avec :

`git stash drop stash{0}` (index du stash dans la liste)

Ou récupérer des modifications avec :

`git stash pop {0}`

Si tu veux récupérer tes changements sans les retirer du stash :

`it stash apply stash{0}.`

Si tu veux tout stash sans inclure les fichiers déjà indexer par git add, tu peux utiliser :

`git stash --keep-index`

Si tu veux inclure les fichiers non-traqués :

`git stash -u`

### 5.2. Rebase

Pour faire simple, git rebase va permettre de rendre propre notre historique git ; notamment dans l’utilisation des branches. Cette commande va permettre de prendre une branche et de venir la greffer ailleurs dans notre historique.

Imaginons que la branche principale ressemble à ça :

A - B – C

Que ta branche ressemble à ça :

A – B - D

Si tu fais un git rebase, cela prendra les modifications de C et viendra greffer tes modifications (D) après. Au niveau de l’historique, il va fusionner les commits de manière linéaire. Cela peut engendrer plusieurs conflits, un par commit.

A – B – C - D

A l’instar de git rebase, le git merge va venir créer un nouveau commit de fusion sans réécrire l’historique. Cela permet d’avoir un historique plus complet mais si l’on travaille avec plusieurs branches, cela peut vite rendre l’historique trop complexe dans la mesure où il va conserver séparément l’historique des deux branches.
