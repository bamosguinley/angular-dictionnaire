### Installation de l'Angular CLI

1. **Installation de l'Angular CLI :**

```sh
npm install -g @angular/cli
```
   - **Rôle :** Installe l'outil de ligne de commande Angular globalement sur votre système.

### Commandes de Création

2. **Créer un nouveau projet :**

```sh
ng new <project-name>
```
   - **Rôle :** Crée un nouveau projet Angular avec une structure de dossiers et des fichiers de configuration par défaut.

3. **Générer un composant :**

```sh
ng generate component <component-name>
# ou
ng g c <component-name>
```
   - **Rôle :** Crée un nouveau composant Angular, y compris les fichiers `.ts`, `.html`, `.css`, et `.spec.ts`.

4. **Générer un service :**

```sh
ng generate service <service-name>
# ou
ng g s <service-name>
```
   - **Rôle :** Crée un nouveau service Angular, qui est une classe injectable utilisée pour encapsuler la logique métier.

5. **Générer un module :**

```sh
ng generate module <module-name>
# ou
ng g m <module-name>
```
   - **Rôle :** Crée un nouveau module Angular, qui permet de regrouper des composants, des directives, des pipes et des services.

6. **Générer une directive :**

```sh
ng generate directive <directive-name>
# ou
ng g d <directive-name>
```
   - **Rôle :** Crée une nouvelle directive Angular, qui ajoute un comportement personnalisé aux éléments DOM.

7. **Générer un pipe :**

```sh
ng generate pipe <pipe-name>
# ou
ng g p <pipe-name>
```
   - **Rôle :** Crée un nouveau pipe Angular, utilisé pour transformer les données dans les templates.

8. **Générer un guard :**

```sh
ng generate guard <guard-name>
# ou
ng g g <guard-name>
```
   - **Rôle :** Crée un nouveau guard Angular, utilisé pour gérer les routes et contrôler l'accès aux différentes parties de l'application.

9. **Générer une interface :**

```sh
ng generate interface <interface-name>
# ou
ng g i <interface-name>
```
   - **Rôle :** Crée une nouvelle interface TypeScript, utilisée pour définir des contrats pour les objets.

10. **Générer une classe :**

```sh
ng generate class <class-name>
# ou
ng g cl <class-name>
```
   - **Rôle :** Crée une nouvelle classe TypeScript, utilisée pour encapsuler la logique métier.

11. **Générer une enum :**

```sh
ng generate enum <enum-name>
# ou
ng g e <enum-name>
```
   - **Rôle :** Crée une nouvelle énumération TypeScript, utilisée pour définir un ensemble de valeurs nommées.

12. **Générer une bibliothèque :**

```sh
ng generate library <library-name>
# ou
ng g lib <library-name>
```
   - **Rôle :** Crée une nouvelle bibliothèque Angular, utilisée pour partager du code réutilisable entre plusieurs applications.

### Commandes de Développement

13. **Servir l'application :**

```sh
ng serve
# ou
ng s
```
   - **Rôle :** Compile l'application et démarre un serveur de développement local avec rechargement automatique.

14. **Servir l'application avec un port spécifique :**

```sh
ng serve --port <port-number>
# ou
ng s --port <port-number>
```
   - **Rôle :** Démarre le serveur de développement sur un port spécifié.

15. **Servir l'application avec une configuration spécifique :**

```sh
ng serve --configuration=<configuration>
# ou
ng s --configuration=<configuration>
```
   - **Rôle :** Utilise une configuration spécifique définie dans le fichier `angular.json` pour servir l'application.

### Commandes de Build

16. **Compiler l'application :**

```sh
ng build
# ou
ng b
```
   - **Rôle :** Compile l'application et génère les fichiers de sortie dans le dossier `dist`.

17. **Compiler l'application pour production :**

```sh
ng build --prod
# ou
ng b --prod
```
   - **Rôle :** Compile l'application avec les optimisations de production, comme la minification et le tree shaking.

18. **Compiler l'application avec une configuration spécifique :**

```sh
ng build --configuration=<configuration>
# ou
ng b --configuration=<configuration>
```
   - **Rôle :** Utilise une configuration spécifique définie dans le fichier `angular.json` pour compiler l'application.

19. **Compiler l'application et regarder les changements :**

```sh
ng build --watch
# ou
ng b --watch
```
   - **Rôle :** Compile l'application et surveille les modifications pour recompiler automatiquement.

### Commandes de Test

20. **Exécuter les tests unitaires :**

```sh
ng test
# ou
ng t
```
   - **Rôle :** Exécute les tests unitaires définis avec Jasmine et Karma.

21. **Exécuter les tests unitaires avec une couverture de code :**

```sh
ng test --code-coverage
# ou
ng t --code-coverage
```
   - **Rôle :** Exécute les tests unitaires et génère un rapport de couverture de code.

22. **Exécuter les tests de bout en bout :**

```sh
ng e2e
```
   - **Rôle :** Exécute les tests de bout en bout définis avec Protractor.

### Commandes de Configuration

23. **Afficher la version Angular CLI :**

```sh
ng version
# ou
ng v
```
   - **Rôle :** Affiche la version de l'Angular CLI et d'autres dépendances Angular.

24. **Afficher la configuration Angular CLI :**

```sh
ng config
```
   - **Rôle :** Affiche ou modifie la configuration Angular CLI.

25. **Mettre à jour Angular CLI et les dépendances :**

```sh
ng update
```
   - **Rôle :** Met à jour Angular CLI et ses dépendances.

26. **Mettre à jour Angular CLI et Angular Core à la dernière version :**

```sh
ng update @angular/cli @angular/core
```
   - **Rôle :** Met à jour Angular CLI et Angular Core à la dernière version stable.

### Commandes de Déploiement

