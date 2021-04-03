# Angular testing

`spyOn()` - отслеживает состояния и использование методов объекта;  
`spyOnProperty()` - используется для отслеживания состояния и использования свойств объекта;  
`jasmine.createSpy` - создает функцию, у которой нет определения;  
`jasmine.createSpyObj` - создает объект-заглушку.  

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
eyJoaXN0b3J5IjpbMTAyMjM2MzQ0OF19
-->