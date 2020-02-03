Оффициальный туториал  [RxJS]([http://reactivex.io/rxjs/manual/tutorial.html](http://reactivex.io/rxjs/manual/tutorial.html))

### Подкатегория операторов
-   Создания (of, from, fromEvent, interval);
-   Преобразования (map, scan, buffer);
-   Фильтрации (filter, take, skip, distinct);
-   Объединения (join, merge, zip);
-   Обработки ошибок (catchError, retry, onErrorResumeNext);
-   Условия (contains, skipUntil, skipWhile, takeUntil, takeWhile);
-   Математические (min, max, count, average);
-   Утилиты (tap, delay);
-   Для Connectable Observable (share, shareReplay, publish).

## Разновидность Observable

**Subject - доставляет данные сразу нескольким подписчикам**
```ts
let subject = new Subject();

subject.subscribe(
  v => {console.log('Observer 1: ' + v);}
);
subject.subscribe(
  v => {console.log('Observer 2: ' + v);}
);

subject.next(9);

//Observer 1: 9
//Observer 2: 9
```

```ts
of('one', 'two').subscribe(v => console.log(v)); // one two
```
```ts
from([1,2,3]).subscribe(v => console.log(v)); // 1 2 3
```
```ts
timer(2000).subscribe(v => console.log(v)); //0
```
```ts
range(42, 3).subscribe(v => console.log(v)); //42,43,44
```
```ts
const inteval$ = interval(500)
  .pipe(take(2))
  .subscribe(v => console.log('interval', v));  // каждые 500мс number++
setTimeout(()  => inteval$.unsubscribe(),  1000);
```

**Объеденить 2 стрима | method | #merge**
```ts
const one$ = from([1, 2]);  
const two$ = from([3, 4]);  
const result = merge(one$, two$);  
result.subscribe((item) => {  
  console.log(item);  
});
// 1
// 2
// 3
// 4
```
**Запихнуть стрим в массив | operators | #toArray**
```ts
addedUser$.pipe(toArray())
```

**Отписки в Angular**
```ts
subscription: Subscription = new Subscription();
...
method() {
  this.subscription.add(  
    this.abc.subscribe();
  );
}
...
ngOnDestroy(): void {  
  if (this.subscription) {  
    this.subscription.unsubscribe();
  }
}
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgyMjg2ODUzMyw4MDI4ODU1MTcsMjA5Mz
U5OTA5NiwtMzMyNDM5MDM2LDE2MDM1ODkzNTksLTIwNjAzODEy
MTIsNTMyNTQ3OTQxLC0xNjQ3NDI0NjIxLC04MTMzNTgzNiwtMT
U0MzEyNTY0NywxMDY4ODY1NDgzLDczMDk5ODExNl19
-->