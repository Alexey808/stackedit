## Settings angular material theme


### 1) Установить пакеты:

`@angular/material` (и его зависимости ниже)  
`@angular/animations`
`@angular/cdk`

### 2) Подключение

**app/material.module.ts**
```ts
import { NgModule } from '@angular/core';  
import {  
  MatAutocompleteModule,  
  MatBadgeModule,  
  MatBottomSheetModule,  
  MatButtonModule,  
  MatButtonToggleModule,  
  MatCardModule,  
  MatCheckboxModule,  
  MatChipsModule,  
  MatDatepickerModule,  
  MatDialogModule,  
  MatDividerModule,  
  MatExpansionModule,  
  MatGridListModule,  
  MatIconModule,  
  MatInputModule,  
  MatListModule,  
  MatMenuModule,  
  MatNativeDateModule,  
  MatPaginatorModule,  
  MatProgressBarModule,  
  MatProgressSpinnerModule,  
  MatRadioModule,  
  MatRippleModule,  
  MatSelectModule,  
  MatSidenavModule,  
  MatSliderModule,  
  MatSlideToggleModule,  
  MatSnackBarModule,  
  MatSortModule,  
  MatStepperModule,  
  MatTableModule,  
  MatTabsModule,  
  MatToolbarModule,  
  MatTooltipModule,  
  MatTreeModule,  
} from '@angular/material';  
  
@NgModule({  
  exports: [  
  MatAutocompleteModule,  
  MatBadgeModule,  
  MatBottomSheetModule,  
  MatButtonModule,  
  MatButtonToggleModule,  
  MatCardModule,  
  MatCheckboxModule,  
  MatChipsModule,  
  MatStepperModule,  
  MatDatepickerModule,  
  MatDialogModule,  
  MatDividerModule,  
  MatExpansionModule,  
  MatGridListModule,  
  MatIconModule,  
  MatInputModule,  
  MatListModule,  
  MatMenuModule,  
  MatNativeDateModule,  
  MatPaginatorModule,  
  MatProgressBarModule,  
  MatProgressSpinnerModule,  
  MatRadioModule,  
  MatRippleModule,  
  MatSelectModule,  
  MatSidenavModule,  
  MatSliderModule,  
  MatSlideToggleModule,  
  MatSnackBarModule,  
  MatSortModule,  
  MatTableModule,  
  MatTabsModule,  
  MatToolbarModule,  
  MatTooltipModule,  
  MatTreeModule,  
  ],  
})  
export class MaterialModule {}
```
**app/app.module.ts**
```ts
import { MaterialModule } from './material.module';
@NgModule({
  ...
  imports: [
    MaterialModule
    ...
  ]
})
```
**app/styles/material-theme.scss**
```scss
@import '~@angular/material/theming';  
@include mat-core();  
@import 'material-palette.scss';  

// Объявляем политру
$mat-palette-primary: mat-palette($palette-primary);  

// Создаём тему
$theme-base: mat-light-theme($mat-palette-primary, $mat-lime, $mat-deep-orange);  

// Подключаем тему
@include angular-material-theme($theme-base);
```
**app/styles/material-palette.scss**
Генератор палитры по основному цвету: [http://mcg.mbitson.com/](http://mcg.mbitson.com/)  
Готовые от angular-material: [https://material.io/archive/guidelines/style/color.html#color-color-palette](https://material.io/archive/guidelines/style/color.html#color-color-palette)  
```scss
$palette-primary: (  
  50 : #ffede6,  
  100 : #ffd1c2,  
  200 : #ffb399,  
  300 : #ff9570,  
  400 : #ff7e51,  
  500 : #ff6732,  
  600 : #ff5f2d,  
  700 : #ff5426,  
  800 : #ff4a1f,  
  900 : #ff3913,  
  A100 : #ffffff,  
  A200 : #fffbfa,  
  A400 : #ffcec7,  
  A700 : #ffb8ad,  
  contrast: (  
    50 : #000000,  
  100 : #000000,  
  200 : #000000,  
  300 : #000000,  
  400 : #000000,  
  500 : #ffffff,  
  600 : #ffffff,  
  700 : #ffffff,  
  800 : #ffffff,  
  900 : #ffffff,  
  A100 : #000000,  
  A200 : #000000,  
  A400 : #000000,  
  A700 : #000000,  
  )  
);
```
**angular.json**
```
"projects": {
  ...
  "architect": {
    ...
    "build": {
      ...
      "options": {
	    ...
	    "styles": [  
          ...  
          "src/app/styles/material-theme.scss"  
],
```
**example**
```html
<button mat-raised-button>basic</button>  
<button mat-raised-button color="primary">primary</button>  
<button mat-raised-button color="accent">accent</button>  
<button mat-raised-button color="warn">warn</button>
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk4OTEwMjQwOV19
-->