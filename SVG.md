# SVG 
Простенький :) графический формат с богатыми возможностями.
Пример файла:
```svg
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
    xmlns:ev="http://www.w3.org/2001/xml-events" width="800px" height="800px">
    <!-- <rect x="0" y="0" width="800" height="800" fill="none" stroke="black" stroke-width="5px" stroke-opacity="0.5" /> -->
    <g fill-opacity="110.6" stroke="black" stroke-width="0.5px">
        <circle cx="50%" cy="50%" r="50%" fill="lightcoral" />
        <circle cx="50%" cy="50%" r="40%" fill="lightblue"  />
        <circle cx="50%" cy="50%" r="25%" fill="lightgreen"  />
        <line x1="0" x2="100%" y1="50%" y2="50%" />
        <line x1="50%" x2="50%" y1="0" y2="100%" />
        <a href="https://wiki.tcsbank.ru/display/ITSA/1C">
            <circle cx="55.444%" cy="50.9999999990%" r="5" fill="black" >
                <title>
                    1С
                </title>
            </circle>
        </a>
    </g>
</svg>
```

для [[VSC]] есть плагин https://marketplace.visualstudio.com/items?itemName=jock.svg с кривоватым превью, зато с подсказками при вводе тегов.

## Документация от мозилы
https://developer.mozilla.org/en-US/docs/Web/SVG