[https://habr.com/ru/company/ruvds/blog/476956/](https://habr.com/ru/company/ruvds/blog/476956/)

**Принудительный ререндер | markDirty**
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

**Cинхронно вызывает процесс обнаружения изменений в компоненте и его подкомпонентах  | detectChanges**
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

**Установка заголовка с помощью службы "Title" **
```ts
import { Title } from "@angular/platform-browser"@Component({  
    ...  
})  
export class LoginComponent implements OnInit {  
    constructor(private title: Title) {} ngOnInit() {  
        title.setTitle("Login")  
    }  
}
```

**Установка "meta" информации cmjfu**
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY4MTA3NzQ3OCwtNzk2ODU4MDQzXX0=
-->