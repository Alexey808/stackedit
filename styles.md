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

**Ко всем классам начинающиеся с "icon-"**
```css
[class^="icon-"] {}
```

**Calc с переменными | SCSS**
```scss
height: calc(#{$headerHeight} / 2 - #{$paddingWidth});
```

**Прозрачность переменной через RGBA | SCSS**
```scss
border-top: 1px solid rgba($orange, .25);
```

**Масштабирование картинок**
```css
width: auto;
height: auto;
max-height: 100%;
max-width: 100%;
```

**Внутренняя тень, вместе с внешней | inset**
```css
box-shadow: inset 0 0 2px 0px red, 0 0 2px 0px red;
```

**Простейшая анимация**
```css
.grow { transition: all .2s ease-in-out; }
.grow:hover { transform: scale(1.1); }
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
**Скрыть стрелки у input с type=number**  
```scss
input { 
  &::-webkit-outer-spin-button,  
  &::-webkit-inner-spin-button {  
    -webkit-appearance: none;  
  }  
  -moz-appearance: textfield;  
}
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbNTQ3MTc5OTE2LC02NjM0ODY1MjcsLTYzND
A4MDA2MSwtNTg5MzM3NjIyLC0yMDc3MDkyNDg0LC0xMzYwOTY2
OTQ1XX0=
-->