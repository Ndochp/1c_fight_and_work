# Библиотека vanessa-runner

## Ссылки
https://github.com/vanessa-opensource/vanessa-runner - оригинал, смотри там девелоп
https://github.com/oscript-library/vanessa-runner - версия хаба

## Способы указания параметров:

[Документация (из библиотеки)](https://github.com/oscript-library/vanessa-runner?tab=readme-ov-file#%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80%D1%8B-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B8-%D0%B8-%D0%B2%D1%8B%D0%B7%D0%BE%D0%B2%D0%B0)
Для работы, кроме параметров, которые описаны и файла настроек, который чуть хуже описан можно использовать переменные окружающей среды, которые совсем не описаны:
```bsl
	СоответствиеПеременных.Вставить("RUNNER_IBCONNECTION", "--ibconnection");
	СоответствиеПеременных.Вставить("RUNNER_IBNAME", "--ibname");
	СоответствиеПеременных.Вставить("RUNNER_DBUSER", "--db-user");
	СоответствиеПеременных.Вставить("RUNNER_DBPWD", "--db-pwd");
	СоответствиеПеременных.Вставить("RUNNER_v8version", "--v8version");
	СоответствиеПеременных.Вставить("RUNNER_uccode", "--uccode");
	СоответствиеПеременных.Вставить("RUNNER_command", "--command");
	СоответствиеПеременных.Вставить("RUNNER_execute", "--execute");
	СоответствиеПеременных.Вставить("RUNNER_storage-user", "--storage-user");
	СоответствиеПеременных.Вставить("RUNNER_storage-pwd", "--storage-pwd");
	СоответствиеПеременных.Вставить("RUNNER_storage-ver", "--storage-ver");
	СоответствиеПеременных.Вставить("RUNNER_storage-name", "--storage-name");
	СоответствиеПеременных.Вставить("RUNNER_ROOT", "--root");
	СоответствиеПеременных.Вставить("RUNNER_WORKSPACE", "--workspace");
	СоответствиеПеременных.Вставить("RUNNER_PATHVANESSA", "--pathvanessa");
	СоответствиеПеременных.Вставить("RUNNER_PATHXUNIT", "--pathxunit");
	СоответствиеПеременных.Вставить("RUNNER_VANESSASETTINGS", "--vanessasettings");
	СоответствиеПеременных.Вставить("RUNNER_NOCACHEUSE", "--nocacheuse");
	СоответствиеПеременных.Вставить("RUNNER_LOCALE", "--locale");
	СоответствиеПеременных.Вставить("RUNNER_LANGUAGE", "--language");

	СоответствиеПеременных.Вставить("RUNNER_V8VERSION", "--v8version");
	СоответствиеПеременных.Вставить("RUNNER_ADDITIONAL", "--additional");
	СоответствиеПеременных.Вставить("RUNNER_UCCODE", "--uccode");
	СоответствиеПеременных.Вставить("RUNNER_COMMAND", "--command");
	СоответствиеПеременных.Вставить("RUNNER_EXECUTE", "--execute");
	СоответствиеПеременных.Вставить("RUNNER_STORAGE_NAME", "--storage-name");
	СоответствиеПеременных.Вставить("RUNNER_STORAGE_USER", "--storage-user");
	СоответствиеПеременных.Вставить("RUNNER_STORAGE_PWD", "--storage-pwd");
	СоответствиеПеременных.Вставить("RUNNER_STORAGE_VER", "--storage-ver");
```
