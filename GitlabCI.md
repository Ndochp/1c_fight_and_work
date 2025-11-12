## Всякие мелочи
### Узнать коммит (и вообще информацию по последнему успешному пайпу)
```
curl --header "PRIVATE-TOKEN:TOKEN" "GITLAB_URL/api/v4/projects/PROJECT_ID/pipelines?status=success&per_page=1" | jq '.[0].sha'
```

- `GITLAB_URL` - URL вашего GitLab-сервера.
- `PROJECT_ID` - идентификатор проекта в GitLab, где вы хотите получить коммит.
- `TOKEN` - ваш токен доступа GitLab API.
`| jq '.[0].sha'` это cli парсер Json, можно и без него, главное принцип запроса АПИ
до кучи полезные ключи: `&source=schedule&ref=develop`
### Кодирование имени проекта в группе для API
Код проекта внутри группы, например `some/thing` должен кодироваться как  `some%2Fthing`, то есть `/` меняется на `%2F`

## Генерация чейнджлогов
#надоСделать Добавить сюда описание файла настройки генерации чейнджлогов из документации (.gitlab/changelog_config.yml)

https://gitlab.company.ru/api/v4/projects/группа%2Fпроект/repository/changelog?version=1.0.47