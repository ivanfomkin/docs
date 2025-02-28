---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Получить все спринты доски

Запрос позволяет получить параметры спринтов доски.

## Формат запроса {#section_ths_h2z_pfb}

Чтобы получить параметры всех спринтов доски, используйте HTTP-запрос с методом `GET`:

```json
GET /{{ ver }}/boards/<board-id>/sprints
Host: {{ host }}
Authorization: OAuth <токен>
{{ org-id }}
```

{% include [headings](../_includes/tracker/api/headings.md) %}

#### Ресурс {#req-resource}

- **\<board-id\>**

    Идентификатор доски.


## Формат ответа {#section_tns_n3z_pfb}

{% list tabs %}

- Запрос выполнен успешно

    В случае успешного выполнения запроса API возвращает ответ с кодом 200. Тело ответа содержит JSON-массив с параметрами спринтов доски.

    #### Тело ответа {#answer-body}

    ```json
    [ 
      {
      "self" : "http://api.tracker.yandex.net/v2/sprints/4469",
      "id" : 4469,
      "version" : 1435288720018,
      "name" : "спринт1",
      "board" : {
        "self" : "http://api.tracker.yandex.net/v2/boards/3",
        "id" : "3",
        "display" : "Тестирование"
      },
      "status" : "in_progress",
      "archived" : false,
      "createdBy" : {
        "self" : "http://api.tracker.yandex.net/v2/users/1120000000014425",
        "id" : "1120000000014425",
        "display" : "Виктор Булдаков"
      },
      "createdAt" : "2015-06-23T17:03:24.799+0000",
      "startDate" : "2015-06-01",
      "endDate" : "2015-06-14",
      "startDateTime": "2015-06-01T07:00:00.000+0000",
      "endDateTime": "2015-06-14T07:00:00.000+0000"
      },
       ...
    ]
    ```

    #### Параметры ответа {#answer-params}

    Параметр | Описание | Тип данных
    -------- | -------- | ----------
    self | Адрес ресурса API, который содержит параметры спринта. | Строка
    id | Идентификатор спринта. | Число
    version | Версия спринта. Каждое изменение спринта увеличивает номер версии. | Число
    name | Название спринта. | Строка
    [board](#board) | Объект с информацией о доске, к задачам которой относится спринт. | Строка
    status | Статус спринта. <br/>Возможные статусы:<ul><li>`draft` — открыт;</li><li>`in_progress` — в работе;</li><li>`released` — решен;</li><li>`archived` — в архиве.</li></ul> | Строка
    archived | Нахождение спринта в архиве:<ul><li>`true`— спринт находится в архиве;</li><li>`false`— спринт активен.</li></ul> | Логический
    [createdBy](#createdBy) | Объект с информацией о создателе спринта. | Объект
    createdAt | Дата и время создания спринта в формате: ```YYYY-MM-DDThh:mm:ss.sss±hhmm``` | Строка
    startDate | Дата начала спринта в формате: ```YYYY-MM-DD``` | Строка
    endDate | Дата окончания спринта в формате: ```YYYY-MM-DD``` | Строка
    startDateTime | Дата и время фактического начала спринта в формате: ```YYYY-MM-DDThh:mm:ss.sss±hhmm``` | Строка
    endDateTime | Дата и время фактического окончания спринта в формате: ```YYYY-MM-DDThh:mm:ss.sss±hhmm``` | Строка

    **Поля объекта** `board` {#board}

    Параметр | Описание | Тип данных
    -------- | -------- | ----------
    self | Адрес ресурса API, который содержит информацию о доске. | Строка
    id | Идентификатор доски. | Строка
    display | Отображаемое название доски. | Строка

    **Поля объекта** `createdBy` {#createdBy}

    Параметр | Описание | Тип данных
    -------- | -------- | ----------
    self | Адрес ресурса API, который содержит информацию о пользователе. | Строка
    id | Идентификатор пользователя. | Строка
    display | Отображаемое имя пользователя. | Строка

- Запрос выполнен с ошибкой

    Если запрос не был успешно обработан, ответное сообщение содержит информацию о возникших ошибках:

    HTTP-код ошибки | Описание ошибки
    --------------- | ---------------
    400 Bad Request | Один из параметров запроса имеет недопустимое значение или формат данных.
    403 Forbidden | У пользователя или приложения нет прав на доступ к ресурсу, запрос отклонен.
    404 Not Found | Запрашиваемый ресурс не найден.
    500 Internal Server Error | Внутренняя ошибка сервиса. Попробуйте повторно отправить запрос через некоторое время.
    503 Service Unavailable | Сервис API временно недоступен.

{% endlist %}
