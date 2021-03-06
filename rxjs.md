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
**fromFetch**
```ts
of(1, 2, 3)
  .pipe(
    map(id =>
      fromFetch(`https://jsonplaceholder.typicode.com/todos/${id}`, {
        selector: resp => resp.json()
      })
    ),
    concatAll()
  )
  .subscribe(todo => console.log(todo.title));
// (after some time) delectus aut autem
// (after some time) quis ut nam facilis et officia qui
// (after some time) fugiat veniam minus
```

**Запихнуть стрим в массив | operators | #toArray**
```ts
addedUser$.pipe(toArray())
```

## map, mergeAll, mergeMap
```ts
const getData = (param) => {
   return of(`retrieved new data with param ${param}`).pipe(delay(1000))
}  

// используем  map  
from([1,2,3,4]).pipe(
  map(param => getData(param))
).subscribe(val => val.subscribe(data => console.log(data)));  

// используем map и mergeAll  
from([1,2,3,4]).pipe(
  map(param => getData(param)),
  mergeAll()
).subscribe(val => console.log(val));  

// используем mergeMap  
from([1,2,3,4]).pipe(
  mergeMap(param => getData(param))
).subscribe(val => console.log(val));
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

_zip_,  _concat_, _map_
```ts
const s1$ = of([{id: 2}, {id: 1}]);  
const s2$ = of([{id: 3}]);  
  
zip(s1$, s2$)  
  .pipe(  
    map(res => [].concat(...res)),  
    map(res => res.sort((a, b) => a.id - b.id))  
  )  
  .subscribe(res => console.log(res));  
/**  
 0: {id: 1}
 1: {id: 2}
 2: {id: 3}
 */
```
_forkJoin_, _map_
```ts
const s1$ = of([{id: 2}, {id: 1}]);  
const s2$ = of([{id: 3}]);  
  
forkJoin([s1$, s2$]).pipe(  
  map(([s1, s2]) => [...s1, ...s2]),  
  map(res => res.sort((a, b) => a.id - b.id))  
).subscribe((res) => console.log(res));  
/*  
0: {id: 1}  
1: {id: 2}  
2: {id: 3}  
*/
```
_merge_, _reduce_,  _map_
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
# v.7  

### connect, для рассылки  
```ts
const chars$ = of("A", "b", "C", "D", "e", "f", "G");

chars$
  .pipe(
    connect(shared$ =>
      merge(
        shared$.pipe(
          filter(x => x.toLowerCase() === x),
          map(x => `lower ${x.toUpperCase()}`)
        ),
        shared$.pipe(
          filter(x => x.toLowerCase() !== x),
          map(x => `upper ${x}`)
        )
      )
    )
  )
  .subscribe(console.log);
// (synchronously) upper A
// (synchronously) lower B
// (synchronously) upper C
// (synchronously) upper D
// (synchronously) lower E
// (synchronously) lower F
// (synchronously) upper G
```

### connectable (аналог connect), для рассылки  
```ts
import { connectable, merge, of } from "rxjs";
import { filter, map } from "rxjs/operators";

const chars$ = of("A", "b", "C", "D", "e", "f", "G");
const connectableChars$ = connectable(chars$);

const lower$ = connectableChars$.pipe(
  filter(x => x.toLowerCase() === x),
  map(x => `lower ${x.toUpperCase()}`)
);

const upper$ = connectableChars$.pipe(
  filter(x => x.toLowerCase() !== x),
  map(x => `upper ${x}`)
);

merge(lower$, upper$).subscribe(console.log);

connectableChars$.connect();
// (synchronously) upper A
// (synchronously) lower B
// (synchronously) upper C
// (synchronously) upper D
// (synchronously) lower E
// (synchronously) lower F
// (synchronously) upper G
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbNDQ1MjI3NDYsODc0MDExMjc1LC02NjgyNT
c4MjcsMTcwMTE3ODExMCwxODk3NDQ0MDE0LC0xMjcyMTA1ODQ1
LDE0NjQwMTE1NTMsMTg3Mjc1MzYxMSwxNjgxNTQ2MSw4MDI4OD
U1MTcsMjA5MzU5OTA5NiwtMzMyNDM5MDM2LDE2MDM1ODkzNTks
LTIwNjAzODEyMTIsNTMyNTQ3OTQxLC0xNjQ3NDI0NjIxLC04MT
MzNTgzNiwtMTU0MzEyNTY0NywxMDY4ODY1NDgzLDczMDk5ODEx
Nl19
-->