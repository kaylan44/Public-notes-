 ## Component d'auto-completion

> Implémentation de l'auto-completion via le module ng2-completer ( [GitHub - oferh/ng2-completer: Angular 2 autocomplete component](https://github.com/oferh/ng2-completer) ) 

1) Installation du module 
```bash 
npm install ng2-completer --save
```
2) Importation du module dans le fichier "app.module.ts" (ajout de FormsModule également)
```ts 
import { FormsModule } from "@angular/forms";
import { AppComponent } from './app.component';
import { Ng2CompleterModule } from "ng2-completer";

@NgModule({
  imports: [
      BrowserModule,
      Ng2CompleterModule,
      FormsModule,
  ],
  ```
3) Import du plugin dans le component

```ts 
import { CompleterService, CompleterData } from 'ng2-completer';

constructor(private completerService: CompleterService) {
  
}
```

4) Utilisation du component en HTML : (voir doc sur le gitHub pour connaitre les fonctionnalités disponibles via output & output)

```html
            <ng2-completer [textSearching]="'common.loading' | translate" 
                           [inputClass]="'form-control'" [(ngModel)]="searchStr"   
                           [placeholder]="'sivstop.stopPlaceHolder' | translate"
                           [datasource]="dataService" [minSearchLength]="3" 
                           (selected)="onStopPointSelect($event)">
            </ng2-completer>
```
5) Definition du dataService pour traiter les données : (possibilité d'utiliser des données stockées localement via "completerService.local" ou directement via une requète sur le serveur via "completerService.remote").
> Exemple avec données sur serveur :
```ts 
        this.dataService = this.completerService.remote(this.sivRestService.urlStopPoint, 'name,code', 'name,code');
```



> Extrait de la doc expliquant les paramètres du completerService.remote

##### Create remote data provider by calling `CompleterService.remote`.

#### Parameters

|Name|Type|Description|Required|
|:---|:---|:---       |:---    |
|url|string|Base url for the search|Yes|
|searchFields|string|Comma separated list of fields to search on. Fields may contain dots for nested attributes; if empty or null all data will be returned.|Yes|
|titleField|string|Name of the field to use as title for the list item.|Yes|

6) L'action à effectuer lorsqu'on sélectionne un élément est a définir via l'output "selected"
> HTML
```html 
(selected)="onStopPointSelect($event)"
```
>Typescript
```ts 
    public onStopPointSelect(item: any) {
        if (item !== null) {
            this.selectedItem = item.originalObject;
        } else {
            this.selectedItem = null;
        }

    }
```




## Bonus : 

Pour modifier le comportement du css, par exemple la classe completer-searching (crée des problèmes dans le front de btrust).

```css
:host /deep/ .completer-searching{
    color: black!important;
}
```
