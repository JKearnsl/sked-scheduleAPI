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
```

## Выбор группы

`GET` `https://sked.mobi/api/v4/groups` `HTTP/1.1`

С параметрами запроса:<br>
`name`: Название_группы<br>
`university_id`: Ид_вуза<br>

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

## Получение токена

`POST` `https://sked.mobi/api/v4/token` `HTTP/1.1`

С json data:

```json
{
    "device_id": "uuid(можно рандомный)",
    "group_id": ид_группы
}
```

ответ:

```json
{
    "code": 200,
    "data": {
        "access_token": "eyJVc2VySWQiOjg5NDcyNCwiRGV2..."
    },
    "errDescr": "",
    "message": "ok"
}
```


Пример запроса:


`POST` `https://sked.mobi/api/v4/token` `HTTP/1.1`

С json data:

```json
{
    "device_id": "7320768f-600d-42fb-8820-f54c60abb440",
    "group_id": 54662
}
```


ответ:

```json
{
    "code": 200,
    "data": {
        "access_token": "eyJVc2VySWQiOjg5NDcyNCwiRGV2..."
    },
    "errDescr": "",
    "message": "ok"
}
```

## Получение расписания

`GET` `https://sked.mobi/api/v4/lessons` `HTTP/1.1`

В headers:
`Authorization`: `Bearer access_token...`

С параметрами запроса:<br>
`startDate`:     Начальная_дата_в_сек<br>
`endDate`:       Конечная_дата_в_сек<br>
`university_id`: Ид_университета<br>
`group_id:`      Ид_группы<br>

Ответ: json расписание


Пример:

`GET` `https://sked.mobi/api/v4/lessons?startDate=1648426726&endDate=1650323926&university_id=22&group_id=54662` `HTTP/1.1`

В headers:
`Authorization`: `Bearer eyJVc2VySWQiOjg5NDcyNC...`

Параметры запроса:<br>
`startDate`:     1648426726<br>
`endDate`:       1650323926<br>
`university_id`: 22<br>
`group_id:`      54662<br>


## Список преподавателей:

`GET` `https://sked.mobi/api/v4/teachers` `HTTP/1.1`

В headers:
`Authorization`: `Bearer eyJVc2VySWQiOjg5NDcyNC...`

С параметрами:<br>
`group_id`: Ид_группы<br>

Ответ: json

Пример запроса:

`GET` `https://sked.mobi/api/v4/teachers?group_id=54662` `HTTP/1.1`

В headers:
`Authorization`: `Bearer eyJVc2VySWQiOjg5NDcyNC...`

С параметрами:
group_id: 54662

Ответ:

```json
{
    "code": 200,
    "data": [
        {
            "degree": "",
            "discipline": "Информатика и программирование, п/г 1",
            "first_name": "Ася",
            "id": 91297,
            "is_my": true,
            "last_name": "асс.Атаян",
            "second_name": "Михайловна"
        },
        {
            "degree": "",
            "discipline": "Информатика и программирование, п/г 2",
            "first_name": "Наталья",
            "id": 168803,
            "is_my": true,
            "last_name": "асс.Щербинина",
            "second_name": "Игоревна"
        },
        ...
    ],
    "errDescr": "",
    "message": "ok"
}
```
