# TS

## tsconfig

```ts
noImplicitAny
strictNullChecks
```

## Examples

**Слияние типов (|)**   
```ts
interface A {
    nameA: string;
}

interface B {
    nameB: string;
}

type AB = A | B;
const testA: AB = { nameA: ''};
const testB: AB = { nameB: ''};
```
**Пересечения типов (&)**  
```ts
interface A {
    nameA: string;
}

interface B {
    nameB: string;
}

type AB = A & B;
const testAB: AB = { nameA: '', nameB: ''};
```
**Обращения к ключам объектов (keyof)**  
```ts
interface IItem {
    id: number;
    name: string;
    bool: boolean;
}

type ITestItem = keyof IItem; // type ITestItem = "id" | "name" | "bool"
```
**Джинерики**  
```ts
interface Point {
 x: number;
 y: number;
}
const pts: Point[] = [{x: 1, y: 1}, {x: 2, y: 0}];

function sortBy<T, K extends keyof T>(vals: T[], key: K): T[] {
   // ...
   return vals;
}

function sortBy(vals: Point[], key: 'x' | 'y'): Point[] {
   // ...
   return vals;
}

function sortBy(vals: Point[], key: keyof Point): Point[] {
   // ...
   return vals;
}

sortBy(pts, 'x'); // ok, 'x' расширяет 'x'|'y' (aka keyof T)
sortBy(pts, 'y'); // ok, 'y' расширяет 'x'|'y'
sortBy(pts, 'z'); // error, Argument of type '"z"' is not assignable to parameter of type '"x" | "y"'.
```
**Создание типа по классу (InstanceType<typeof CLASS_NAME>)**  
```ts
class C {
    nameC = 'test C';
    getName(): string { 
        return this.nameC;
    }
}

type C1 = InstanceType<typeof C>;

const myClass: C1 = new C();

console.log(myClass.getName());
```

## Examples
 
 ```ts
 interface IObject { [key: string]: any; }
 ```

**Исключение типов**   
```ts
type PassportForm = Omit<EmployeeSubmitResponse, 'patronymicName' | 'registrationAddress'>;  
export interface IPassportForm extends PassportForm {  
   middleName: string;  
   reg_add: IAddressInfo;  
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE1NTQyMDg5LDQxMjUzNDE3NywtMTc3Mj
Y0NDU2OCwtMjc5MjI0ODkyXX0=
-->