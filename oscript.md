---
Aliases: OneScript, оскрипт, ванскрипт
---
# Библиотека vanessa-runner
#надоСделать вставить ссылку на гитхаб, оскрипт хаб и точечно  в документацию
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
