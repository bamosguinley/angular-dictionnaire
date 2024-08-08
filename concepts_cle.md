## Guide des Concepts Clés en Angular

### Prérequis
1. Connaissances de base en JavaScript/TypeScript.
2. Angular CLI installé (`npm install -g @angular/cli`).
3. Node.js installé.

### Création d'un Projet Angular

Créez un nouveau projet Angular :

```sh
ng new angular-guide
cd angular-guide
```

### Les Input et Output

Les propriétés `@Input` et `@Output` permettent de passer des données entre les composants parents et enfants.

#### Exemple de `@Input`

**Composant enfant (`child.component.ts`) :**

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<p>{{ childMessage }}</p>`
})
export class ChildComponent {
  @Input() childMessage!: string;
}
```

**Composant parent (`parent.component.ts`) :**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <app-child [childMessage]="parentMessage"></app-child>
  `
})
export class ParentComponent {
  parentMessage = 'Message from parent';
}
```

#### Exemple de `@Output`

**Composant enfant (`child.component.ts`) :**

```typescript
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<button (click)="sendMessage()">Send Message</button>`
})
export class ChildComponent {
  @Output() messageEvent = new EventEmitter<string>();

  sendMessage() {
    this.messageEvent.emit('Message from child');
  }
}
```

**Composant parent (`parent.component.ts`) :**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <app-child (messageEvent)="receiveMessage($event)"></app-child>
    <p>{{ message }}</p>
  `
})
export class ParentComponent {
  message = '';

  receiveMessage($event: string) {
    this.message = $event;
  }
}
```

### Gestion des Formulaires

Angular propose deux façons principales de gérer les formulaires : les formulaires basés sur les templates et les formulaires réactifs.

#### Formulaires Basés sur les Templates

**Module (`app.module.ts`) :**

```typescript
import { FormsModule } from '@angular/forms';

@NgModule({
  imports: [
    // autres imports
    FormsModule
  ],
})
export class AppModule { }
```

**Composant (`template-form.component.ts`) :**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-template-form',
  template: `
    <form #userForm="ngForm" (ngSubmit)="onSubmit(userForm)">
      <label for="name">Name:</label>
      <input type="text" id="name" [(ngModel)]="user.name" name="name" required>
      
      <label for="email">Email:</label>
      <input type="email" id="email" [(ngModel)]="user.email" name="email" required>
      
      <button type="submit">Submit</button>
    </form>
  `
})
export class TemplateFormComponent {
  user = { name: '', email: '' };

  onSubmit(form: any) {
    console.log(form.value);
  }
}
```

#### Formulaires Réactifs

**Module (`app.module.ts`) :**

```typescript
import { ReactiveFormsModule } from '@angular/forms';

@NgModule({
  imports: [
    // autres imports
    ReactiveFormsModule
  ],
})
export class AppModule { }
```

**Composant (`reactive-form.component.ts`) :**

```typescript
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-reactive-form',
  template: `
    <form [formGroup]="userForm" (ngSubmit)="onSubmit()">
      <label for="name">Name:</label>
      <input type="text" id="name" formControlName="name">
      
      <label for="email">Email:</label>
      <input type="email" id="email" formControlName="email">
      
      <button type="submit">Submit</button>
    </form>
  `
})
export class ReactiveFormComponent implements OnInit {
  userForm!: FormGroup;

  constructor(private fb: FormBuilder) { }

  ngOnInit(): void {
    this.userForm = this.fb.group({
      name: ['', Validators.required],
      email: ['', [Validators.required, Validators.email]]
    });
  }

  onSubmit() {
    console.log(this.userForm.value);
  }
}
```

### Services et Injection de Dépendances

Les services en Angular sont utilisés pour encapsuler des logiques réutilisables, généralement pour interagir avec une API ou gérer des états partagés.

#### Création d'un Service

```sh
ng generate service services/data
```

