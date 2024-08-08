## Guide Complet CRUD avec Angular

### Prérequis
1. Connaissances de base en JavaScript/TypeScript.
2. Angular CLI installé (`npm install -g @angular/cli`).
3. Node.js installé.

### Création d'un Projet Angular

Commencez par créer un nouveau projet Angular :

```sh
ng new angular-crud
cd angular-crud
```

### Création des Composants

Créez les composants nécessaires pour les opérations CRUD :

```sh
ng generate component components/create
ng generate component components/read
ng generate component components/update
ng generate component components/delete
```

### Configuration du Service pour les Opérations CRUD

Créez un service pour gérer les opérations CRUD :

```sh
ng generate service services/crud
```

Modifiez le fichier `crud.service.ts` pour inclure les méthodes CRUD :

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class CrudService {
  private apiUrl = 'http://localhost:3000/items'; // URL de votre API

  constructor(private http: HttpClient) { }

  getItems(): Observable<any> {
    return this.http.get(this.apiUrl);
  }

  getItem(id: number): Observable<any> {
    return this.http.get(`${this.apiUrl}/${id}`);
  }

  createItem(item: any): Observable<any> {
    return this.http.post(this.apiUrl, item);
  }

  updateItem(id: number, item: any): Observable<any> {
    return this.http.put(`${this.apiUrl}/${id}`, item);
  }

  deleteItem(id: number): Observable<any> {
    return this.http.delete(`${this.apiUrl}/${id}`);
  }
}
```

### Configuration du Module HTTP

Assurez-vous que le module HTTP est importé dans `app.module.ts` :

```typescript
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  declarations: [
    // composants
  ],
  imports: [
    // autres imports
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### Création de l'Interface de l'Item

Créez un fichier `item.ts` pour définir l'interface de l'item :

```typescript
export interface Item {
  id: number;
  name: string;
  description: string;
}
```

### Implémentation des Composants

#### Composant Create

Modifiez `create.component.ts` pour inclure le formulaire de création :

```typescript
import { Component } from '@angular/core';
import { CrudService } from '../../services/crud.service';
import { Item } from '../../item';

@Component({
  selector: 'app-create',
  templateUrl: './create.component.html',
  styleUrls: ['./create.component.css']
})
export class CreateComponent {
  item: Item = { id: 0, name: '', description: '' };

  constructor(private crudService: CrudService) { }

  createItem(): void {
    this.crudService.createItem(this.item).subscribe(response => {
      console.log('Item créé', response);
    });
  }
}
```

Et le fichier `create.component.html` :

```html
<h2>Créer un nouvel item</h2>
<form (ngSubmit)="createItem()">
  <label for="name">Nom:</label>
  <input type="text" id="name" [(ngModel)]="item.name" name="name" required>

  <label for="description">Description:</label>
  <input type="text" id="description" [(ngModel)]="item.description" name="description" required>

  <button type="submit">Créer</button>
</form>
```

Assurez-vous d'importer les modules de formulaire nécessaires dans `app.module.ts` :

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

#### Composant Read

Modifiez `read.component.ts` pour afficher la liste des items :

```typescript
import { Component, OnInit } from '@angular/core';
import { CrudService } from '../../services/crud.service';
import { Item } from '../../item';

@Component({
  selector: 'app-read',
  templateUrl: './read.component.html',
  styleUrls: ['./read.component.css']
})
export class ReadComponent implements OnInit {
  items: Item[] = [];

  constructor(private crudService: CrudService) { }

  ngOnInit(): void {
    this.crudService.getItems().subscribe(data => {
      this.items = data;
    });
  }
}
```

Et le fichier `read.component.html` :

```html
<h2>Liste des items</h2>
<ul>
  <li *ngFor="let item of items">
    {{ item.name }}: {{ item.description }}
  </li>
</ul>
```

#### Composant Update

Modifiez `update.component.ts` pour inclure le formulaire de mise à jour :

```typescript
import { Component, OnInit } from '@angular/core';
import { CrudService } from '../../services/crud.service';
import { Item } from '../../item';
import { ActivatedRoute, Router } from '@angular/router';

@Component({
  selector: 'app-update',
  templateUrl: './update.component.html',
  styleUrls: ['./update.component.css']
})
export class UpdateComponent implements OnInit {
  item: Item = { id: 0, name: '', description: '' };

  constructor(
    private crudService: CrudService,
    private route: ActivatedRoute,
    private router: Router
  ) { }

  ngOnInit(): void {
    const id = +this.route.snapshot.paramMap.get('id')!;
    this.crudService.getItem(id).subscribe(data => {
      this.item = data;
    });
  }

  updateItem(): void {
    this.crudService.updateItem(this.item.id, this.item).subscribe(response => {
      console.log('Item mis à jour', response);
      this.router.navigate(['/read']);
    });
  }
}
```

Et le fichier `update.component.html` :

```html
<h2>Mettre à jour l'item</h2>
<form (ngSubmit)="updateItem()">
  <label for="name">Nom:</label>
  <input type="text" id="name" [(ngModel)]="item.name" name="name" required>

  <label for="description">Description:</label>
  <input type="text" id="description" [(ngModel)]="item.description" name="description" required>

  <button type="submit">Mettre à jour</button>
</form>
```

#### Composant Delete

Modifiez `delete.component.ts` pour inclure la suppression d'un item :

```typescript
import { Component, OnInit } from '@angular/core';
import { CrudService } from '../../services/crud.service';
import { Item } from '../../item';

@Component({
  selector: 'app-delete',
  templateUrl: './delete.component.html',
  styleUrls: ['./delete.component.css']
})
export class DeleteComponent implements OnInit {
  items: Item[] = [];

  constructor(private crudService: CrudService) { }

  ngOnInit(): void {
    this.crudService.getItems().subscribe(data => {
      this.items = data;
    });
  }

  deleteItem(id: number): void {
    this.crudService.deleteItem(id).subscribe(response => {
      console.log('Item supprimé', response);
      this.items = this.items.filter(item => item.id !== id);
    });
  }
}
```

Et le fichier `delete.component.html` :

```html
<h2>Supprimer un item</h2>
<ul>
  <li *ngFor="let item of items">
    {{ item.name }}: {{ item.description }}
    <button (click)="deleteItem(item.id)">Supprimer</button>
  </li>
</ul>
```

### Configuration du Routage

Ajoutez les routes nécessaires dans `app-routing.module.ts` :

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { CreateComponent } from './components/create/create.component';
import { ReadComponent } from './components/read/read.component';
import { UpdateComponent } from './components/update/update.component';
import { DeleteComponent } from './components/delete/delete.component';

const routes: Routes = [
  { path: 'create', component: CreateComponent },
  { path: 'read', component: ReadComponent },
  { path: 'update/:id', component: UpdateComponent },
  { path: 'delete', component: DeleteComponent },
  { path: '', redirectTo: '/read', pathMatch: 'full' }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

### Résumé

Ce guide vous a montré comment créer une application CRUD complète avec Angular en utilisant les concepts suivants :

1. **Création d'un projet Angular** avec Angular CLI.
2. **Création de composants** pour chaque opération CRUD (Create, Read, Update, Delete).
3. **Création d'un service CRUD** pour communiquer avec une API backend.
4. **Configuration du module HTTP** pour permettre les requêtes HTTP.
5. **Définition de l'interface Item** pour représenter les données.
6. **Implémentation des composants** pour gérer les opérations CRUD.
7.
