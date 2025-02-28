---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Создать макрос

Запрос позволяет создать макрос.

## Формат запроса {#section_sw2_w4f_sfb}

Чтобы создать макрос, используйте HTTP-запрос с методом `POST`:

```json
POST /{{ ver }}/queues/<queue-id>/macros
Host: {{ host }}
Authorization: OAuth <токен>
{{ org-id }}

{
  "name": "Тестовый макрос",
  "body": "Тестовый комментарий\nnot_var{{currentDateTime}}\nnot_var{{issue.author}}",
  "fieldChanges": [
    {
      "field": "tags",
      "value": "tag1"
    }, 
     ...
  ]
}
```

{% include [headings](../_includes/tracker/api/headings.md) %}

#### Ресурс

- **\<issue-id\>** 
  Идентификатор или ключ очереди. Ключ очереди чувствителен к регистру символов.

#### Тело запроса

  Тело запроса содержит параметры макроса.
   Параметр | Описание | Тип данных
   ----- | ----- | -----
   name | Название макроса.<br/><br/>Обязательное поле. | Строка
   body | [Сообщение](manager/create-macroses.md), которое будет создано при выполнении макроса. Формат: ``` <Текст сообщение>\n<переменная> ```<br/>где:<ul><li> `<Текст сообщения>`— текст, который будет создан в поле **Комментарий** при выполнении макроса.</li><li> ``\n`` — символ переноса строки.</li><li> Переменная, которая может содержать:<br/>`not_var{{currentUser}}` — имя пользователя, который выполнил макрос;<br/> `not_var{{currentDateTime.date}}` — дату выполнения макроса; <br/>`not_var{{currentDateTime}}` — дату и время выполнения макроса;<br/>`{{issue.<ключ_поля>}}` — ключ поля задачи, значение которого отразится в сообщении. Полный список полей задачи: [https://tracker.yandex.ru/admin/fields]({{ link-admin-fields }})</li></ul>Чтобы удалить сообщение, используйте конструкцию `"body": {"unset":1}` | Строка
   [fieldChanges](#fieldChanges) | Массив с информацией о полях задачи, изменения которых запустит макрос. | Массив объектов

  **Объекты массива** `fieldChanges` {#fieldChanges}
   Параметр | Описание | Тип данных
   -------- | -------- | ---------- 
   field | Идентификатор поля задачи.<br/><br/>[Полный список полей задачи]({{ link-admin-fields }}) | Строка
   value | Значение поля задачи. | Строка

## Формат ответа {#section_ibd_4yf_sfb}

{% list tabs %}

- Запрос выполнен успешно
  
  В случае успешного выполнения запроса API возвращает ответ с кодом 200. Тело ответа
 содержит JSON-объект с параметрами созданного макроса.

    ```json
      {
        "self": "{{ host }}/v2/queues/TEST/macros/3",
        "id": 3,
        "queue": {
          "self": "{{ host }}/v2/queues/TEST", 
          "id": "1",
          "key": "TEST",
          "display": "Тестовая очередь"
           },
        "name": "Тестовый макрос",
        "body": "Тестовый комментарий\nnot_var{{currentDateTime}}\nnot_var{{issue.author}}",
        "fieldChanges": [
          {
            "field": {
               "self": "{{ host }}/v2/fields/tags", 
               "id": "tags",
               "display": "Теги"
              },
            "value": [
                    "tag1"
                     ]
          },
           ...
        ]
      }
    ```

    #### Параметры ответа {#answer-params}
    Параметр | Описание | Тип данных
    ----- | ----- | -----
    self | Адрес ресурса API, который содержит параметры макроса. | Строка
    id | Идентификатор макроса. | Число
    [queue](#queue) | Объект с информацией об очереди, к задачам которой применяется макрос. | Объект
    name | Название макроса. | Строка
    body | [Сообщение](manager/create-macroses.md), которое будет создано при выполнении макроса. Формат: ``` <Текст сообщение>\n<переменная> ```<br/>где:<ul><li> `<Текст сообщения>`— текст, который будет создан в поле **Комментарий** при выполнении макроса.</li><li> ``\n`` — символ переноса строки.</li><li> Переменная, которая может содержать:<br/>`not_var{{currentUser}}` — имя пользователя, который выполнил макрос;<br/> `not_var{{currentDateTime.date}}` — дату выполнения макроса; <br/>`not_var{{currentDateTime}}` — дату и время выполнения макроса;<br/>`{{issue.<ключ_поля>}}` — ключ поля задачи, значение которого отразится в сообщении. Полный список полей задачи: [https://tracker.yandex.ru/admin/fields]({{ link-admin-fields }})</li></ul>Чтобы удалить сообщение, используйте конструкцию `"body": {"unset":1}` | Строка
    [fieldChanges](#fieldChanges) | Массив с информацией о полях задачи, изменения которых запустит макрос. | Массив объектов

    **Поля объекта** `queue`{#queue}
    Параметр | Описание | Тип данных
    -------- | -------- | ----------     
    self | Адрес ресурса API, который содержит информацию об очереди. | Строка
    id | Идентификатор очереди. | Строка
    key | Ключ очереди. | Строка
    display | Отображаемое название очереди. | Строка

    **Поля объекта** `fieldChanges` {#fieldChanges}
    Параметр | Описание | Тип данных
    -------- | -------- | ----------     
    [field](#field) | Объект с информацией о поле задачи. | Объект
    value | Массив со значениями поля задачи. | Массив объектов

    **Поля объекта** `field` {#field}
    Параметр | Описание | Тип данных
    -------- | -------- | ---------- 
    self | Адрес ресурса API, который содержит информацию о поле задачи. | Строка
    id | Идентификатор поля задачи. | Строка
    display | Отображаемое название поля задачи. | Строка

- Запрос выполнен с ошибкой
  
  Если запрос не был успешно обработан, ответное сообщение содержит информацию о возникших
 ошибках:
    HTTP-код ошибки | Описание ошибки
    ----- | -----
    `400 Bad Request` | Один из параметров запроса имеет недопустимое значение или формат данных.
    `403 Forbidden` | У пользователя или приложения нет прав на доступ к ресурсу, запрос отклонен.
    `404 Not Found` | Запрашиваемый ресурс не найден.
    `409 Conflict` | Запрос не может быть выполнен по причине конфликта имен.
    `422 Unprocessable Entity` | Ошибка валидации JSON, запрос отклонен.
    `500 Internal Server Error` | Внутренняя ошибка сервиса. Попробуйте повторно отправить запрос через некоторое время.
    `503 Service Unavailable` | Сервис API временно недоступен.
    
{% endlist %}