**Service (`data.service.ts`) :**

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  private apiUrl = 'http://localhost:3000/data'; // URL de votre API

  constructor(private http: HttpClient) { }

  getData(): Observable<any> {
    return this.http.get(this.apiUrl);
  }

  postData(data: any): Observable<any> {
    return this.http.post(this.apiUrl, data);
  }
}
```

#### Utilisation d'un Service dans un Composant

**Composant (`data.component.ts`) :**

```typescript
import { Component, OnInit } from '@angular/core';
import { DataService } from '../../services/data.service';

@Component({
  selector: 'app-data',
  template: `
    <div *ngFor="let item of data">
      {{ item.name }}: {{ item.value }}
    </div>
    <button (click)="addData()">Add Data</button>
  `
})
export class DataComponent implements OnInit {
  data: any[] = [];

  constructor(private dataService: DataService) { }

  ngOnInit(): void {
    this.dataService.getData().subscribe(response => {
      this.data = response;
    });
  }

  addData() {
    const newData = { name: 'New Item', value: 'New Value' };
    this.dataService.postData(newData).subscribe(response => {
      this.data.push(response);
    });
  }
}
```

### Directives

Les directives sont des classes qui ajoutent un comportement supplémentaire aux éléments dans votre application Angular.

#### Directives Structurelles

**Exemple avec `*ngIf` :**

```html
<div *ngIf="isVisible">This is visible</div>
<button (click)="isVisible = !isVisible">Toggle Visibility</button>
```

**Exemple avec `*ngFor` :**

```html
<ul>
  <li *ngFor="let item of items">{{ item }}</li>
</ul>
```

#### Directives d'Attribut

Créez une directive personnalisée :

```sh
ng generate directive directives/highlight
```

**Directive (`highlight.directive.ts`) :**

```typescript
import { Directive, ElementRef, HostListener } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(private el: ElementRef) { }

  @HostListener('mouseenter') onMouseEnter() {
    this.highlight('yellow');
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.highlight(null);
  }

  private highlight(color: string | null) {
    this.el.nativeElement.style.backgroundColor = color;
  }
}
```

**Utilisation de la Directive :**

```html
<p appHighlight>Hover over me to see the highlight</p>
```

### Pipes

Les pipes sont utilisés pour transformer les données dans les templates Angular.

#### Utilisation des Pipes Intégrés

**Exemple avec `date` pipe :**

```html
<p>{{ currentDate | date:'fullDate' }}</p>
```

**Exemple avec `uppercase` pipe :**

```html
<p>{{ 'hello' | uppercase }}</p>
```

#### Création d'un Pipe Personnalisé

```sh
ng generate pipe pipes/custom
```

**Pipe (`custom.pipe.ts`) :**

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'custom'
})
export class CustomPipe implements PipeTransform {
  transform(value: string, ...args: unknown[]): string {
    return `Custom: ${value}`;
  }
}
```

**Utilisation du Pipe Personnalisé :**

```html
<p>{{ 'example' | custom }}</p>
```

### Routing

Le routing en Angular permet de naviguer entre différentes vues ou pages.

#### Configuration du Routing

**Module de Routage (`app-routing.module.ts`) :**

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './components/home/home.component';
import { AboutComponent } from './components/about/about.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'about', component: AboutComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

**Module Principal (`app.module.ts`) :**

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { HomeComponent } from './components/home/home.component';
import { AboutComponent } from './components/about/about.component';

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    AboutComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

**Composant Principal (`app.component.html`) :**

```html
<nav>
  <a routerLink="/">Home</a>
  <a routerLink="/about">About</a>
</nav>
<router-outlet></router-outlet>
```

### Services HTTP

Pour interagir avec une API backend, Angular utilise `HttpClient`.

#### Configuration du Module HTTP

**Module Principal (`app.module.ts`) :**

```typescript
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  imports: [
    // autres imports
    HttpClientModule
  ],
})
export class AppModule { }
```

#### Service HTTP

