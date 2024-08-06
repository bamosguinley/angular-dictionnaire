# Dictionnaire Angular

## Commandes Angular CLI

### `ng new`
- **Description**: Crée un nouveau projet Angular.
- **Usage**: `ng new project-name`
- **Options courantes**:
  - `--routing`: Ajoute un fichier de configuration de routage.
  - `--style=scss`: Utilise SCSS pour le styling.

### `ng serve`
- **Description**: Compile et lance une application Angular dans un serveur de développement.
- **Usage**: `ng serve`
- **Options courantes**:
  - `--port=4201`: Définit le port du serveur.
  - `--open`: Ouvre l'application dans le navigateur par défaut.

### `ng generate`
- **Description**: Génère des fichiers de code (composants, services, modules, etc.).
- **Usage**: `ng generate component component-name` ou `ng g c component-name`
- **Types courants**:
  - `ng g c`: Génère un composant.
  - `ng g s`: Génère un service.
  - `ng g m`: Génère un module.

### `ng build`
- **Description**: Compile l'application en un bundle pour la production.
- **Usage**: `ng build`
- **Options courantes**:
  - `--prod`: Compile en mode production.
  - `--output-path=dist/other-dir`: Définit le répertoire de sortie.

### `ng test`
- **Description**: Lance les tests unitaires.
- **Usage**: `ng test`
- **Options courantes**:
  - `--watch=false`: Lance les tests une seule fois.

### `ng e2e`
- **Description**: Lance les tests end-to-end (e2e).
- **Usage**: `ng e2e`
- **Options courantes**:
  - `--protractor-config=e2e/protractor.conf.js`: Utilise un fichier de configuration Protractor personnalisé.

### `ng add`
- **Description**: Ajoute des fonctionnalités à un projet Angular, comme des bibliothèques ou des frameworks.
- **Usage**: `ng add library-name`
- **Exemples**:
  - `ng add @angular/material`: Ajoute Angular Material.
  - `ng add @ngrx/store`: Ajoute NgRx Store.

### `ng update`
- **Description**: Met à jour les dépendances et les packages du projet Angular.
- **Usage**: `ng update`
- **Options courantes**:
  - `ng update @angular/cli @angular/core`: Met à jour Angular CLI et Core à la dernière version.

### `ng lint`
- **Description**: Analyse le code source pour les erreurs et les mauvaises pratiques.
- **Usage**: `ng lint`
- **Options courantes**:
  - `--fix`: Corrige automatiquement les erreurs corrigibles.

### `ng deploy`
- **Description**: Déploie l'application sur un service de hosting.
- **Usage**: `ng deploy`
- **Pré-requis**:
  - Une configuration spécifique pour le service de hosting, par exemple `@angular/fire` pour Firebase.

## Concepts de Base

### Composants (Components)
- **Description**: Les composants sont les blocs de construction de base d'une application Angular. Ils sont responsables de la gestion de la vue.
- **Fichiers**: `.component.ts`, `.component.html`, `.component.css`
- **Exemple de création**:
  ```bash
  ng generate component my-component
  ```

### Modules
- **Description**: Les modules regroupent des composants, des directives, des pipes et des services. Chaque application Angular possède au moins un module racine, généralement appelé `AppModule`.
- **Fichiers**: `.module.ts`
- **Exemple de création**:
  ```bash
  ng generate module my-module
  ```

### Directives
- **Description**: Les directives sont des classes qui ajoutent des comportements aux éléments dans vos applications Angular.
- **Types**:
  - **Attribute Directive**: Change l'apparence ou le comportement d'un élément.
  - **Structural Directive**: Change la structure du DOM (e.g., `*ngIf`, `*ngFor`).
- **Exemple de création**:
  ```bash
  ng generate directive my-directive
  ```

### Services
- **Description**: Les services sont utilisés pour partager des données et des fonctionnalités entre différentes parties de l'application.
- **Fichiers**: `.service.ts`
- **Exemple de création**:
  ```bash
  ng generate service my-service
  ```

### Pipes
- **Description**: Les pipes permettent de transformer les données dans les templates.
- **Usage**: `{{ data | pipeName }}`
- **Exemple de création**:
  ```bash
  ng generate pipe my-pipe
  ```

### Templates
- **Description**: Les templates définissent la vue pour un composant.
- **Fichiers**: `.component.html`
- **Exemple de template**:
  ```html
  <div>
    <h1>{{ title }}</h1>
    <p>{{ description }}</p>
  </div>
  ```

