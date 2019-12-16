Оффициальный туториал  [RxJS]([http://reactivex.io/rxjs/manual/tutorial.html](http://reactivex.io/rxjs/manual/tutorial.html))



```ts
of('one', 'two').subscribe(v => console.log(v)); // one two

from([1,2,3]).subscribe(v => console.log(v)); // 1 2 3

const inteval$ = interval(500).subscribe(v => console.log('interval', v));  // 0,1
setTimeout(()  => inteval$.unsubscribe(),  1000);
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMzc5MzQ1MTY3LC04MTMzNTgzNiwtMTU0Mz
EyNTY0NywxMDY4ODY1NDgzLDczMDk5ODExNl19
-->