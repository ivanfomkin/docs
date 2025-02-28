---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Перенести задачу в другую очередь

Запрос позволяет переместить задачу в другую очередь.

Перед выполнением запроса убедитесь, что пользователь имеет доступ к редактированию переносимых задач и их созданию в новой очереди.

{% note warning %}

Если переносимая задача имеет тип и статус, которые не существуют в новой очереди, перенос не будет выполнен. Чтобы при переносе сбросить статус задачи в начальное значение, используйте параметр `InitialStatus`.
 
По умолчанию при переносе очищаются значения компонентов, версий и проектов задачи. Если в новой очереди настроены аналогичные значения для этих полей, для переноса компонентов, версий и проектов используйте параметр `MoveAllFields`.

Если в задаче установлены значения [локальных полей](../../local-fields.md), при переносе в другую очередь они будут удалены.
 
{% endnote %}

## Формат запроса {#section_rnm_x4j_p1b}

Для переноса задачи используйте HTTP-запрос с методом `POST`:

```json
POST /{{ ver }}/issues/<issue-id>/_move?queue=<queue-id>
Host: {{ host }}
Authorization: OAuth <OAuth-токен>
{{ org-id }}
```
{% include [headings](../../../_includes/tracker/api/headings.md) %}

#### Параметры запроса {#req-get-params}

**Ресурс**

Параметр | Описание | Тип данных
----- | ----- | -----
\<issue-id\> | Обязательный параметр. Идентификатор перемещаемой задачи. | Строка

**Обязательные параметры**

Параметр | Описание | Тип данных
----- | ----- | -----
\<queue-id\> | Обязательный параметр. Ключ очереди, в которую необходимо перенести задачу. | Строка

**Дополнительные параметры**

Параметр | Описание | Тип данных
----- | ----- | -----
notify | Признак уведомления об изменении задачи:<ul><li>`true` – (по умолчанию) пользователи, указанные в полях задачи, получат уведомления;</li><li>`false` – пользователи не получат уведомления.</li></ul> | Логический
notifyAuthor | Признак уведомления автора задачи:<ul><li>`true` – автор получит уведомление;</li><li>`false` (по умолчанию) – автор не получит уведомление.</li></ul> | Логический
moveAllFields | Перенос версий, компонентов и проектов задачи в новую очередь:<ul><li>`true` – перенести, если в новой очереди существуют соответствующие версии, компоненты, проекты;</li><li>`false` (по умолчанию) – очистить версии, компоненты, проекты.</li></ul> | Логический
initialStatus | Сброс статуса задачи в начальное значение. Статус необходимо сбросить, если задача переносится в очередь с другим [воркфлоу](../../manager/add-workflow.md):<ul><li>`true` – статус будет сброшен;</li><li>`false` (по умолчанию) – статус останется без изменений.</li></ul> | Логический
expand | Дополнительные поля, которые будут включены в ответ:<ul><li>`attachments` – вложения;</li><li>`comments` – комментарии;</li><li>`workflow` – воркфлоу задачи;</li><li>`transitions` – переходы по жизненному циклу.</li></ul> | Строка

#### Тело запроса {#req-body-params}

