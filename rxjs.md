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

## Разновидности Observable

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
**BehaviorSubject - передает новому подписчику последнее значение, в качестве аргумента принимает начальное значение**
```ts
let behaviorSubject = new BehaviorSubject<Number>(3);

behaviorSubject.subscribe(
  v => {console.log('Observer with value of 3: ' + v);}
);

behaviorSubject.next(9);

behaviorSubject.subscribe(
  v => {console.log('Observer with value of 9: ' + v);}
);
```
**ReplaySubject - передает новому подписчику все предыдущие значения, принимаемый параметр - количество предыдущих значений**
```ts
let replaySubject = new ReplaySubject<Number>(2);

replaySubject.next(3);
replaySubject.next(6);
replaySubject.next(9);
replaySubject.next(12);

replaySubject.subscribe(
  value => {console.log('ReplaySubject: ' + value);}
);
```
**AsyncSubject - передает новому подписчику последнее значение, но только после того, как будет вызван метод complete()**
```ts
let asyncSubject = new AsyncSubject<Number>(3);
    
asyncSubject.subscribe(
  value => {console.log('AsyncSubject: ' + value);}
);

asyncSubject.next(3);
asyncSubject.next(6);
asyncSubject.next(9);

asyncSubject.complete();
```

## Методы создающие Observable
```ts
of('one', 'two').subscribe(v => console.log(v)); // one two
```
```ts
from([1,2,3]).subscribe(v => console.log(v)); // 1 2 3
```

## Прочие методы
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
eyJoaXN0b3J5IjpbMTY4MTU0NjEsODAyODg1NTE3LDIwOTM1OT
kwOTYsLTMzMjQzOTAzNiwxNjAzNTg5MzU5LC0yMDYwMzgxMjEy
LDUzMjU0Nzk0MSwtMTY0NzQyNDYyMSwtODEzMzU4MzYsLTE1ND
MxMjU2NDcsMTA2ODg2NTQ4Myw3MzA5OTgxMTZdfQ==
-->