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