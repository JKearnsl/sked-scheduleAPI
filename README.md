# sked-scheduleAPI
API приложения sked - расписание занятий для ВУЗов


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

В headers:<br>
`Authorization`: `Bearer access_token...`

С параметрами запроса:<br>
`startDate`:     Начальная_дата_в_сек<br>
`endDate`:       Конечная_дата_в_сек<br>
`university_id`: Ид_университета<br>
`group_id:`      Ид_группы<br>

Ответ: json расписание


Пример:

`GET` `https://sked.mobi/api/v4/lessons?startDate=1648426726&endDate=1650323926&university_id=22&group_id=54662` `HTTP/1.1`

В headers:<br>
`Authorization`: `Bearer eyJVc2VySWQiOjg5NDcyNC...`

Параметры запроса:<br>
`startDate`:     1648426726<br>
`endDate`:       1650323926<br>
`university_id`: 22<br>
`group_id:`      54662<br>


## Список преподавателей:

`GET` `https://sked.mobi/api/v4/teachers` `HTTP/1.1`

В headers:<br>
`Authorization`: `Bearer access_token...`

С параметрами:<br>
`group_id`: Ид_группы<br>

Ответ: json

Пример запроса:

`GET` `https://sked.mobi/api/v4/teachers?group_id=54662` `HTTP/1.1`

В headers:<br>
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

## Кол-во публичных задач

`GET` `https://sked.mobi/api/v4/counters` `HTTP/1.1`

В headers:<br>
`Authorization`: `Bearer access_token...`

Пример ответа:

```json
{
    "code": 200,
    "data": {
        "shared_tasks": 1
    }
}
```

## Список задач

`GET` `https://sked.mobi/api/v4/Tasks` `HTTP/1.1`

В headers:<br>
`Authorization`: `Bearer access_token...`

Пример ответа:

```json
{
    "code": 200,
    "data": [],
    "errDescr": "",
    "message": "ok"
}
```

## Список публичных расшаренных (доступных) задач

`GET` `https://sked.mobi/api/v4/Tasks/shared` `HTTP/1.1`

В headers:<br>
`Authorization`: `Bearer access_token...`

Пример ответа:

```json
{
    "code": 200,
    "data": [
        {
            "attachments": null,
            "author": "Sked",
            "author_page": "https://t.me/university_open",
            "can_edit": false,
            "create_date": 1629068941,
            "deadline": 0,
            "id": 159969,
            "is_public": true,
            "lesson": null,
            "lesson_id": null,
            "remind_date": 0,
            "reminder": "no",
            "share_date": 1629068941,
            "status": "inbox",
            "text": "Теперь при создании задачи вы можете сделать её публичной – она будет доступна для просмотра всем в вашей группе.\n\nАвтор задачи может устанавливать дедлайн, прикреплять информацию о занятии и вносить изменения которые будут доступны всем.",
            "title": "Создавайте публичные задачи ",
            "tracking": 0
        }
    ],
    "errDescr": "",
    "message": "ok"
}
```

## Изменить статус задачи (Принять/Отклонить)

`POST` `https://sked.mobi/api/v4/Tasks/status` `HTTP/1.1`

В headers:<br>
`Authorization`: `Bearer access_token...`

В дата передается json:

```json
{
    "id": 159969,
    "status": "ACTIVE"
}
```


Пример ответа:

```json
{
    "code": 200,
    "data": {
        "attachments": null,
        "author": "Sked",
        "author_page": "https://t.me/university_open",
        "can_edit": false,
        "create_date": 1649192437,
        "deadline": 0,
        "id": 576678,
        "is_public": true,
        "lesson": null,
        "lesson_id": null,
        "remind_date": 0,
        "reminder": "no",
        "share_date": 1629068941,
        "status": "active",
        "text": "Теперь при создании задачи вы можете сделать её публичной – она будет доступна для просмотра всем в вашей группе.\n\nАвтор задачи может устанавливать дедлайн, прикреплять информацию о занятии и вносить изменения которые будут доступны всем.",
        "title": "Создавайте публичные задачи ",
        "tracking": 0
    },
    "errDescr": "",
    "message": "ok"
}
```