27. **Déployer sur GitHub Pages :**

```sh
ng deploy --repo=<repository-url>
```
   - **Rôle :** Déploie l'application sur GitHub Pages.

### Commandes Diverses

28. **Analyser les dépendances :**

```sh
ng analyze
```
   - **Rôle :** Analyse les dépendances et suggère des optimisations.

29. **Linter le projet :**

```sh
ng lint
```
   - **Rôle :** Analyse le code source pour détecter et corriger les problèmes de style et de syntaxe.

30. **Formatage du code avec Prettier (si configuré) :**

```sh
ng format
```
   - **Rôle :** Formate le code source selon les règles définies par Prettier.

### Commandes Avancées

31. **Extraire les messages d'internationalisation :**

```sh
ng xi18n
```
   - **Rôle :** Extrait les messages d'internationalisation de l'application pour la traduction.

32. **Exécuter une commande en mode expérimental :**

```sh
ng <command> --experimental
```
   - **Rôle :** Exécute une commande en mode expérimental pour tester de nouvelles fonctionnalités.

33. **Générer un schéma :**

```sh
ng generate schematic <schematic-name>
```
   - **Rôle :** Crée un nouveau schéma personnalisé pour Angular CLI.

34. **Développer une application de laboratoire :**

```sh
ng generate app <app-name>
# ou
ng g app <app-name>
```
   - **Rôle :** Crée une nouvelle application de laboratoire pour tester des concepts.

35. **Ajouter une bibliothèque à un projet existant :**

```sh
ng add <library-name>
```
   - **Rôle :** Ajoute une bibliothèque ou un outil tiers à un projet Angular existant.

### Commandes d'Administration

36. **Configurer l'environnement :**

```sh
ng config --global <key> <value>
```
   - **Rôle :** Modifie la configuration globale de l'Angular CLI.

37. **Afficher les logs :**

```sh
ng log
```
   - **Rôle :** Affiche les journaux de l'Angular CLI pour le dépannage.

### Commandes de Mise à Niveau

38. **Migrer un projet Angular vers la dernière version :**

```sh
ng update @angular/core @angular/cli
```
   - **Rôle :** Met à jour un projet Angular existant vers la dernière version.

### Commandes de Débogage

39. **Exécuter l'application avec un profil de débogage :**

```sh
ng serve --source-map
# ou
ng s --source-map
```
   - **Rôle :** Démarre l'application en mode développement avec les sourcemaps activés, ce qui facilite le débogage du code source dans le navigateur.

### Commandes de Performances

40. **Analyser les performances :**

```sh
ng build --stats-json
# Puis analyser avec un outil tiers comme webpack-bundle-analyzer
```
   - **Rôle :** Génère un fichier JSON contenant les statistiques de build, qui peut être analysé avec des outils tiers pour identifier les points à améliorer.

### Commandes Complémentaires

41. **Démarrer une application générée automatiquement :**

```sh
ng run <project>:<target>[:configuration]
```
   - **Rôle :** Exécute une cible spécifiée (comme build, test, lint, etc.) pour un projet.

42. **Ajouter un schéma personnalisé :**

```sh
ng add @angular/pwa
```
   - **Rôle :** Ajoute un schéma personnalisé à un projet Angular existant, comme la configuration pour les Progressive Web Apps (PWA).

43. **Configurer un proxy pour le développement :**

```sh
ng serve --proxy-config proxy.conf.json
```
   - **Rôle :** Utilise un fichier de configuration de proxy pour rediriger les appels API pendant le développement.

44. **Effectuer une migration spécifique :**

```sh
ng update @angular/core --migrate-only --from=<version> --to=<version>
```
   - **Rôle :** Effectue uniquement les migrations de version sans mettre à jour les packages.

45. **Exécuter une commande custom :**

```sh
ng e2e --protractor-config=protractor.custom.conf.js
```
   - **Rôle :** Exécute les tests de bout en bout avec une configuration personnalisée.

46. **Créer un service worker :**

```sh
ng add @angular/service-worker
```
   - **Rôle :** Ajoute et configure un service worker pour l'application afin de permettre la mise en cache et le fonctionnement hors ligne.

47. **Mettre à jour le schéma de l'application :**

```sh
ng update @schematics/angular
```
   - **Rôle :** Met à jour les schémas utilisés pour la génération de code Angular.

48. **Affichage d'aide pour une commande spécifique :**

```sh
ng help <command>
```
   - **Rôle :** Affiche l'aide détaillée pour une commande spécifique de l'Angular CLI.

49. **Configurer le proxy de l'API pour le développement local :**

```sh
ng serve --proxy-config proxy.conf.json
```
   - **Rôle :** Utilise un fichier `proxy.conf.json` pour rediriger les requêtes API vers un serveur backend lors du développement local.

50. **Analyser les dépendances d'un projet Angular :**

```sh
ng analytics
```
   - **Rôle :** Affiche ou modifie les paramètres d'analyse d'utilisation de l'Angular CLI.

### Commandes de Maintenance

51. **Nettoyer le cache Angular :**

```sh
ng cache clean
```
   - **Rôle :** Nettoie le cache des packages npm utilisés par Angular CLI.

52. **Analyser les paquets de votre projet :**

```sh
ng analytics
```
   - **Rôle :** Fournit des informations sur l'utilisation des paquets et permet de configurer la collecte des données d'analyse.

53. **Configurer l'utilisation des services de l'Angular CLI :**

```sh
ng analytics enable/disable
```
   - **Rôle :** Active ou désactive la collecte des données d'utilisation de l'Angular CLI.

Avec ce dictionnaire des commandes Angular CLI, vous disposez d'une vue d'ensemble complète des outils et des fonctionnalités disponibles pour créer, développer, tester, et déployer des applications Angular.
