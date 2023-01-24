
## Сбросить пароль в 1С

Источник: http://www.avtomatizator.ru/nashi-publikatsii/31026/

### Где 1С хранит данные о паролях

1С:Предприятие 8.2/8.3 хранит информацию о паролях в двух местах:
1.      В таблице БД **v8users**.
2.      В файле **users.usr**. Файл бинарно сохранен в таблице **Params**.

Учтите, что пароли хранятся не в открытом виде, а в виде хэш кодов. Это несимметричный алгоритм шифрования без возможности обратного восстановления. Поэтому зайти и задать где-то в конкретном поле новый пароль не получится.

Не пытайтесь стирать вообще всю инфу из полей с паролями. Они не бывают пустыми.

### Как получить админский доступ в 1С без пароля

Основная идея в том, что, если при загрузке базы 1С:Предприятия не будет обнаружен ни один пользователь, то вошедший получит максимальные права. При этом, формирование списка доступных привилегий 1С  выполняет только на входе и больше к ним не обращается.

#### Шаг 1. Переименовываем таблицу v8users и файл users.usr

Перед входом в базу данных, куда требуется получить доступ, переименуем таблицу **v8users** в **v8users_tmp**. Так же переименуем файл **users.usr** в **users.usr_tmp**.

Откроем **Management Studio**.

Создаем новый запрос к БД:
``` sql
USE [your_database]
GO
EXEC sp_rename 'v8users', 'v8users_tmp'
GO
UPDATE [Params]
SET [FileName] = 'users.usr_tmp'
WHERE [FileName] = 'users.usr'
GO
```

Идентификатор «your_database» замените на идентификатор своей базы 1С.

И запускаем его: F5 или иконка с восклицательным знаком.

#### Шаг 2. Вход в 1С:Предприятие в режиме конфигуратора

Открываем 1С в режиме конфигуратора. При входе ни пользователя ни пароля запрошено не будет. База откроется с полными правами.

Имейте в виду, что отдельные конфигурации 1С имеют ряд особенностей по управлению пользователями. Эти особенности следует учитывать при выполнении процедуры сброса пароля 1С.

#### Шаг 3. Восстановление таблицы v8users и файла users.usr

Теперь выполним обратную операцию тому, что было сделано на шаге 1.
Снова создаем новый SQL скрипт в **Management Studio**, и вписываем туда:
``` sql
USE [your_database]
GO

DROP TABLE [v8users]
GO

EXEC sp_rename 'v8users_tmp', 'v8users'
GO

UPDATE [Params]
SET FileName = 'users.usr'
WHERE FileName = 'users.usr_tmp'
GO
```


Идентификатор «your_database» замените на идентификатор своей базы 1С.

И запускаем его: F5 или иконка с восклицательным знаком.

#### Шаг 4. Изменяем пароль администратора или создаем нового

В Конфигураторе 1С измените пароль существующего администратора или создайте нового пользователя с административными правами.

##### Замечание: Сброс пароля 1С лучше делать для существующего пользователя

Имейте в виду, что в таких конфигурациях, как «Управление торговлей» версии 11 создание пользователей следует выполнять в режиме 1С:Преприятия, а не в Конфигураторе. Поэтому лучше изменить пароль существующего администратора, а не создавать через Конфигуратор нового пользователя.

### Заключение

Закройте Конфигуратор и откройте снова. Теперь будет действовать указанный пароль на шаге 4.

Обязательно учитывайте особенности управления пользователями конкретной конфигурации 1С.

## Работа с MS SQL в пакетном режиме
Используется утилита sqlcmd
### Достать базу из беэкапа (полного)
``` 
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
