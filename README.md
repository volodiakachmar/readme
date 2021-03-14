# Angular

### BEM fast start
- https://ru.bem.info/technologies/classic/project-stub/
- https://habr.com/ru/company/yandex/blog/276035/
- https://habr.com/ru/post/305548/
- https://habr.com/ru/post/203440/
- https://ru.bem.info/technologies/classic/project-stub/


### Реактивные формы (Reactive Forms) в Angular

https://medium.com/@maks.zhitlov/reactive-forms-in-angular-2f8abe884f79

### class-validator
https://github.com/typestack/class-validator
 
### Шпаргалка
 https://angular.io/guide/cheatsheet

### Как я структурирую CSS
 https://habr.com/ru/post/523884/

### BEM CSS
https://habr.com/ru/company/yandex/blog/276035/

### Common names for div classes
https://github.com/yoksel/common-words/blob/master/README.md

### Visual Code Plugins to install as Angular dev
  - Angular Essentials
  - Darcula
  - Material Icon theme
  - TSlint
  - AutoImport
  - angular2-snippets

### Form validation library
https://formvalidation.io/
  
### Angular Material UI Framework
https://material.angular.io/components/categories

### Other UI Frameworks for Angular
- https://www.ag-grid.com/
- https://clarity.design/core-components/search/
- https://ng-bootstrap.github.io/#/components/tooltip/examples
- https://valor-software.com/ngx-bootstrap/#/
- https://onsen.io/theme-roller/
- https://ng-lightning.github.io/ng-lightning/
- https://demos.telerik.com/kendo-ui/bar-charts/index
- https://ng-semantic.herokuapp.com/#/elements/search
- https://www.infragistics.com/
- https://vaadin.com/comparison
- https://primefaces.org/primeng/showcase/#/colorpicker

### HTML architecture for future projects
- https://github.com/apennell/she-templates#code-structure
- https://csslayout.io/patterns
- https://codepen.io/adriangyuricska/pen/bNXaBj
- https://css-tricks.com/snippets/css/css-grid-starter-layouts/
- https://codepen.io/codyhouse/pen/FdkEf
- https://colorlib.com/wp/css-layouts/

### JS
- top js function I can use in work
  https://1loc.dev/
- how to manage HTML DOM with vanilla JavaScript only? https://htmldom.dev/
- Fake credit card numbers library https://fakenumbers.io/

### CSS
https://github.com/yoksel/common-words/blob/master/README.md

### RxJS
- https://academind.com/tutorials/understanding-rxjs/

### READY SNIPPETS FOR ANGULAR+TS
- як на клік змінювати колір тексту + взаємодія з вибраними клівішами клавіатури

#### HTML
```html
<p (click)="changeColor('blue')" [style.color]="mycolor">
 It is working
</p>

<input type="text" (input)="changeColor($event.target.value)"
(keydown.control.shift.enter)="changeColor('green')">
```
#### TS

```ts
changeColor(color){
  this.mycolor = color;
}
```

- Передача даних в компонент за допомогою Input()
Існує для передачі інформації з дочерного компоненту до головного або навпаки. В компоненті з якого хочемо
відпривати інформацію ми пишемо квадратні дужки і всередині назва атрибуту який ми імплементуємо в компоненті в якому 
хочему цю інформацію отримати за допомогою атрибуту Input(). В кінці ми передаємо з компоненту з [] = "тут буде переменна
для передачі в інший компонент".

- Как передвати дані із компоненту або як передавати подію яка сталась в дочерному компоненті так щоб
 про неї дізнався головний компонент / Output()

https://www.youtube.com/watch?v=OKhYwdAzn5k&list=PLDyvV36pndZF-vwsVB48ivZyNJ4ETBKNY&index=8

- Directives

```
ng g d  // to create directive
```

- Inteceptors
Звичайний сервіс який обробляє запроси на сервер і з серверу.

HttpClient -> Interceptors -> API
HttpClient <- Interceptors <- API

#### interceptor.service.ts

```ts
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs/Observable';
import 'rxjs/add/operator/catch';
import 'rxjs/add/observable/throw';


@Injectable()
export class MyInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
   const request = req.clone({params: req.params.set('x','5')});
   return next.handle(request).catch( error => {
       if(error.status === 401) {
         console.log('Redirect tp login')
      }
      return Observable.throw(error);
    });
  }
}
```

#### app.component.ts

```ts
import { Component } from '@angular/core';
import { HttpClient } from '@angular/common/http';

...

export class AppComponent {
constructor(_http: HttpClient){
   _http.get('https://api.github.com/search/users').subscribe(results => {
     console.log(results);
   })
  }
}
```
- Routing

#### app.component.html

```html
<a routerLink="" routerLinkActive="active" [routerLinkActiveOptions]="{exact: true}">Home</a> <!-- active is a СSS class -->
<a routerLink="users" routerLinkActive="active">Users</a>
<a routerLink="users" [queryParams]="{q: notFound}" routerLinkActive="active">New</a>  
```


#### app.module.ts

```ts
const routes = [
{ path: '', component: HomeComponent },
{ path: 'users', component: UsersComponent },
{ path: 'user/:userId', component: UsersComponent }
];

@NgModule({
declarations: [],
imports: [
BrowserModule,
RouterModule.forRooot(routes)
]

})
```

#### home.component.ts

```ts
...
export class HomeComponent implements OnInit {

constructor(private _router:Router, private _route: ActivatedRoute){  }

ngOnInit(){  }

goToUser(userId) {
this._route.navigate('users, userId', {skipLocationChange: true, relativeTo: this._route})
 .then(_ => {

  });
}

```  

#### home.component.html

```html
...
<button click="goToUser(someParam)"></button>
```  

### Udemy course and timelines 
   - Як працювати з формами(перевірка валідності і відносно цього блокувати інші елементи) --> 290 episode
   - Запрос до Firebase з фронту(логування реєстрація + токен і зразу перевіряє чи вже такий емейл існую) --> 291-294
