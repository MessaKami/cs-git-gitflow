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
