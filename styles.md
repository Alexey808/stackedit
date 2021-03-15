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

**Calc с переменными | SCSS**
```css
height: calc(#{$headerHeight} / 2 - #{$paddingWidth});
```

**Медиа запросы**
```css
@media screen and (max-width: 960px) { /* разрешение экрана */ }
@media screen and (orientation: landscape) { /* ориентация экрана */
   portrait - портретная ориентация
   landscape - альбомная оринетация
}
@media streen and (aspect-ratio: 16/9) { /* соотношение сторон */ }
@media streen and (hover: hover) { /* механизм ввода может наводиться на элемент */ }
@media streen and (hover: none) and (pointer: fine) { /* механизм ввода не может наводиться на элемент */ 
   pointer: coarse - включает в себя указательно ограниченной точности
   pointer: fine - включает в себя точное указатель
   pointer: none - не включает в себя указатель
}

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzk2MjgxMDA4LC01ODkzMzc2MjIsLTIwNz
cwOTI0ODQsLTEzNjA5NjY5NDVdfQ==
-->