
## Добавление env
Добавленные здесь `channel` и `theme` опционально. Как пример для изменения api или темы в зависимости от окружения. И подобные изменения нужно применить и к дефолтным `environment.ts` и `environment.prod.ts` соответственно.

**src/environments/types**
```ts
export interface IEnvironment {  
  production: boolean;  
  name: string;  
  channel: string;  
  theme: string;  
}
```
**src/environments/environment-myenv.ts**
```ts
import { IEnvironment } from './types';  
  
export const environment: IEnvironment = {  
  production: false,  
  name: 'MYENV',  
  channel: 'MYCHANNEL',  
  theme: 'my-theme', 
};
```
**src/environments/environment-myenv.prod.ts**
```ts
import { IEnvironment } from './types';  
  
export const environment: IEnvironment = {  
  production: true,  
  name: 'MYENV',  
  channel: 'MYCHANNEL',  
  theme: 'my-theme', 
};
```
****
```ts

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExODU3MjQ4ODldfQ==
-->