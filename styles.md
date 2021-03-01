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
`[class^="icon-"]:before {}` - 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4OTk5MDI4MTQsLTEzNjA5NjY5NDVdfQ
==
-->