## Мелочи

### regedit
Не надо бегать по дереву, можно длинные строки типа
`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Search` вставлять сразу в адресую строку
### Отключить поиск в кнопке пуск
Работает в Win10
В `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Search` добавить ключи типа число 32, значение 0:
* BingSearchEnabled
* CortanaConsent
* 