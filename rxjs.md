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
## Отписки | #unsubscribe
Операторы которые отписываются при определённых условиях
- take(n)
- asyncPipe
- takeUntil
- takeWhile
- first

**Кастомный (@AutoUnsub) декаратор отписки**
```ts
function AutoUnsub() {
  return function(constructor) {
    const orig = constructor.prototype.ngOnDestroy
    constructor.prototype.ngOnDestroy = function() {
      for(const prop in this) {
        const property = this[prop]
        if(typeof property.subscribe === "function") {
          property.unsubscribe()
        }
      }
      orig.apply()
    }
  }
}

/* use */
@Component({ ... })  
@AutoUnsub  
export class AppComponent implements OnInit { ... }
```

# Объединяющие

_zip_,  _concat_
```ts
const s1$ = of([{id: 4}, {id: 2}]);  
const s2$ = of([{id: 1}]);  
const s3$ = of([{id: 3}]);  
  
zip(s1$, s2$, s3$)  
  .pipe(  
    map(res => [].concat(...res)),  
    map(res => res.sort((a, b) => a.id - b.id))  
  )  
  .subscribe(res => console.log(res));  
/**  
 0: {id: 1}
 1: {id: 2}
 2: {id: 3}
 3: {id: 4}
 */
```
_forkJoin_, _map_
```ts
const s1$ = of([{id: 2}, {id: 1}]);  
const s2$ = of([{id: 3}]);  
  
forkJoin([s1$, s2$]).pipe(  
  map(([s1, s2]) => [...s1, ...s2]),  
  map(res => res.sort((a, b) => a.id - b.id))  
).subscribe((res) => {  
  console.log(res);  
});  
/*  
0: {id: 1}  
1: {id: 2}  
2: {id: 3}  
*/
```
_merge_, _reduce_
```ts
const s1$ = from([{id: 2}, {id: 1}]);  
const s2$ = from([{id: 3}]);  
  
merge(s1$, s2$).pipe(  
  reduce((result, value) => {  
    return [...result, value];  
  }, []),  
  map(res => res.sort((a, b) => a.id - b.id))  
).subscribe((res) => console.log(res));  
/*  
0: {id: 1}  
1: {id: 2}  
2: {id: 3}  
*/
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTcwMTE3ODExMCwxODk3NDQ0MDE0LC0xMj
cyMTA1ODQ1LDE0NjQwMTE1NTMsMTg3Mjc1MzYxMSwxNjgxNTQ2
MSw4MDI4ODU1MTcsMjA5MzU5OTA5NiwtMzMyNDM5MDM2LDE2MD
M1ODkzNTksLTIwNjAzODEyMTIsNTMyNTQ3OTQxLC0xNjQ3NDI0
NjIxLC04MTMzNTgzNiwtMTU0MzEyNTY0NywxMDY4ODY1NDgzLD
czMDk5ODExNl19
-->