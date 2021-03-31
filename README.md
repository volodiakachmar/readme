# Angular

### BEM fast start
- https://ru.bem.info/technologies/classic/project-stub/
- https://habr.com/ru/company/yandex/blog/276035/
- https://habr.com/ru/post/305548/
- https://habr.com/ru/post/203440/
- https://ru.bem.info/technologies/classic/project-stub/

### Angular folder structure 
- https://itnext.io/choosing-a-highly-scalable-folder-structure-in-angular-d987de65ec7

### Angular Upgrade to another Version
https://update.angular.io/?l=3&v=5.0-11.0

### Реактивные формы (Reactive Forms) в Angular + all I need to know about Forms + Validation + error messages
https://github.com/Maks-Zhitlov/angular-reactive-forms
https://medium.com/@maks.zhitlov/reactive-forms-in-angular-2f8abe884f79

### class-validator
https://github.com/typestack/class-validator
 
### Angular interview questions
https://github.com/sudheerj/angular-interview-questions#what-is-an-observer
 
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
- https://taiga-ui.dev/
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
- https://material.src.zone/components/card
- https://trimox.github.io/angular-mdc-web/#/angular-mdc-web/slider/examples

### HTML architecture for future projects
- https://github.com/apennell/she-templates#code-structure
- https://csslayout.io/patterns
- https://codepen.io/adriangyuricska/pen/bNXaBj
- https://css-tricks.com/snippets/css/css-grid-starter-layouts/
- https://codepen.io/codyhouse/pen/FdkEf
- https://colorlib.com/wp/css-layouts/
- https://developer.mozilla.org/ru/docs/Web/CSS/CSS_Grid_Layout/Realizing_common_layouts_using_CSS_Grid_Layout
- https://getbootstrap.com/docs/4.0/layout/grid/

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
 
- Маршрутизатор События роутера (Router Events)

```ts
import { ActivatedRoute, Router, Event } from '@angular/router';
...

export class UsersComponent implements OnInit {

constructor(private route: ActivatedRoute, private router: Router){
  this.route.queryParams.subscribe(params => console.log(params));
  this.route.data.subscribe(data => console.log(data));
  
  this.router.events.subscribe(events: Event) => {
   if(event instanceof NavigationStart) {
    console.log(events);
      }  
    }
  }
}
```

### RxJS
https://rxru.fun/#/api/operators/pipeable/zip

### NgRx
- [documentation](https://ngrx.io/guide/store/why)
- [article #1 ru](https://medium.com/ngx/angular-ngrx-%D1%8F%D1%81%D0%BD%D0%BE%D0%B5-%D0%B8-%D1%87%D1%91%D1%82%D0%BA%D0%BE%D0%B5-%D0%B2%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5-bdf1c97f44b2)
- https://tony-scialo.github.io/slides-ngrx/#/56
- [presentation #2 ru](https://docs.google.com/presentation/d/1MknPww1MdwzreFvDh086TzqaB5yyQga0PaoRR9bgCXs/edit#slide=id.g2fa7fd70ec_0_2288)


### Interesting repo on GitHub
- [Comprehensive Introduction to @ngrx/store](https://gist.github.com/btroncone/a6e4347326749f938510)
- [Authentication in Angular with NGRX](https://mherman.org/blog/authentication-in-angular-with-ngrx/)

### Angular Security
- [Angular.io Security Guide](https://angular.io/guide/security)

### Angular Auth with Auth()
- [Angular 2 authentication sample from auth0-blog](https://auth0.com/blog/complete-guide-to-angular-user-authentication/)

### Ready Components with Bit
[Bit platform with ready components](https://bit.dev/components)

### Angular for Mobile Dev
- [NativeScript](https://play.nativescript.org/)
- [Using NativeScript](https://www.syntaxsuccess.com/viewarticle/using-nativescript-with-angular-2.0)
- [angular-meteor](https://angular-meteor.com/tutorials/whatsapp2/ionic/setup)

### Angular with Babel
- [Babel](https://babeljs.io/)
- [A skeleton Angular 2 app built with Babel and Browserify](https://plnkr.co/edit/PxCzCu?p=preview&preview)
- [skeleton with Babel](https://github.com/shuhei/babel-angular2-app)

### Angular with TS
- [TS Doc](https://www.typescriptlang.org/)
- [TS playground](https://www.typescriptlang.org/play?#code)
- [Angular animation](https://jiayihu.github.io/ng-animate/)

### Udemy course and timelines 
   - Як працювати з формами(перевірка валідності і відносно цього блокувати інші елементи) --> 290 episode
   - Запрос до Firebase з фронту(логування реєстрація + токен і зразу перевіряє чи вже такий емейл існую) --> 291-294
