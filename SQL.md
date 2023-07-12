
[Сбросить пароль в 1С](Сбросить%20пароль%20в%201С.md)

## Всякие ошибки доступа:
Для доступа к скулю на соседней машине нужен:
1. Включенный 1433 порт на фаерволе
2. TCP режим работы в SQL Configuration
3. Для парольного доступа - смешанный режим в свойствах сервера в студии
4. 

## Подключить MDF без лога
attach mdf without log
При выборе mdf файла создается вторая строчка для лога с предупреждением "будет создан новый пустой", а потом падает с ошибкой доступа. Способ обхода - просто удалить строчку лога. Тогда скуль сам соберет лог как надо. (и положит в папку по умолчанию)

## Привязать пользователя сервера к пользователю базы данных

Иногда происходит отвязка юзверя, или при переносе базы с сервера на сервер нужно привязать к пользователю с тем же именем. Запрос такой

```sql
ALTER USER sonarqube WITH LOGIN = sonarqube;
```

## Работа с MS SQL в пакетном режиме
Используется утилита sqlcmd
### Достать базу из беэкапа (полного)
```cmd 
sqlcmd -S <Инстанс сервера> -U <Пользователь> -P <Пароль>  -Q "RESTORE DATABASE %1 FROM DISK='%2' WITH REPLACE"
```
### погасить/поднять базу

``` 
sqlcmd -S <Инстанс сервера> -U <Пользователь> -P <Пароль>  -Q "ALTER DATABASE [Имя базы данных] SET OFFLINE WITH ROLLBACK IMMEDIATE"
```
WITH ROLLBACK IMMEDIATE - это с разрывом существующих соединений

<details>
    <summary>на всякий случай рядом, пока без проверок Детач/аттач</summary>

```
Goto cmd (Run->cmd)

To connect to local SQL server default instance
>sqlcmd -S .\
Or to connect to named instance (SQLEXPRESS being your named instance)
>sqlcmd -S .\SQLEXPRESS
Or connect to SQL server on another machine
>sqlcmd -S REMOTEMACHINE\INSTANCENAME
After connecting switch to master database
>use master;
>go

Then you should see – Changed database context to ‘master’.

Now attach/detach your database
>sp_detach_db ‘database name’;

>go

>sp_attach_db ‘database name’,’path to mdf’,’path to ldf’;

>go

Edit: To verify the file location, sp_helpfile stored procedure can be used.

use ‘database name’;
go
sp_helpfile
go
```
</details>

##  Размер таблиц в БД MS SQL SERVER отсортированный по убыванию
https://speshuric.livejournal.com/53616.html
``` SQL
select
case when grouping (so.name) = 1 then 'Итого:' else so.name end name,
8*sum(si.data_pages) data, 
8*sum(si.index_pages) indexes, 
8*(sum(si.data_pages)+sum(si.index_pages)) q, 
case when grouping (so.name) = 0 then max (si.rows) else 0 end rows, 
count (is_index) index_count, 
case when grouping (so.name) = 0 then min (isnull(date_recount,getdate())) else null end date_recount_stat,
case when grouping (so.name) = 0 then max (reclen) else 0 end record_len
from
(select 
        case 
                when si.indid between 2 and 251 then isnull(si.used,0)
                else 0
        end index_pages,
        case 
                when si.indid<2 then si.dpages 
                when si.indid = 255 then isnull(si.used,0)
                else 0
        end data_pages,
        case    when si.indid < 2 then si.rows 
                when si.indid between 2 and 251 then 0
                else 0
        end rows,
        case    
                when si.indid between 1 and 251 then 1
                else 0
        end is_index,
        si.id, si.indid, si.name, 
        STATS_DATE(si.id, si.indid) date_recount
from sysindexes si (nolock) 

where si.name not like '_wa_sys%' and si.name not like 'Statistic_%'
) si inner join sysobjects as so (nolock) on so.id=si.id and so.name not like 'sys%'
inner join (select sum(length) reclen, id from syscolumns (nolock) group by id) sc on sc.id = so.id
group by so.name with rollup
order by grouping (so.name), q desc, so.name
```

1. Скрипт запускать из контекста анализируемой БД
2. Размеры приведены к килобайтам.
3. rows может быть неточно (см. документацию)
4. Колонки:
    * name - имя таблицы
    * data - килобайт данных
    * indexes - килобайт индексов
    * q - сумма данных и индексов
    * rows - записей
    * index_count - индексов
    * date_recount_stat - статистика
    * record_len - длина записи
5. На 2005 не проверял. 
