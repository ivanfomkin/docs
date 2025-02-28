---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Прикрепить файл

Запрос позволяет прикрепить файл к задаче.

## Формат запроса {#section_rnm_x4j_p1b}

Чтобы прикрепить файл, используйте HTTP-запрос с методом `POST`:

```
POST /{{ ver }}/issues/<issue-id>/attachments/?filename=<новое имя файла>
Host: {{ host }}
Authorization: OAuth <OAuth-токен>
{{ org-id }}
Content-Type: multipart/form-data

<file_data>

```

{% include [headings](../../../_includes/tracker/api/headings.md) %}

- **Content-Type**

    Формат тела запроса. Должен иметь значение `multipart/form-data`.

#### Ресурс {#resource}

- **\<issue-id\>**

    Идентификатор или ключ задачи.

#### Параметры запроса {#req-params}

- **filename (необязательный)**

    Новое имя файла, с которым он будет храниться на сервере. Необязательный параметр.

#### Тело запроса {#req-body}

- **\<file_data\>**

    Файл в бинарном формате. Размер файла не должен превышать 1024 Мбит.

## Формат ответа {#section_xc3_53j_p1b}

В случае успешного выполнения запроса API возвращает ответ с кодом 201. Тело ответа содержит параметры прикрепленного файла в формате JSON:

```json
{
  "self" : "{{ host }}/v2/issues/JUNE-2/attachments/123",
  "id" : "123",
  "name" : "pic.png",
  "content" : "{{ host }}/v2/issues/JUNE-2/attachments/123/pic.png",
  "thumbnail" : "{{ host }}/v2/issues/JUNE-2/thumbnails/123",
  "createdBy" : {
    "self" : "{{ host }}/v2/users/12314567890",
    "id" : "1234567890",
    "display" : "<отображаемое имя сотрудника>"
  },
  "createdAt" : "2017-06-11T05:16:01.339+0000",
  "mimetype" : "image/png",
  "size" : 5678
  "metadata" : {
    "size" : "128x128"
  }
}
```

#### Параметры ответа {#answer-params}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса API, который соответствует прикрепленному файлу. | Строка
id | Уникальный идентификатор файла. | Строка
name | Имя файла. | Строка
content | Адрес ресурса для скачивания файла. | Строка
thumbnail | Адрес ресурса для скачивания миниатюры предпросмотра. Доступно только для графических файлов. | Строка
[createdBy](#createdBy) | Объект с информацией о пользователе, прикрепившем файл. | JSON-объект.
createdAt | Дата и время загрузки файла в формате:<br/>``` YYYY-MM-DDThh:mm:ss.sss±hhmm ``` | Строка
mimetype | Тип файла, например:<ul><li>`text/plain` — текстовый файл;</li><li>`image/png` — изображение в формате png.</li></ul> | Строка
size | Размер файла в байтах. | Целое число.
[metadata](#metadata) | Объект с метаданными файла. | JSON-объект.

**Поля объекта** `createdBy` {#createdBy}

Параметр | Описание | Тип данных
----- | ----- | -----
self | Адрес ресурса, соответствующего пользователю, загрузившему файл. | Строка
id | Логин пользователя. | Строка
display | Имя пользователя (как в интерфейсе). | Строка

**Поля объекта** `metadata` {#metadata}

Параметр | Описание | Тип данных
----- | ----- | -----
size | Размер изображения в пикселях. | Строка

## Возможные коды ответа {#section_otf_jrj_p1b}

201
:   В результате выполнения запроса с методом `POST` успешно создан новый объект.

404
:   Запрошенный объект не был найден. Возможно, вы указали неверное значение идентификатора или ключа объекта.

