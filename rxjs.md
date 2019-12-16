Оффициальный туториал  [RxJS]([http://reactivex.io/rxjs/manual/tutorial.html](http://reactivex.io/rxjs/manual/tutorial.html))



```ts
of('one', 'two').subscribe(v => console.log(v)); // one two
```
```ts
from([1,2,3]).subscribe(v => console.log(v)); // 1 2 3
```
timer(2000).subscribe(v => console.log(v)); //0

range(42, 3).subscribe(v => console.log(v)); //42,43,44

const inteval$ = interval(500).subscribe(v => console.log('interval', v));  // каждые 500мс number++
setTimeout(()  => inteval$.unsubscribe(),  1000);
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkxNzEyNDcyNCwtODEzMzU4MzYsLTE1ND
MxMjU2NDcsMTA2ODg2NTQ4Myw3MzA5OTgxMTZdfQ==
-->