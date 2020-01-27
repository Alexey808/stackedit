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
```
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
eyJoaXN0b3J5IjpbLTQ4MjgwNzUwOCwyMDkzNTk5MDk2LC0zMz
I0MzkwMzYsMTYwMzU4OTM1OSwtMjA2MDM4MTIxMiw1MzI1NDc5
NDEsLTE2NDc0MjQ2MjEsLTgxMzM1ODM2LC0xNTQzMTI1NjQ3LD
EwNjg4NjU0ODMsNzMwOTk4MTE2XX0=
-->