Тело запроса можно использовать в случае, если требуется изменить параметры переносимой задачи. Тело имеет такой же формат, как и при [редактировании задачи](patch-issue.md#req-body-params).

> Перенос задачи:
> 
> - Используется HTTP-метод POST.
> - Задача <q>TEST-1</q> перемещается в очередь <q>NEW</q>.
> 
> ```
> POST /v2/issues/TEST-1/_move?queue=NEW
> Host: {{ host }}
> Authorization: OAuth <OAuth-токен>
> {{ org-id }}
> ```

## Формат ответа {#section_xpm_q1y_51b}

```json
{
    "self": "{{ host }}/v2/issues/NEW-1",
    "id": "1a2345678b",
    "key": "NEW-1",
    "version": 2,
    "aliases": [
        "TEST-1"
    ],
    "previousQueue": {
        "self": "{{ host }}/v2/queues/TEST",
        "id": "3",
        "key": "TEST",
        "display": "TEST"
    },
    "description": "<описание задачи>",
    "type": {
        "self": "{{ host }}/v2/issuetypes/2",
        "id": "2",
        "key": "task",
        "display": "Задача"
    },
    "createdAt": "2020-09-04T14:18:56.776+0000",
    "updatedAt": "2020-11-12T12:38:19.040+0000",
    "lastCommentUpdatedAt": "2020-10-18T13:33:44.291+0000",
    },
    "summary": "Тест",
    "updatedBy": {
        "self": "{{ host }}/v2/users/1234567890",
        "id": "1234567890",
        "display": "Имя Фамилия"
    },
    "priority": {
        "self": "{{ host }}/v2/priorities/3",
        "id": "3",
        "key": "normal",
        "display": "Средний"
    },
    "followers": [
        {
            "self": "{{ host }}/v2/users/1234567890",
            "id": "1234567890",
            "display": "Имя Фамилия"
        }
    ],
    "createdBy": {
        "self": "{{ host }}/v2/users/1234567890",
        "id": "1234567890",
        "display": "Имя Фамилия"
    },
    "assignee": {
        "self": "{{ host }}/v2/users/1234567890",
        "id": "1234567890",
        "display": "Имя Фамилия"
    },
    "queue": {
        "self": "{{ host }}/v2/queues/NEW",
        "id": "5",
        "key": "NEW",
        "display": "Очередь"
    },
    "status": {
        "self": "{{ host }}/v2/statuses/8",
        "id": "1",
        "key": "open",
        "display": "Открыт"
    },
    "previousStatus": {
        "self": "{{ host }}/v2/statuses/1",
        "id": "1",
        "key": "open",
        "display": "Открыт"
    },
    "favorite": false
}
```

#### Параметры ответа {#answer-params}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса API, который содержит информацию о задаче. | Строка
id | Идентификатор задачи. | Строка
key | Ключ задачи. | Строка
version | Версия задачи. Каждое изменение параметров задачи увеличивает номер версии. | Число
aliases | Массив с информацией об альтернативных ключах задачи. | Массив строк
[previousQueue](#previous-queue) | Объект с информацией о предыдущей очереди задачи. | Объект
description | Описание задачи. | Строка
[type](#type) | Объект с информацией о типе задачи. | Объект
createdAt | Дата и время создания задачи. | Строка
updatedAt | Дата и время обновления задачи. | Строка
lastCommentUpdatedAt | Дата и время последнего добавленного комментария. | Строка
summary | Название задачи. | Строка
[updatedBy](#updated-by) | Объект с информацией о последнем пользователе, изменявшим задачу. | Объект
[priority](#priority) | Объект с информацией о приоритете. | Объект
[followers](#followers) | Массив объектов с информацией о наблюдателях задачи. | Массив строк
[createdBy](#created-by) | Объект с информацией о создателе задачи. | Объект
[assignee](#assignee) | Объект с информацией об исполнителе задачи. | Объект
[queue](#queue) | Объект с информацией об очереди задачи. | Объект
[status](#status) | Объект с информацией о статусе задачи. | Объект
[previousStatus](#previous-status) | Объект с информацией о предыдущем статусе задачи. | Объект
favorite | Признак избранной задачи:<ul><li>`true` – уведомления отключены;</li><li>`false` – уведомления включены.</li></ul> | Логический

**Поля объекта** `previousQueue` {#previous-queue}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса API, который содержит информацию об очереди. | Строка
id | Идентификатор очереди. | Число
key | Ключ очереди. | Строка
display | Отображаемое название очереди. | Строка

**Поля объекта** `type` {#type}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса API, который содержит информацию о типе задачи. | Строка
id | Идентификатор типа задачи. | Число
key | Ключ типа задачи. | Строка
display | Отображаемое название типа задачи. | Строка

**Поля объекта** `updatedBy` {#updated-by}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса API, который содержит информацию о пользователе. | Строка
id | Идентификатор пользователя. | Число
display | Отображаемое имя пользователя. | Строка

**Поля объекта** `priority` {#priority}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса API, который содержит информацию о приоритете. | Строка
id | Идентификатор типа приоритета. | Число
key | Ключ типа приоритета. | Строка
display | Отображаемое название типа приоритета. | Строка

**Поля массива объектов** `followers` {#followers}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса API, который содержит информацию о пользователе. | Строка
id | Идентификатор пользователя. | Число
display | Отображаемое имя пользователя. | Строка

**Поля объекта** `createdBy` {#created-by}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса API, который содержит информацию о пользователе. | Строка
id | Идентификатор пользователя. | Число
display | Отображаемое имя пользователя. | Строка

**Поля объекта** `assignee` {#assignee}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса API, который содержит информацию о пользователе. | Строка
id | Идентификатор пользователя. | Число
display | Отображаемое имя пользователя. | Строка

**Поля объекта** `queue` {#queue}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса API, который содержит информацию об очереди. | Строка
id | Идентификатор очереди. | Число
key | Ключ очереди. | Строка
display | Отображаемое название очереди. | Строка

**Поля объекта** `status` {#status}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса API, который содержит информацию о статусе. | Строка
id | Идентификатор статуса. | Число
key | Ключ типа статуса. | Строка
display | Отображаемое название типа статуса. | Строка

**Поля объекта** `previousStatus` {#previousStatus}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса API, который содержит информацию о статусе. | Строка
id | Идентификатор статуса. | Число
key | Ключ типа статуса. | Строка
display | Отображаемое название типа статуса. | Строка

## Возможные коды ответа {#section_otf_jrj_p1b}

200
:   Запрос выполнен успешно.

401
:   Пользователь не авторизован. Проверьте, были ли выполнены действия, описанные в разделе [{#T}](../access.md).

403
:   У вас не хватает прав на выполнение этого действия. Наличие прав можно перепроверить в интерфейсе {{ tracker-name }} — для выполнения действия при помощи API и через интерфейс требуются одинаковые права.

404
:   Запрошенный объект не был найден. Возможно, вы указали неверное значение идентификатора или ключа объекта.

