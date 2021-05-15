# Angular testing

`spyOn()` - отслеживает состояния и использование методов объекта;  
`spyOnProperty()` - используется для отслеживания состояния и использования свойств объекта;  
`jasmine.createSpy` - создает функцию, у которой нет определения;  
`jasmine.createSpyObj` - создает объект-заглушку.  

## Tests  

**Тесты | #toBe, #toContain, #beforeEach, #beforeAll, #afterEach, #afterAll**
Базовое в юнит тестах
```ts
/* base unit tests */
describe('myMethod', () => {
	it('should ...', () => {
		expect(myFunc(1)).toBe(2); // toBe жёсткое соответствие
		expect(getMyStr('test')).toContain('test'); // toContain частич соответств, прим к строкам массивам
		expect(getMyArray()).toContain('test3'); // toContain частич соответств
	})
})
```
**Базовое в тестировании компонентов**
```ts
/* base testing component */
describe('myComponent', () => {
	let myComponent: MyComponent;

	beforeEach(() => { // вызывается перед каждый тестом it-ом
		component = new MyComponent();
	});
	beforeAll(() => {}); // вызывается перед всеми "it"
	afterEach(() => {}); // вызывается после завершения каждого "it"
	afterAll(() => {}); // вызывается после завершения всех "it"

	it('should ...', () => {
		expect(myFunc(1)).toBe(2); // toBe жёсткое соответствие
	})
})
```

## Examples

**Тестирование метода сервиса возвращающего простые элементы**   
```ts
describe('AppService', () => {
 beforeEach(() => {
   const appServiceSpy = jasmine.createSpyObj('AppService', {
     getData: [1, 2, 3]
   });

   TestBed.configureTestingModule({
     providers: [
       {provide: AppService, useValue: appServiceSpy}
     ]
   });
  
   appService = TestBed.get(AppService);
 });

 it('emulate getData usage', () => {
   const data = [1, 2, 3];

   appService.getData.and.returnValue(data);

   expect(appService.getData().length)
     .toBe(data.length, 'length should be 3');
  });
});
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU5Mjg1NDA1OSwxMDIyMzYzNDQ4XX0=
-->