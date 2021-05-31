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

## Async  

**Способ 2**  
```ts
it('', fakeAsync(() => { 
  fixture.whenStable().then(() => {  
    // code
  })  
}));
```

**Способ 1**  
```ts
it('', fakeAsync(() => { 
  tick(100);  
  fixture.detectChanges(); 
  // code
}));
```

## window scroll
```ts
it('should do something on window scroll', () => {
  window.dispatchEvent(new Event('scroll'));
  expect(...)....
});
```

## Ввод значений в input. Тестирование HostListener
```ts
import { DateMaskDirective } from './date-mask.directive';  
import { ComponentFixture, TestBed } from '@angular/core/testing';  
import { FormsModule, ReactiveFormsModule } from '@angular/forms';  
import { DateMaskTestComponent } from './date-mask-test.component';  
import { By } from '@angular/platform-browser';  
  
fdescribe('DateMaskDirective', () => {  
  let fixture: ComponentFixture<DateMaskTestComponent>;  
 let input: HTMLInputElement;  
 let component: DateMaskTestComponent;  
  
  beforeEach(() => {  
    fixture = TestBed.configureTestingModule({  
      declarations: [DateMaskDirective, DateMaskTestComponent],  
  imports: [FormsModule, ReactiveFormsModule],  
  }).createComponent(DateMaskTestComponent);  
  
  component = fixture.componentInstance;  
  input = fixture.debugElement.query(  
      By.directive(DateMaskDirective),  
  ).nativeElement as HTMLInputElement;  
  fixture.detectChanges();  
  });  
  
  it('should create an instance', () => {  
    expect(fixture.componentInstance).toBeTruthy();  
  });  
  
  it('should run to hide', () => {  
    expect(component.isHide).toBeFalsy();  
  input.value = '01.01.2021';  
  input.dispatchEvent(new Event('input'));  
  fixture.detectChanges();  
  expect(component.isHide).toBeTruthy();  
  });  
});
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDM5NTExMTE3LDEyMzA2NTk3NjEsLTEzOT
QwODA0NDYsODEwNzgyMTQwLC01OTI4NTQwNTksMTAyMjM2MzQ0
OF19
-->