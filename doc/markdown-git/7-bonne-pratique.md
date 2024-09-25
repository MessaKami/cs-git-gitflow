---

## 7.1. Rédiger des messages de commit clairs

Rédiger des messages de commit clairs est crucial pour maintenir un historique Git lisible et utile pour toute l'équipe. Voici quelques bonnes pratiques à suivre pour écrire des messages de commit efficaces :

### 1. **Utilisez l'impératif pour le titre du commit**
Le titre doit être court (50 caractères maximum) et formulé à l'impératif. Cela décrit ce que fait le commit, pas ce qu'il a fait. Par exemple :
- ✅ `Fix login issue`
- ✅ `Add user authentication`
- ❌ `Fixed login issue`
- ❌ `Adding user authentication`

### 2. **Utilisez des préfixes pour indiquer le type de modification**
Pour améliorer la lisibilité et standardiser les messages de commit, utilisez les préfixes suivants :
- **`feat:`** (nouvelle fonctionnalité pour l'utilisateur, pas une fonctionnalité liée au build script)  
  Exemple : `feat: Add user registration feature`
  
- **`fix:`** (correction de bug pour l'utilisateur, pas un correctif pour le build script)  
  Exemple : `fix: Resolve issue with form validation`

- **`docs:`** (modifications apportées à la documentation)  
  Exemple : `docs: Update installation guide in README`

- **`style:`** (formatage, points-virgules manquants, etc. ; pas de changement dans le code de production)  
  Exemple : `style: Fix indentation and remove extra spaces`

- **`refactor:`** (refactorisation du code de production, ex. renommer une variable)  
  Exemple : `refactor: Rename 'userData' to 'userProfile' for clarity`

- **`test:`** (ajout de tests manquants ou refactorisation des tests ; pas de changement dans le code de production)  
  Exemple : `test: Add unit tests for login functionality`

- **`chore:`** (mise à jour de tâches de build, de configurations, etc. ; pas de changement dans le code de production)  
  Exemple : `chore: Update Grunt tasks for build process`

### 3. **Soyez concis, mais descriptif**
Le titre doit suffire à comprendre l'objectif du commit sans avoir à lire les détails du code. Un bon message de commit doit donner une idée immédiate de ce qui a changé.

### 4. **Ajoutez une description si nécessaire**
Pour les changements plus complexes, ajoutez une description sous le titre. Séparez le titre et la description par une ligne vide. La description doit expliquer pourquoi le changement a été effectué, quels problèmes il résout, ou toute autre information importante.
Exemple :
```plaintext
feat: Add validation for email input

This ensures that users cannot submit the form without a valid email address, which reduces errors and improves data quality.
```

### 5. **Mentionnez les issues ou tickets**
Si le commit est lié à une issue ou un ticket, mentionnez-le dans le message avec un lien ou une référence. Cela permet de retracer facilement les changements liés à une tâche ou à un bug précis.
Exemple :
```plaintext
fix: Resolve broken image link in the homepage

Resolves #123
```

### 6. **Commits atomiques**
Un commit doit être atomique, c'est-à-dire qu'il doit représenter une seule modification ou un ensemble de changements cohérents et relatifs à une seule tâche. N'essayez pas de faire plusieurs choses dans un seul commit.

### 7. **Exemples de bons messages de commit**
- `feat: Refactor user authentication logic`
- `docs: Update README with installation instructions`
- `fix: Correct typo in settings page`
- `style: Improve formatting in search function`
- `test: Add unit tests for payment gateway`
- `chore: Update npm dependencies`

---

Cette section avec les préfixes normalisés aidera à maintenir une meilleure structure dans l'historique des commits, facilitant ainsi la navigation et la compréhension des changements.