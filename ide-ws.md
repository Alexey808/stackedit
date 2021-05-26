## Плагины для автодополнения  
https://www.tabnine.com/

## Подключение prettier в WebStorm  

**Установка**   
`git checkout -b feature/prettier`  
`npm install --save-dev --save-exact prettier`  
По умолчанию обычно редактор сам находит плагин. 

**settings -> Languages & Frameworks -> JavaScript -> Prettier**  
```
Node interpreter: Project node (/usr/bin/node)

Prettier package: ~/projects/job/forward/admin-panel-front/node_modules/prettier
```

**.prettierrc**  
```
{  
  "singleQuote": true,  
  "trailingComma": "all"  
}
```

**Ссылки**  
https://www.jetbrains.com/help/webstorm/prettier.html#ws_prettier_apply_code_style   
https://prettier.io/docs/en/configuration.html  
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzA3MTYxNzE4XX0=
-->