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
## Синтакс обращения к селекторам  

**Ко всем классам начинающиеся с "icon-"**
```css
[class^="icon-"] {}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNzcwOTI0ODQsLTEzNjA5NjY5NDVdfQ
==
-->