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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ2MjEwNjY1MywtMTY0NzkyOTQ5MywtNz
k2ODU4MDQzXX0=
-->