# Angular settings  


## Добавление env
Добавленные здесь `channel` и `theme` опционально. Как пример для изменения api или темы в зависимости от окружения. Подобные изменения нужно применить и к дефолтным `environment.ts` и `environment.prod.ts` соответственно.

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

За основу для prod версии можно сопировать параметры с `production`
```json
// вложенность: architect > build > configurations

"production": { },
"myenv": {  
  "fileReplacements": [  
    {  
      "replace": "src/environments/environment.ts",  
      "with": "src/environments/environment-myenv.ts"  
    }  
  ]  
},  
"myenv-prod": {  
  "fileReplacements": [  
    {  
      "replace": "src/environments/environment.ts",  
      "with": "src/environments/environment-myenv.prod.ts"  
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

// вложенность: architect > configurations

"production": { },
"myenv": {  
  "browserTarget": "angular-base:build:myenv"  
},  
"myenv-prod": {  
  "browserTarget": "angular-base:build:myenv-prod"  
}
```
**package.json**
```json
{
  "scripts": {
     "start-myenv": "ng serve --configuration=myenv",
     "build-myenv": "ng build --configuration=myenv-prod", 
  }
}
```


## Подключение stylelint

1) `npm install --save-dev stylelint stylelint-config-standard`
2) Создаём `.stylelintrc.json` в корне проекта и генерируем пользовательские правила. Генератор: https://maximgatilin.github.io/stylelint-config/
3) Настройка подсветки в WebStorm: Settings/Preferences > Languages and Frameworks > Style Sheets > Stylelint ставим галочку Enable. 

**корень_проекта/.stylelintrc.json**  

Понравились мне  
```
{
    "extends": "stylelint-config-standard",
    "rules": {
        "indentation": 2,
        "no-duplicate-selectors": true,
        "color-hex-case": "lower",
        "selector-no-id": true,
        "selector-combinator-space-after": "always",
        "selector-attribute-operator-space-before": "always",
        "selector-attribute-operator-space-after": "always",
        "declaration-block-trailing-semicolon": "always",
        "declaration-colon-space-before": "never",
        "declaration-colon-space-after": "always",
        "property-no-vendor-prefix": true,
        "value-no-vendor-prefix": true,
        "function-url-quotes": "always",
        "font-family-name-quotes": "always-where-required",
        "at-rule-no-vendor-prefix": true,
        "rule-empty-line-before": "always-multi-line",
        "selector-pseudo-class-parentheses-space-inside": "never",
        "selector-no-vendor-prefix": true,
        "media-feature-range-operator-space-before": "always",
        "media-feature-range-operator-space-after": "always",
        "media-feature-parentheses-space-inside": "never",
        "media-feature-name-no-vendor-prefix": true,
        "media-feature-colon-space-before": "never",
        "media-feature-colon-space-after": "always"
    }
}
```
**Отключение линтеров**
```css
/* stylelint-disable */
a {}
/* stylelint-enable */
```
```css
/* stylelint-disable-next-line declaration-no-important */
color: pink !important;
```

## Настройка абсолютных путей

**tsconfig.app.json**
```json
"compilerOptions": {
  ..
  "paths": {  
    "@api/*": ["app/api/*"],  
    "@data/*": ["app/data-services/*"],  
    "@modules/*": ["app/modules/*"],  
    "@env/*": ["environments/*"]  
  }
}
```

## Настройка proxy  

**proxy.conf.ts**
```ts
const HOST = `https://host.me/`;  
  
const PROXY_CONFIG = {  
  "/api/*":{  
    "target": HOST,  
    "secure": true,  
    "changeOrigin": true  
  }  
}  
  
module.exports = PROXY_CONFIG;
```

**angular.json**
```json
...
"architect": {
  "serve": {
    "options": {
       ...
       "proxyConfig": "./proxy.conf.ts"
    }
  }
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbODE2MzU3MTIyLDgxNjM1NzEyMiwxMzY5Nz
cyMTYsMTY1OTI2MDg5NywtMTI3NjYwMjU3MywtNzkyMjQ5MTQx
LC0yMDkwNzI2MjAsLTE1MjQ2NjUzMDJdfQ==
-->