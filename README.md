# sket-scheduleAPI
API приложения sked - расписание занятий для ВУЗов


TODO: написать sync wrapper на python


## Выбор университета:

`GET` `https://sked.mobi/api/v4/universities` `HTTP/1.1`

Пример ответа:

```json
{
    "code": 200,
    "data": [
        {
            "formatted_name": "Санкт-Петербургский<br>политехнический<br>университет ",
            "group_name_example": "3530202/90002",
            "group_name_example_simple": "353020290002",
            "id": 5,
            "name": "СПбПУ - Санкт-Петербургский политехнический университет ",
            "order": 1,
            "tags": "СПбПУ, Санк-Петербург, Политех "
        },
        {
            "formatted_name": "СибГУТИ",
            "group_name_example": "АБ-021",
            "group_name_example_simple": "аб021",
            "id": 82,
            "name": "СибГУТИ - Сибирский государственный университет телекоммуникаций и информатики",
            "order": 1,
            "tags": "СибГУТИ, ГУТИ. Сибирь "
        },
        ...
    ],
    "errDescr": "",
    "message": "ok"
}

## Выбор группы

`GET` `https://sked.mobi/api/v4/groups` `HTTP/1.1`

С параметрами запроса:
`name` = `ГРУППА`
`university_id` = `ИД ВУЗА`

Пример:

`GET` `https://sked.mobi/api/v4/groups?name=ВПР12&university_id=22` `HTTP/1.1`

ответ:

```json
{
    "code": 200,
    "data": {
        "groups": [
            {
                "id": 54662,
                "info": "1 курс, ф. ИиВТ",
                "name": "ВПР12",
                "schedule_status": "Доступно расписание"
            }
        ],
        "header": null
    },
    "errDescr": "",
    "message": "ok"
}
```
