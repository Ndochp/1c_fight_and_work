## Трехсторонка ручная
Картина выглядит так:

| База | Наши изменения | Новинка вендора |
| ---- | -------------- | --------------- |
| 1    | 2              | 3               |
и никто из них не слит никуда, все сливаем руками. 

Исполняемый файл `AppData\Local\Apps\Araxis\Araxis Merge\Compare.exe`
Командная строка в конфигураторе должна выглядеть так:
```cmd
/wait /3 /merge /a1 /title1:%oldVendorCfgTitle /title2:%baseCfgTitle /title3:%secondCfgTitle %oldVendorCfg %baseCfg %secondCfg %merged
```