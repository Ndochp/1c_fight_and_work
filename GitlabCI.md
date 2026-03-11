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

## Управление именем и созданием патча
Делается через раздел `workflow`. Имя это поле 
https://docs.gitlab.com/ci/yaml/workflow/#switch-between-branch-pipelines-and-merge-request-pipelines
If GitLab attempts to trigger:

- A merge request pipeline, start the pipeline. For example, a merge request pipeline can be triggered by a push to a branch with an associated open merge request.
- A branch pipeline, but a merge request is open for that branch, do not run the branch pipeline. For example, a branch pipeline can be triggered by a change to a branch, an API call, a scheduled pipeline, and so on.
- A branch pipeline, but there is no merge request open for the branch, run the branch pipeline.

You can also add a rule to an existing `workflow` section to switch from branch pipelines to merge request pipelines when a merge request is created.

Add this rule to the top of the `workflow` section, followed by the other rules that were already present:

yaml

```yaml
workflow:
  rules:
    - if: $CI_COMMIT_BRANCH && $CI_OPEN_MERGE_REQUESTS && $CI_PIPELINE_SOURCE == "push"
      when: never
    - # Previously defined workflow rules here
```

[Triggered pipelines](https://docs.gitlab.com/ci/triggers/) that run on a branch have a `$CI_COMMIT_BRANCH` set and could be blocked by a similar rule. Triggered pipelines have a pipeline source of `trigger` or `pipeline`, so `&& $CI_PIPELINE_SOURCE == "push"` ensures the rule does not block triggered pipelines.