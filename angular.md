[https://habr.com/ru/company/ruvds/blog/476956/](https://habr.com/ru/company/ruvds/blog/476956/)

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
**Ссылки на элемент | @ViewChild**
```ts
 
<input  type="text" #myInput>
...
@ViewChild('myInput') private refMyInput: ElementRef;
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgxMzcyMDc0Miw5NjAxOTU3MzksMTUzOT
ExMTI2NCwtNzEyODAxNzQzLDczNTYyNDU4NCwtNjAzNzU5NTI1
LDE4ODI1NTM3MjcsMTk4MDU1NTY4NCwyMTM5NDIwNTAwLC0xNz
g4ODA4MDIwLC0xNjQ3OTI5NDkzLC03OTY4NTgwNDNdfQ==
-->