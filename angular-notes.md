
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
**angular.json**
Параметры 
```json
"myenv": {  
  "fileReplacements": [  
    {  
      "replace": "src/environments/environment.ts",  
      "with": "src/environments/environment-my.ts"  
    }  
  ]  
},  
"myenv-prod": {  
  "fileReplacements": [  
    {  
      "replace": "src/environments/environment.ts",  
      "with": "src/environments/environment-my.prod.ts"  
    }  
  ],  
  "optimization": true,  
  "outputHashing": "all",  
  "sourceMap": false,  
  "extractCss": true,  
  "namedChunks": false,  
  "extractLicenses": true,  
  "vendorChunk": false,  
  "buildOptimizer": true,  
  "budgets": [  
    {  
      "type": "initial",  
      "maximumWarning": "2mb",  
      "maximumError": "5mb"  
    },  
    {  
      "type": "anyComponentStyle",  
      "maximumWarning": "6kb",  
      "maximumError": "10kb"  
    }  
  ]  
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzOTkwMTEzNDddfQ==
-->