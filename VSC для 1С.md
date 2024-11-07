## Трюки
### Замена двойных энтеров на одинарные:
Ищем `^(\s*\n)\s*\n`
Меняем `$1`
Описание: с начала строки только пробелы 0..х, ентер, пробелы, ентер. Оставляем только первую строку.
### Уборка хвостовых пробелов
Ищем `(\S)\s+$`
Меняем `$1`
Описание: Непробельный символ, потом 1..n пробельных, в конце строки - меняем на непробельный символ

### Найти не в запросе
`^(\s*)\S(?<!\|)(.*)(\.тн_ПодготовкаЛистовСообщенийДляВоенкомата)`
С начала строки, потом пробельные символы, непробельный, и он не вертикальная черта, потом что угодно, и наконец - что ищем.

## VSC как сравнивалка для 1С
Опять же, спасибо Зигину https://t.me/radio_ingvar
https://github.com/zeegin/vscode-merge-tool-adapter-cli - сравнивалка студией через конфигуратор
Цитата:
### VSCode CLI

`--diff <file1> <file2>` - Open a file difference editor. Requires two file paths as arguments.

`--merge <path1> <path2> <base> <result>` - Perform a three-way merge by providing paths for two modified versions of a file, the common origin of both modified versions, and the output file to save merge results.

`--wait` - Wait for the files to be closed before returning.

`--new-window` - Opens a new session of VS Code instead of restoring the previous session (default).

`--sync <on | off>` - Turn sync on or off.

### VSCode

Compare two files:

```batchfile
--diff %baseCfg %secondCfg --new-window --sync off
```

Three-way merge:

```batchfile
--merge %baseCfg %secondCfg %oldVendorCfg %merged --new-window --sync off --wait
```


Копаем diffEditor в vscode глубже...

В апреле этого года в vscode добавили новый усовершенствованный алгоритм сравнения файлов. По умолчанию он сейчас не включен. С ним сравнения выглядят заметно лучше.

Для включения надо в настройках передернуть по инструкции.

https://code.visualstudio.com/updates/v1_78?ref=dailydevbytes.com#_diff-algorithm-improvements

## 1С тема
https://github.com/ChernyakAI/vscode-onec-theme
1. В Visual Studio Code перейдите на вкладку "Расширения"
2. В окне поиска введите "OneC Theme"
# Ссылки
[Платформа 1С](Платформа%201С.md)
[[VSC]]