**Service (`data.service.ts`) :**

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  private apiUrl = 'http://localhost:3000/data'; // URL de votre API

  constructor(private http: HttpClient) { }

  getData(): Observable<any> {
    return this.http.get(this.apiUrl);
  }

  postData(data: any): Observable<any> {
    return this.http.post(this.apiUrl, data);
  }
}
```

#### Utilisation du Service HTTP

**Composant (`data.component.ts`) :**

```typescript
import { Component, OnInit } from '@angular/core';
import { DataService } from '../../services/data.service';

@Component({
  selector: 'app-data',
  template: `
    <div *ngFor="let item of data">
      {{ item.name }}: {{ item.value }}
    </div>
    <button (click)="addData()">Add Data</button>
  `
})
export class DataComponent implements OnInit {
  data: any[] = [];

  constructor(private dataService: DataService) { }

  ngOnInit(): void {
    this.dataService.getData().subscribe(response => {
      this.data = response;
    });
  }

  addData() {
    const newData = { name: 'New Item', value: 'New Value' };
    this.dataService.postData(newData).subscribe(response => {
      this.data.push(response);
    });
  }
}
```

### Gérer les Événements

Angular permet de gérer les événements en utilisant le binding d'événements.

#### Binding d'Événements

**Composant (`event.component.ts`) :**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-event',
  template: `
    <button (click)="onClick()">Click Me</button>
    <p>{{ message }}</p>
  `
})
export class EventComponent {
  message = '';

  onClick() {
    this.message = 'Button clicked!';
  }
}
```

### Cycle de Vie des Composants

Angular fournit plusieurs hooks de cycle de vie pour les composants.

#### Exemple de Hooks de Cycle de Vie

**Composant (`lifecycle.component.ts`) :**

```typescript
import { Component, OnInit, OnDestroy, AfterViewInit } from '@angular/core';

@Component({
  selector: 'app-lifecycle',
  template: `
    <p>Lifecycle component loaded</p>
  `
})
export class LifecycleComponent implements OnInit, OnDestroy, AfterViewInit {
  ngOnInit() {
    console.log('ngOnInit called');
  }

  ngAfterViewInit() {
    console.log('ngAfterViewInit called');
  }

  ngOnDestroy() {
    console.log('ngOnDestroy called');
  }
}
```

### Modules et Lazy Loading

Angular permet de diviser l'application en modules et de charger certains modules de manière paresseuse (lazy loading).

#### Création d'un Module

```sh
ng generate module features/feature
ng generate component features/feature/feature
```

#### Configuration de Lazy Loading

**Module de Routage Principal (`app-routing.module.ts`) :**

```typescript
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'about', component: AboutComponent },
  { path: 'feature', loadChildren: () => import('./features/feature/feature.module').then(m => m.FeatureModule) }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

**Module de Fonctionnalité (`feature-routing.module.ts`) :**

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { FeatureComponent } from './feature/feature.component';

const routes: Routes = [
  { path: '', component: FeatureComponent }
];

@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule]
})
export class FeatureRoutingModule { }
```

**Module de Fonctionnalité (`feature.module.ts`) :**

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FeatureRoutingModule } from './feature-routing.module';
import { FeatureComponent } from './feature/feature.component';

@NgModule({
  declarations: [FeatureComponent],
  imports: [
    CommonModule,
    FeatureRoutingModule
  ]
})
export class FeatureModule { }
```

### Conclusion

Ce guide a couvert les concepts suivants :

1. **Input et Output** pour la communication entre composants.
2. **Gestion des Formulaires** avec des formulaires basés sur les templates et réactifs.
3. **Services et Injection de Dépendances** pour encapsuler la logique réutilisable.
4. **Directives** pour ajouter des comportements supplémentaires aux éléments.
5. **Pipes** pour transformer les données dans les templates.
6. **Routing** pour naviguer entre différentes vues.
7. **Services HTTP** pour interagir avec une API backend.
8. **Gestion des Événements** pour réagir aux actions de l'utilisateur.
9. **Cycle de Vie des Composants** pour gérer les différentes phases de vie d'un composant.
10. **Modules et Lazy Loading** pour optimiser le chargement de l'application.

Avec ces concepts, vous devriez avoir une bonne base pour développer des applications Angular robustes et maintenables.
