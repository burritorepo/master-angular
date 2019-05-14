# Components & Templates

Un componente en Angular esta formado por un archivo html, un archivo de estilos y un archivo de js(ts).

A travez de la interpolacion podemos agregar variables, llamar a funciones, hacer calculos desde la plantilla html.

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <h1>{{title}}</h1>
    <h2>My favorite hero is: {{myHero}}</h2>
  `
})
export class AppComponent {
  title = 'Tour of Heroes';
  myHero = 'Windstorm';
}
```

## *ngFor

Para mostrar una lista de elementos podemos usar ngFor, esto es una directiva iterador.

```javascript
export class AppComponent {
  title = 'Tour of Heroes';
  heroes = ['Windstorm', 'Bombasto', 'Magneta', 'Tornado'];
  myHero = this.heroes[0];
}
```

```javascript
template: `
  <h1>{{title}}</h1>
  <h2>My favorite hero is: {{myHero}}</h2>
  <p>Heroes:</p>
  <ul>
    <li *ngFor="let hero of heroes">
      {{ hero }}
    </li>
  </ul>
`
```

## *ngIf

*ngIf Se comporta tal cual un if de javascript

```javascript
<p *ngIf="heroes.length > 3">There are many heroes!</p>
```

## Variables de plantilla

A travez de las variables de plantilla podemos tener acceso al elemento con este identificador

```html
<label>Type something:
  <input #customerInput>{{customerInput.value}}
</label>
```