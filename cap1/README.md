# Angular

Angular es un framework para construir aplicaciones en html y typescript orientado a componentes y modulos. Al ser un framework, Angular nos provee de todo lo necesario para construir una aplicacion, desde **modulos**, **componentes**, **directivas**, **validacion y creacion de formularios**, **animaciones**, **filtros**, **inyeccion de dependencias**, **manejo http**, **testing**, **e2e**, **cli** e integracion con **Ionic** o **NativeScript**.

 Una aplicacion angular se define por un conjunto de ngModules, una aplicacion al menos tiene un modulo raiz para su arranque.

 Los componentes trabajan con los ngModules para obtener el contexto para la compilacion de los metodos de los modulos externos.

Los componentes estan formados por codigo html y estilos css, y tambien por servicios que estos ultimos se pueden inyectar como dependencias.

Y a travez del ngModule Router podemos definir rutas y enlazar modulos o componentes a estas.

## Entonces diriamos que angular esta formado por

* Modules
* Components
* Templates, directives, and data binding
* Services and dependency injection
* Routing
  
---

![angular](./angular.png)

---

## Modules

Las aplicaciones en Angular son modulares y su sistema de modularizacion se llama ngModules. Los modulos son bloques para un dominio de aplicacion, un flujo de trabajo o un conjunto de funciones relacionadas. Desde un modulo podemos llamar a otros modulos, servicios, componentes o a otros archivos de codigo.

Todo aplicacion tiene su modulo raiz desde donde se iniciara la aplicacion, este modulo puede contener otros modulos y asi generar gerarquias anidadas de cualquier profundidad.

Los modulos se definen con el decorador **@ngModule**, es una funcion que toma un objeto de metadatos, cuyas propiedades describen el modulo.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

@NgModule({
  imports:      [ BrowserModule ],
  providers:    [ Logger ],
  declarations: [ AppComponent ],
  exports:      [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Components

Los componentes controlan las vistas del sistema, estos estan formados por una plantilla html, un archivo css y un archivo ts. Angular crea, actualiza y destruye los componentes a medida que el usuario se mueve en la aplicacion. Para controlar estos estados los hacemos a travez de su ciclo de vida del componente.

Los componentes se definen con el decorador **@Component** este decorador le indica donde obtener sus recursos para crear un componente.

```javascript
@Component({
  selector:    'app-hero-list',
  templateUrl: './hero-list.component.html',
  providers:  [ HeroService ]
})
export class HeroListComponent implements OnInit {
/* . . . */
}
```

A Travez de la plantilla del componente podemos usar la sintaxis de angular, usar directivas y aprovechar el data binding didireccional.

Data binding nos ayuda a coordinar las partes de la plantilla con la parte del componente.

---

![component](./component.png)

---

## Pipes

Las tuberías angulares le permiten declarar transformaciones de valor de visualización en su plantilla HTML. Una clase con el decorador @Pipe define una función que transforma los valores de entrada en valores de salida para mostrarlos en una vista.

```javascript
<!-- Default format: output 'Jun 15, 2015'-->
 <p>Today is {{today | date}}</p>

<!-- fullDate format: output 'Monday, June 15, 2015'-->
<p>The date is {{today | date:'fullDate'}}</p>

 <!-- shortTime format: output '9:43 AM'-->
 <p>The time is {{today | date:'shortTime'}}</p>
 ```

## Directivas

Las directivas tambien son componentes en angular pero estas son mas orientadas a la plantilla, existen 2 tipos de directivas **estructurales** y de **atributos**

### Estructurales

Las directivas estructurales modifican el diseño al agregar, eliminar y reemplazar elementos en el DOM.

```javascript
<li *ngFor="let hero of heroes"></li>
<app-hero-detail *ngIf="selectedHero"></app-hero-detail>
```

### Atributo

Las directivas de atributos alteran la apariencia o el comportamiento de un elemento existente. En las plantillas, se ven como atributos HTML normales, de ahí el nombre.

```javascript
<input [(ngModel)]="hero.name">
```

## Servicios e Inyeccion de dependencia

Un servicio es una clase que puede ser un dato o cualquier valor o una funcion. Literalmente es una clase con un solo proposito bien definido.

Angular nos provee de los servicios a travez de la inyeccion de dependencias, los servicios se pueden inyectar en un modulo o en un componente directamente a travez de la palabra reservada **provider**.

A travez de los servicios podemos obtener funcionalidades desde otras clases y poder importarlas desde un componente o modulo.

```javascript
// logger.service.ts
export class Logger {
  log(msg: any)   { console.log(msg); }
  error(msg: any) { console.error(msg); }
  warn(msg: any)  { console.warn(msg); }
}
```

```javascript
// hero.service.ts
export class HeroService {
  private heroes: Hero[] = [];

  constructor(
    private backend: BackendService,
    private logger: Logger) { }

  getHeroes() {
    this.backend.getAll(Hero).then( (heroes: Hero[]) => {
      this.logger.log(`Fetched ${heroes.length} heroes.`);
      this.heroes.push(...heroes); // fill cache
    });
    return this.heroes;
  }
}
```

### Inyeccion de dependencia

La inyeccion de dependencia se utiliza para proporcionar nuevos componentes con los servicios u otras cosas que se necesite.

Para definir una clase como un servicio en angular se utiliza el decorador **@Injectable**

Dentro de este decorador definiremos un provideIn haciendo que ese servicio este disponible en dicho modulo, si no se pone nada por defecto lo agrega al root

```javascript
@Injectable({
 providedIn: 'root',
})
```

Si quisieramos utilizar un servicio podriamos declararlo en el modulo o directamente en el component.

```javascript
@NgModule({
  providers: [
  BackendService,
  Logger
 ],
 ...
})
```

```javascript
@Component({
  selector:    'app-hero-list',
  templateUrl: './hero-list.component.html',
  providers:  [ HeroService ]
})
```

---

![injector](./injector.png)

---