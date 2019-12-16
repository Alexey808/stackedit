Оффициальный туториал  [RxJS]([http://reactivex.io/rxjs/manual/tutorial.html](http://reactivex.io/rxjs/manual/tutorial.html))



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


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNjAzODEyMTIsNTMyNTQ3OTQxLC0xNj
Q3NDI0NjIxLC04MTMzNTgzNiwtMTU0MzEyNTY0NywxMDY4ODY1
NDgzLDczMDk5ODExNl19
-->