### Data Binding
- **Description**: Permet de lier les données entre le modèle et la vue.
- **Types**:
  - **Interpolation**: `{{ value }}`
  - **Property Binding**: `[property]="value"`
  - **Event Binding**: `(event)="handler($event)"`
  - **Two-way Binding**: `[(ngModel)]="value"`

## Concepts Avancés

### Routing
- **Description**: Angular Router permet la navigation entre les différentes vues ou composants de l'application.
- **Fichiers**: `app-routing.module.ts`
- **Usage**:
  ```typescript
  const routes: Routes = [
    { path: '', component: HomeComponent },
    { path: 'about', component: AboutComponent }
  ];
  ```

### Lazy Loading
- **Description**: Permet de charger les modules à la demande, réduisant ainsi le temps de chargement initial.
- **Usage**:
  ```typescript
  const routes: Routes = [
    { path: 'feature', loadChildren: () => import('./feature/feature.module').then(m => m.FeatureModule) }
  ];
  ```

### Guards
- **Description**: Les guards sont des services utilisés pour protéger les routes.
- **Types**:
  - `CanActivate`
  - `CanActivateChild`
  - `CanDeactivate`
  - `CanLoad`
- **Exemple de création**:
  ```bash
  ng generate guard my-guard
  ```

### Resolvers
- **Description**: Les resolvers récupèrent les données avant que la route ne soit activée.
- **Usage**:
  ```typescript
  const routes: Routes = [
    { path: 'detail/:id', component: DetailComponent, resolve: { data: DataResolver } }
  ];
  ```

### State Management
- **Description**: Gestion de l'état de l'application avec des bibliothèques comme NgRx.
- **Usage**:
  - **Store**: Contient l'état global de l'application.
  - **Actions**: Déclenchent des changements d'état.
  - **Reducers**: Gèrent les changements d'état.
  - **Effects**: Gèrent les effets secondaires.

### Dependency Injection
- **Description**: Mécanisme pour fournir des dépendances aux composants et services.
- **Usage**:
  ```typescript
  @Injectable({
    providedIn: 'root',
  })
  export class MyService {
    constructor(private http: HttpClient) {}
  }
  ```

### Forms
- **Description**: Angular propose deux approches pour les formulaires : les formulaires réactifs et les formulaires basés sur les templates.
- **Formulaires réactifs**:
  ```typescript
  this.form = this.fb.group({
    name: ['', Validators.required],
    email: ['', [Validators.required, Validators.email]]
  });
  ```
- **Formulaires basés sur les templates**:
  ```html
  <form #form="ngForm" (ngSubmit)="onSubmit(form)">
    <input name="name" ngModel required />
    <input name="email" ngModel email required />
    <button type="submit">Submit</button>
  </form>
  ```

### Interceptors
- **Description**: Les interceptors permettent d'intercepter et de manipuler les requêtes et réponses HTTP.
- **Exemple de création**:
  ```bash
  ng generate interceptor my-interceptor
  ```

## Autres Fonctionnalités

