## 9. Ressources et outils supplémentaires

---

### 9.1. Alias Git : Simplifier l'utilisation des commandes Git
Les alias Git permettent de raccourcir des commandes complexes ou souvent utilisées. Cela améliore la productivité en réduisant la saisie. Voici comment créer un alias pour une commande Git :
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
```
Ces alias permettent par exemple de taper `git st` au lieu de `git status`.

### 9.2. Utiliser Git avec un IDE (VSCode, IntelliJ, etc.)
La plupart des IDE modernes intègrent Git directement, ce qui facilite la gestion des commits, des branches et des fusions sans avoir à utiliser la ligne de commande. Voici quelques IDE populaires avec des intégrations Git :

- **VSCode** : Support Git natif dans la barre latérale avec visualisation des modifications, commits et branchements.
- **IntelliJ IDEA** : Intégration Git complète, y compris les outils de rebase, merge, et pull requests.
- **Eclipse** : Utilise le plugin EGit pour intégrer Git à l'IDE.
  
Utiliser Git dans un IDE vous permet de voir les changements en temps réel, de gérer visuellement les branches et de résoudre les conflits de manière plus intuitive.