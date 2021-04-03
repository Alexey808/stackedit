

## Подключение stylelint  

1) `npm install --save-dev stylelint stylelint-config-standard`
2) Создаём правила. Генератор правил: https://maximgatilin.github.io/stylelint-config/
3) Конфиг файл
**.stylelintrc.json**
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
2) Settings/Preferences > Languages and Frameworks > Style Sheets > Stylelint ставим галочку Enable. 

Генератор правил: https://maximgatilin.github.io/stylelint-config/

~/dev/angular-base/node_modules/stylelint

architect > build > configurations

architect > configurations
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjQyNTIwNjYxLDY0OTc0MTE5XX0=
-->