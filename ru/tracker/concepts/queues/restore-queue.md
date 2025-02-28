---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Восстановить очередь

Запрос позволяет восстановить удаленную очередь.

## Формат запроса {#section_rnm_x4j_p1b}

Для восстановления удаленной очереди используйте HTTP-запрос с методом `POST`:

```json
POST /v2/queues/<queue-id>/_restore
Host: {{ host }}
Authorization: OAuth <токен>
{{ org-id }}
```

{% include [headings](../../../_includes/tracker/api/headings.md) %}

#### Ресурс {#req-resource}

- **\<queue-id\>**

    Идентификатор или ключ очереди. Ключ очереди чувствителен к регистру символов.

## Формат ответа {#section_xc3_53j_p1b}

```json
{
    "self": "{{ host }}/v2/queues/TEST",
    "id": 3,
    "key": "TEST",
    "version": 5,
    "name": "Test",
    "lead": {
           "self": "{{ host }}/v2/users/1120000000016876",
           "id": "<id сотрудника>",
           "display": "<отображаемое имя сотрудника>"
    },
    "assignAuto": false,
    "defaultType": {
           "self": "{{ host }}/v2/issuetypes/1",
           "id": "1",
           "key": "bug",
           "display": "Ошибка"
    },
    "defaultPriority": {
           "self": "{{ host }}/v2/priorities/3",
           "id": "3",
           "key": "normal",
           "display": "Средний"
    },
    "denyVoting": false
}
```

#### Параметры ответа {#answer-params}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Ссылка на очередь. | Строка
id | Идентификатор очереди. | Строка
key | Ключ очереди. | Строка
version | Версия очереди. Каждое изменение очереди увеличивает номер версии. | Число
name | Название очереди. | Строка
[lead](#lead) | Блок с информацией о владельце очереди. | Объект
assignAuto` | Автоматически
 назначить исполнителя для новых задач очереди:<br/><br/>`true`— назначить.<br/><br/>`false`— не назначать. | Логический
[defaultType](#default-type) | Блок с информацией о типе задачи по умолчанию. | Объект
[defaultPriority](#default-priority) | Блок с информацией о приоритете задачи по умолчанию. | Объект
denyVoting | Признак возможности голосования за задачи. | Логический

**Поля объекта** `lead` {#lead}

Параметр | Описание | Тип данных
-------- | -------- | ----------
self | Ссылка на пользователя. | Строка
id | Идентификатор пользователя. | Строка
display | Отображаемое имя пользователя. | Строка

**Поля объекта** `defaultType` {#default-type}

Параметр | Описание | Тип данных
-------- | -------- | ----------
self | Ссылка на тип задачи. | Строка
id | Идентификатор типа задачи. | Строка
key | Ключ типа задачи. | Строка
display | Отображаемое название типа задачи. | Строка

**Поля объекта** `defaultPriority` {#default-priority}

Параметр | Описание | Тип данных
-------- | -------- | ----------
self | Ссылка на тип приоритета. | Строка
id | Идентификатор приоритета. | Строка
key | Ключ приоритета. | Строка
display | Отображаемое название приоритета. | Строка

## Возможные коды ответа {#section_otf_jrj_p1b}

200
:   Запрос выполнен успешно.

404
:   Запрошенный объект не был найден. Возможно, вы указали неверное значение идентификатора или ключа объекта.

