


**Анонимные функции | Оператор void**
```js
void function() {
	console.log('test');
}()
// test
```
```js
void function aRecursion(i) {
	if(i > 0) {
		console.log(i--)
		aRecursion(i)
	}
}(2)
// 1
// 2
```

**Анонимные функции | Паттерн IIFE**
```js
//пример 1, возвращаемые значения
var result = (function() {  
return "From IIFE";  
}());    
console.log(result) // From IIFE
```
```js
// пример 2, модульность
var Sequence = (function sequenceIIFE() {  

	// приватная переменная для хранения значения счетчика  
	var current = 0;  
	  
	// объект, возвращаемый IIFE  
	return {  
		getCurrentValue: function() {  
		return current;  
	},  
	  
	getNextValue: function() {  
		current = current + 1;  
		return current;  
	}  
};  
}());  
  
console.log(Sequence.getNextValue()); // 1  
console.log(Sequence.getNextValue()); // 2  
console.log(Sequence.getCurrentValue()); // 2
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbNzI4MzI3MTE1LC0xNjMyNTcyODE3XX0=
-->