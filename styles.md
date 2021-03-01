**Font | Подключение шрифта с поддержкой normal и bold**
```scss
@font-face {  
  font-family: 'Helvetica Neue';  
  src: url('#{$font-path}HelveticaNeue.woff') format('woff');  
  font-weight: normal;  
  font-style: normal  
}  
  
@font-face {  
  font-family: 'Helvetica Neue';  
  src: url('#{$font-path}HelveticaNeue-Bold.woff') format('woff');  
  font-weight: bold;  
  font-style: normal  
}
```

**Синтакс обращения к селекторам**  
`[class^="icon-"] {}` - ко всем классам начинающиеся с "icon-"  
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjE5OTIyODkwLC0xMzYwOTY2OTQ1XX0=
-->