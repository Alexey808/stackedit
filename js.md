


**Анонимные функции | Оператор void**
```js
void function() {
	console.log('test');
}()
//> test
```
```js
void function aRecursion(i) {
	if(i > 0) {
		console.log(i--)
		aRecursion(i)
	}
}(2)
//> 1
//> 2
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

**Делает объект и его свойства не изменяемыми | #freeze**
```js
Object.freeze(myObject);
```

**Делает объект  не изменяемым но перезаписываемыми свойствами  | #seal**
```js
Object.seal(myObject);
```

**Проверка свойства**  
```js
function onConsole(val) {
	if ('name' in val) {
	    console.log(val);
	}
}
onConsole({name: 'test'}); // {name: 'test'}
onConsole({nameee: 'it is fail'}); // undefined
```

**JSON и Base64**
```js
{
	amount: 10.00,
	description: 'test_payment',
	issuer_id: '0.160102105757055',
	ts: 1607028732,
	user_info: {user_id: 'test_user111'},
	view: {skin: 'checkout'},
	scenario: 'item',
	pay_method: 'cpgtest',
	currency: 'RUB',
};


var obj =  {
	amount: 10.00,
	description: 'test_payment',
	issuer_id: '0.160102105757055',
	ts: 1607028732,
	user_info: {user_id: 'test_user111'},
	view: {skin: 'checkout'},
	scenario: 'item',
	pay_method: 'cpgtest',
	currency: 'RUB',
};

var obj = { prop1: 'test1', prop2: { value: 'test2' } };

var obj_json = JSON.stringify(obj); // object -> json

var json_base64 = btoa(obj_json); // json -> base64

var base64_json = atob(json_base64); // base64 -> json

var json_obj = JSON.parse(base64_json); // json -> object
```



<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA0NzIzNTAxNSw3OTEwNzQ3NzcsLTY5OD
g3MTM1MCwtMjA5NjM3NDc5NSwtMTExMjQ1ODcxLDcyODMyNzEx
NSwtMTYzMjU3MjgxN119
-->