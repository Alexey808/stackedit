[https://habr.com/ru/company/ruvds/blog/476956/](https://habr.com/ru/company/ruvds/blog/476956/)



# Заголовок 1 уровня
## Заголовок 2 уровня
### Заголовок 3 уровня
**жирное начертание**
__жирное начерт__
_наклонное начертание_
```html
подсветка синтаксиса HTML
```

```css
подсветка синтаксиса css
```

**Принудительный ререндер | #markDirty**  
Возможно ререндер идёт с корня. Ломая стратегию OnPush в других компонентах. Но рекомендовали использовать markDirty а не detectChanges
```ts
import { ɵmarkDirty as markDirty } from  '@angular/core';
@Component({...})
class  MyComponent {
	setTitle(title: string) {
		this.title = title;
		markDirty(this);
	}
}
```

**Cинхронно вызывает процесс обнаружения изменений в компоненте и его подкомпонентах  | #detectChanges**  
Предположительно ререндер идёт от компонента.
```ts
import { ɵdetectChanges as detectChanges } from '@angular/core';
@Component({...})
class  MyComponent {
	setTitle(title: string) {
		this.title = title;
		detectChanges(this);
	}
}
```

**Установка заголовка с помощью службы "Title"  | #Title**  
```ts
import { Title } from "@angular/platform-browser"
@Component({  
    ...  
})  
export class LoginComponent implements OnInit {  
  constructor(private title: Title) {} ngOnInit() {  
    title.setTitle("Login")  
  }  
}
```

**Установка "meta" информации страницы | #Meta**  
```ts
import { Meta } from "@angular/platform-browser"
@Component({  
    ...  
})  
export class BlogComponent implements OnInit {  
  constructor(private meta: Meta) {} ngOnInit() {  
    meta.updateTag({name: "title", content: ""})  
    meta.updateTag({name: "description", content: "Lorem ipsum dolor"})  
    meta.updateTag({name: "image", content: "./assets/blog-image.jpg"})  
    meta.updateTag({name: "site", content: "My Site"})  
  }  
}
```

**Proxy (перехват, модификация, замена) запросов | #HttpInterceptor**  
Используется для: 
-   Аутентификация
-   Кэширование
-   Подмена бэкэнд
-   Преобразование URL
-   Изменение заголовков
```ts
@Injectable()  
export class MockBackendInterceptor implements HttpInterceptor {  
  constructor() {} 
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {  
    ...  
  }  
}
```
```ts
@NgModule({  
...  
providers: [  
  {  
    provide: HTTP_INTERCEPTORS,  
    useClass: MockBackendInterceptor,  
    multi: true  
  }  
]  
...  
})  
export class AppModule {}
```

**Метод запускающийся при инициализации приложения | #APP_INITIALIZER**  
```ts
function runSettingsOnInit() {  
...  
}
```
```ts
@NgModule({  
  providers: [  
    { provide: APP_INITIALIZER, useFactory: runSettingsOnInit }  
  ]  
})
```

**Bootstrap Listener | #APP_BOOTSTRAP_LISTENER**
```ts
@NgModule({  
  {  
    provide: APP_BOOTSTRAP_LISTENER, multi: true,  
    useExisting: runOnBootstrap  
  }  
...  
})  
export class AppModule {}
```  

**Одиночное и множественное представление | #ngPlural**

Атрибут [ngPlural] для выражения переключения. Внутренние элементы с [ngPluralCase] будут отображаться на основе их выражения.
```ts
<p [ngPlural]="components">  
  <ng-template ngPluralCase="=1">1 component removed</ng-template>  
  <ng-template ngPluralCase=">1">{{components}} components removed </ng-template>  
</p>
```

**Подписка на свойства store(селектор)**
По задаче, надо изменить значения control form у ангуляр материал во время изменения выбранного пользователя
```ts
// Пример 1. подписка на свойства стора по селекту sGetSelectUser
ngOnInit(): void {
  this.subscription.add(  
    this.store.pipe(  
      select(sGetSelectUser)  
    ).subscribe((user) => {  
      this.userForm.get('baseInfo').setValue({  
        userId: user.id,  
        userName: user.name  
      });  
    })  
  );
}
// Пример 2. Ловим изменения в @input и отслеживаем в ngOnChanges
ngOnChanges(changes: SimpleChanges): void {  
  if (changes.selectUser) {  
    this.userForm.get('baseInfo').setValue({  
      userId: changes.selectUser.currentValue.id,  
      userName: changes.selectUser.currentValue.name  
    });  
  }   
}
```

**Общепринятые core.module.ts и shared.module.ts**
Общий модуль расшаривающий сервисы подобно общему компоненту shared.module
```ts
@NgModule({imports:[], declarations:[], providers:[]})
export class CoreModule {
  static forRoot(): ModuleWithProviders  {  
    return { 
      ngModule: CoreModule,
      providers: [ 
        AuthService,
        LoggerService,
        SettingsService
      ]
    };
  }
}
```

**Подписка на исходящи события инпута | subscribe**
```ts
<input type="text" #inputName>
...
@ViewChild('inputName', {static: false}) refInputName: ElementRef<any>;
@Output() eventEditUser = new EventEmitter();
...
ngAfterViewInit(): void {
const refInputName$: Observable<ElementRef> = fromEvent(this.refInputName.nativeElement, 'input');
refInputName$.subscribe((e: ElementRef<any>) => {
    this.eventEditUser.emit({
      name: e.refInputName.value
    });
  });
}
```
**Ссылки на элемент | @ViewChild, #шаблонные_ссылки**
```ts
 
<input  type="text" #myInput>
...
@ViewChild('myInput') private refMyInput: ElementRef;
```

**Пример input с типизацией и обработкой enter и blur | #шаблонные_ссылки, #keyup, #blur**  
```html template
<input type="text" 
       (keyup.enter)="onInput($event)" 
       (blur)="onBlur(myInput.value)"
       #myInput/>
<h2>{title}</h2>
```
```ts component
title: string = '';
// ...
onInput(event: KeyboardEvent) {
  // this.title = (<HTMLInputElement>event.target).value;
  this.title = (event.target as HTMLInputElement).value;
}

onBlur(value: string) {
  this.title = value;
}
```

**Динамические стили/классы | #ngStyle, #ngClass**
```html
<div [ngStyle]="{
        width: '200px',
        height: '200px',
        margin: '10px',
        backgroundColor: bool ? '#ccc' : '#333'
}"></div>
...
<div [ngClass]="{
        color1: !bool,
        color2: bool
}"></div>
...
<div [class.color1]="!bool"
     [class.color2]="bool"
></div>
```

**Структурная директива ngIf, шаблоны ng-template | #ngIf, #ngTemplate**
```html
<div *ngIf="!bool; else myElse">ngIf</div>
<ng-template #myElse>
  <div>myElse</div>
</ng-template>
...
<div  *ngIf="condition; then thenBlock else elseBlock"></div>
<ng-template  #thenBlock>Content to render when condition is true.</ng-template>
<ng-template  #elseBlock>Content to render when condition is false.</ng-template>
```

**Структурная директива ngSwitch| #ngSwitch, #ngSwitchCase, #ngSwitchDefault**
```html
<div [ngSwitch]="bool" (click)="bool = !bool">
  <p *ngSwitchCase="true">ngSwitchCase-1</p>
  <p *ngSwitchCase="false">ngSwitchCase-2</p>
  <p *ngSwitchDefault>ngSwitchDefault-0</p>
</div>
```
**Структурная директива ngFor| #ngFor**
```html
<ul *ngFor="let n of arr; let inx = index">
  <li>{{inx + 1}}: {{n}}</li>
</ul>
```
**Ng-content | #ng-content**
```html
// Родительский компонент app-test
// items = [{name: 'test-1'}, {name: 'test-2'}, ... ]
<div *ngFor="let item of items; let i = index">
  <app-content-test [itemName]="item.name">
    <div>num: {{i + 1}}</div>
  </app-content-test>
</div>
```
```html
// Дочерний компонент app-content-test
<div>
  <ng-content></ng-content>
  <div>name: {{itemName}}</div>
</div>
```
```ts
// Дочерний компонент app-content-test, доступ к коненту
@ContentChild('info', {static: true}) infoRef: ElementRef;
ngOnInit(): void {
  console.log(this.infoRef.nativeElement);
}
```
**Стратегии компонента | #ChangeDetectionStrategy, #ViewEncapsulation**
```ts
import { Component, ChangeDetectionStrategy, ViewEncapsulation} from '@angular/core';

@Component({
  selector: 'app-mycmp',
  templateUrl: './content.mycmp.html',
  styleUrls: ['./content.mycmp.scss'],
  changeDetection: ChangeDetectionStrategy.OnPush, // ререндер только при изменении инпутов
  encapsulation: ViewEncapsulation.None // сделать стили глобальными
})
export class ContentComponent {
  // ...
}
```

**Атрибутная дирректива, пример передачи параметров | #@Directive, #@HostBinding #@HostListener**
```html
<div appTestDirective color="green">test content</div>
```
```ts
import {Directive, ElementRef, HostBinding, HostListener, Input, Renderer2} from '@angular/core';

@Directive({
  selector: '[appTestDirective]'
})
export class TestDirectiveDirective {
  @Input() color = 'red';
  @HostBinding('style.color') elColor = null;

  constructor(
    // private elRef: ElementRef,
    // private renderer: Renderer2
  ) {}

  @HostListener('click', ['$event.target']) onCLick(event: Event) {
      console.log(event);
  }

  @HostListener('mouseenter') onEnter() {
    // this.renderer.setStyle(this.elRef.nativeElement, 'color', this.color); // 1 вариант
    this.elColor = this.color; // 2 вариант
  }

  @HostListener('mouseleave') onLeave() {
    // this.renderer.setStyle(this.elRef.nativeElement, 'color', null); // 1 вариант
    this.elColor = null; // 2 вариант
  }
}
```
**Структурная дирректива | #@Directive**
```html
<div *appMyIf="bool">test content</div>
```
```ts
import {Directive, Input, TemplateRef, ViewContainerRef} from '@angular/core';

@Directive({
  selector: '[appMyIf]'
})
export class MyIfDirective {
  @Input('appMyIf') set myIf(condition: boolean) {
    if (!condition) {
      this.viewContainer.createEmbeddedView(this.templateRef);
    } else {
      this.viewContainer.clear();
    }
  }
  constructor(
    private templateRef: TemplateRef<any>,
    private viewContainer: ViewContainerRef
  ) { }
}
```
**Кастомный пайп фильтр | #@Pipe**
search-filter.pipe.ts
```ts
import { Pipe, PipeTransform } from '@angular/core';
import { Item } from '../../app.component'; // { title: string }

@Pipe({
  name: 'searchFilter',
  pure: false // отключает оптимизация detec-changes
})
export class SearchFilterPipe implements PipeTransform {

  transform(items: Item[], search: string = ''): Item[] {
    if (!search.trim()) {
      return items;
    }

    return items.filter((item: Item) => {
      return item.title.includes(search);
    });
  }
}
```
**Шаблон компонента использующий пайп**
```html
<!-- 
  search = '';
  items: Item = [{titile: abc},{titile: xyz}];
-->
<div>
  <input type="text" [(ngModel)]="search" />
  <div *ngFor="let item of items | searchFilter:search">
    <p>{{item.title}}</p>
  </div>
</div>
```
**Модуль компонента использующий пайп**
```ts
@NgModule({
  declarations: [
    // ...
    SearchFilterPipe
    // ...
  ],
  // ...
})
```

**Проверка доступа к камере**  
```html
<iframe src="https://webrtc.github.io/samples/src/content/getusermedia/gum/"
        allow="camera"
        width="100%"
        height="700px"
></iframe>
```

**runOutsideAngular**
```ts
this.ngZone.runOutsideAngular(() => {  
   // .... 
});
```

## Events 

**Отлавливаем событие resize**  
```html
<div (window:resize)="onResize$.next()"></div>
```
или
```ts
@HostListener('window:resize', ['$event'])
onResize(event) {
  event.target.innerWidth;
}
```

## Routing  

авигация**  
```html
`<a routerLink="/page">1</a>`
```
```html
`<a [routerLink]="['page', item.id]"
    [queryParams]="{bool: true}"
    fragment="fragment">2<a>`
```
```ts
constructor(  
 private router: Router,  
) { }
// ...
this.router.navigate(['/page', id], {
  queryParams: {
    bool: true
  },
  fragment: 'fragment'
});
```
**Подписки на роутинг**  
```ts
constructor(  
  private routActive: ActivatedRoute,  
  private router: Router,  
)
## {  
        "],  
    "@data/*": ["app/data-services/*"],  
    "@modules/*": ["app/modules/*"],  
    "@env/*": ["environments/*"]  
  }
}
```

## Настройка proxy  

**proxy.conf.ts**
```ts
const HOST = `https://host.me/`;  
  
const PROXY_CONFIG = { }  
  
ngOnInit(): void {  
  this.routActive.params.subscribe((params: Params) => {});"/api/*":{  
    "target": HOST,  
  
  this.routActive.queryParams.subscribe((params: Params) => {});"secure": true,  
  
  this.routActive.fragment.subscribe((fragment"changeOrigin": string) => {});  
}
```

# Dependency Injection


## Example DI token  

**Токен**
```ts
import { InjectionToken } from '@angular/core';  
  
export  const TEST_DI_TOKEN = new InjectionToken<string>(  
  'test injection token',  
  {  
    factory: () => {  
      return 'test_di_token';  ue  
  }  
}  
  
module.exports = PROXY_CONFIG;
```

**angular.json**
```json
...
"architect": {
  "serve": {
    "options": {
    }   ...
  }  
);
```
**Компонент** 
```ts
constructor(  
  @Inject(TEST_DI_TOKEN) readonly testDiToken: string,  
) {
  console.log(this.testDiToken); // test_di_token   "proxyConfig": "./proxy.conf.ts"
    }
  }
}
```

## Form | Validator

**component**
```ts
MinDate.validate('01.01.2000')
```
**min-date.ts**
```ts
import { AbstractControl, ValidationErrors, ValidatorFn } from '@angular/forms';  
import { parse, isAfter } from 'date-fns';  
  
import { DATE_FORMAT } from '../../utils/global';  
  
  
export class MinDate {  
  public static validate(min: string): ValidatorFn {  
    return (control: AbstractControl): ValidationErrors | null => {  
      const minDate = parse(  
        min,  
  DATE_FORMAT,  
 new Date(),  
  );  
 const dateIsAfter = isAfter(control.value, minDate);  
  
 return dateIsAfter ? null : { issueMinDate: true };  
  };  
  }  
}
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI3MTQ3ODIwMywtMTMwNTE1ODcyNSwtNT
Y2NjkzMDI5LC0xOTMzOTQ3NTk4LC0xMDY0MjIxNzA1LC0zNTIz
MjAwNjgsLTExMjM5MDAzNDIsLTU4NDYwMTQ3MywxNzg1NzI4Mj
MxLC0xNzE1NjM4NTEwLDEwMDczMzY1ODYsLTEwODY5OTI3NjYs
LTExNzQyNzc0OTYsLTEyNjI3NTY4NjcsMTA4MTA2MTU1XX0=
-->