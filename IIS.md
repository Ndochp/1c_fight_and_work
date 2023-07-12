# IIS

## Как включить HTTPS на свежем сервере
Нужно перейти в дефолт сайт и на правой стороне нажать в Binding - по умолчанию там только 80. Нужно создать новый биндинг HTTPS и добавить в него сертификат
![](Pasted%20image%2020230110130624.png)
## Проблема подключения из за пределов местного сервере
`A potentially dangerous Request.Path value was detected fr om the client (:). Description: An unhandled exception occurred during the execution of the current web request`
Надо у опубликованного сайта (IIS) указать Classic .NET AppPool в пуле приложений вместо DefaultAppPool и перезапустить IIS. Или в самом DefaultAppPool заменить managed pipline mode на Classic