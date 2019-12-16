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
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzM1NjI0NTg0LC02MDM3NTk1MjUsMTg4Mj
U1MzcyNywxOTgwNTU1Njg0LDIxMzk0MjA1MDAsLTE3ODg4MDgw
MjAsLTE2NDc5Mjk0OTMsLTc5Njg1ODA0M119
-->