### Animations
- **Description**: Angular propose un module d'animations pour ajouter des transitions et des animations.
- **Fichiers**: `.component.ts` pour la logique des animations, `.component.html` pour les templates.
- **Exemple d'animation**:
  ```typescript
  import { trigger, state, style, transition, animate } from '@angular/animations';

  @Component({
    selector: 'app-my-component',
    templateUrl: './my-component.component.html',
    styleUrls: ['./my-component.component.css'],
    animations: [
      trigger('fadeInOut', [
        state('in', style({ opacity: 1 })),
        transition(':enter', [
          style({ opacity: 0 }),
          animate(300)
        ]),
        transition(':leave', [
          animate(300, style({ opacity: 

```markdown
          0 }))
        ])
      ])
    ]
  })
  export class MyComponent {}
  ```

### Custom Directives
- **Description**: Créer des directives personnalisées pour ajouter des comportements spécifiques aux éléments.
- **Exemple de création**:
  ```bash
  ng generate directive my-directive
  ```
- **Exemple d'utilisation**:
  ```typescript
  import { Directive, ElementRef, Renderer2 } from '@angular/core';

  @Directive({
    selector: '[appHighlight]'
  })
  export class HighlightDirective {
    constructor(el: ElementRef, renderer: Renderer2) {
      renderer.setStyle(el.nativeElement, 'backgroundColor', 'yellow');
    }
  }
  ```

### Internationalization (i18n)
- **Description**: Angular propose des outils pour internationaliser les applications.
- **Usage**:
  - Utiliser `@angular/localize` pour l'internationalisation.
  - Extraire les messages de traduction avec `ng extract-i18n`.
  - Utiliser les fichiers de traduction (e.g., `messages.fr.xlf`).

### Testing
- **Description**: Angular utilise des outils comme Jasmine et Karma pour les tests unitaires et Protractor pour les tests end-to-end.
- **Exemple de tests unitaires**:
  ```typescript
  import { TestBed, async } from '@angular/core/testing';
  import { AppComponent } from './app.component';

  describe('AppComponent', () => {
    beforeEach(async(() => {
      TestBed.configureTestingModule({
        declarations: [
          AppComponent
        ],
      }).compileComponents();
    }));

    it('should create the app', () => {
      const fixture = TestBed.createComponent(AppComponent);
      const app = fixture.componentInstance;
      expect(app).toBeTruthy();
    });
  });
  ```

### Service Workers
- **Description**: Angular supporte les Service Workers pour les applications progressives (PWA).
- **Usage**:
  - Ajouter `@angular/pwa` au projet avec `ng add @angular/pwa`.
  - Configurer le fichier `ngsw-config.json`.

### HttpClient
- **Description**: Module pour effectuer des requêtes HTTP.
- **Usage**:
  ```typescript
  import { HttpClient } from '@angular/common/http';

  @Injectable({
    providedIn: 'root'
  })
  export class DataService {
    constructor(private http: HttpClient) {}

    getData() {
      return this.http.get('https://api.example.com/data');
    }
  }
  ```

### Custom Pipes
- **Description**: Créer des pipes personnalisés pour transformer les données dans les templates.
- **Exemple de création**:
  ```bash
  ng generate pipe my-pipe
  ```
- **Exemple d'utilisation**:
  ```typescript
  import { Pipe, PipeTransform } from '@angular/core';

  @Pipe({
    name: 'customPipe'
  })
  export class CustomPipe implements PipeTransform {
    transform(value: string): string {
      return value.toUpperCase();
    }
  }
  ```

## Moins Utilisés

### Custom Schematics
- **Description**: Créer des schémas personnalisés pour automatiser les tâches avec Angular CLI.
- **Exemple de création**:
  - Suivre la documentation officielle d'Angular pour créer et utiliser des schémas personnalisés.

### SSR (Server-Side Rendering)
- **Description**: Utiliser Angular Universal pour le rendu côté serveur.
- **Usage**:
  - Ajouter `@nguniversal/express-engine` au projet avec `ng add @nguniversal/express-engine`.
  - Suivre les étapes de configuration pour activer le rendu côté serveur.

### Angular Elements
- **Description**: Créer des composants Angular réutilisables sous forme de Web Components.
- **Usage**:
  ```typescript
  import { createCustomElement } from '@angular/elements';
  import { Injector } from '@angular/core';
  import { MyComponent } from './my-component/my-component.component';

  const el = createCustomElement(MyComponent, { injector: this.injector });
  customElements.define('my-component', el);
  ```

### Angular Ivy
- **Description**: Ivy est le nouveau moteur de rendu d'Angular.
- **Usage**: Ivy est activé par défaut dans les versions récentes d'Angular.

### Schematics
- **Description**: Outils pour automatiser les tâches de développement.
- **Usage**: Utiliser `ng generate` pour créer des fichiers de code.

### Custom Builders
- **Description**: Créer des builders personnalisés pour Angular CLI.
- **Exemple de création**:
  - Suivre la documentation officielle d'Angular pour créer et utiliser des builders personnalisés.

### Angular CDK (Component Dev Kit)
- **Description**: Fournit des outils pour développer des composants Angular.
- **Usage**: Importer des modules spécifiques du CDK comme `DragDropModule`, `OverlayModule`, etc.
- **Exemple d'utilisation**:
  ```typescript
  import { DragDropModule } from '@angular/cdk/drag-drop';

  @NgModule({
    imports: [
      DragDropModule
    ],
  })
  export class AppModule {}
  ```

---

Ce guide devrait couvrir la plupart des besoins et répondre à de nombreuses questions que vous pourriez avoir en travaillant avec Angular. Pour des détails supplémentaires, reportez-vous toujours à la documentation officielle d'Angular.