Заметьте в data->status значение поменялось с "inbox" на "active"


# Создание задачи

Для создания публичной задачи (доступной всем в группе), потребуется
авторизация в ВК, для остальных(приватных) - не потребуется.

## Загрузка файла для задачи

Чтобы загрузить файл, нужно выполнить ряд действий

### Получение ссылки на загрузку

`POST` `https://sked.mobi/api/v4/resources` `HTTP/1.1`

В headers:<br>
`Authorization`: `Bearer access_token...`

В дата передается json:

```json
{
    "filename": "pick_photo-766564743.jpg"
}
```

"pick_photo-766564743.jpg" - имя файла на устройстве


Пример ответа:

```json
{
    "code": 200,
    "data": {
        "attachment_id": 3188,
        "ext": ".jpg",
        "url": "https://sked1.fra1.digitaloceanspaces.com/pick_photo-766564743_637847896380634156.jpg?AWSAccessKeyId=WAOODPZG7QQALEHHOCB7&Expires=1649193258&Signature=RgocH1he2vLWV0Xkdm2nGuXGYU0%3D"
    },
    "errDescr": "",
    "message": "ok"
}
```

Теперь можно по этой ссылке загрузить файл на сервер

### Загрузка файла на сервер

По полученной ссылке из пункта "Получение ссылки на загрузку"<br>
Выполняем `put` запрос на данную ссылку и передаем картинку
в формате `binary/octet-stream`

Пример запроса:

![img.png](img_upload_pic.png)

Файл загружен, можно приступать к созданию задачи 


## Создание задачи

`POST` `https://sked.mobi/api/v4/Tasks` `HTTP/1.1`

В headers:<br>
`Authorization`: `Bearer access_token...`

В дата передается json:

```json
{
    "attachments": [
        {
            "id": 3188
        }
    ],
    "deadline": 1649970398,
    "id": 0,
    "is_public": false,
    "remind_date": 1649106410,
    "reminder": "CUSTOM",
    "status": "ACTIVE",
    "text": "Testdescr",
    "title": "Test"
}
```

Подробно рассмотрим некоторые моменты

`"attachments"` содержит ид вложенных файлов;<br>
пример `"id": 3188` взят из пункта "Загрузка файла для задачи"

`"deadline": 1649970398` содержит время завершения

`"remind_date": 1649106410` содержит время напоминания


Пример ответа:

```json
{
    "code": 201,
    "data": {
        "attachments": [
            {
                "ext": ".jpg",
                "id": 3188,
                "name": "pick_photo-766564743.jpg",
                "url": "https://sked1.fra1.digitaloceanspaces.com/pick_photo-766564743_637847896380634156.jpg"
            }
        ],
        "author": null,
        "author_page": null,
        "can_edit": true,
        "create_date": 1649182040,
        "deadline": 1649970398,
        "id": 576680,
        "is_public": false,
        "lesson": null,
        "lesson_id": null,
        "remind_date": 1649106410,
        "reminder": "custom",
        "share_date": 0,
        "status": "active",
        "text": "Testdescr",
        "title": "Test",
        "tracking": 0
    },
    "errDescr": "",
    "message": "Created new task"
}
```


## Удаление задачи:

`DELETE` `https://sked.mobi/api/v4/Tasks/576680` `HTTP/1.1`

В headers:<br>
`Authorization`: `Bearer access_token...`

Пример ответа:

```json
{
    "code": 200,
    "data": null,
    "errDescr": "",
    "message": "Task removed"
}
```


Если есть вопросы и предложения, открывайте `Issues`. <br>
Обертку выпущу тогда, когда будет желание и потребность 
