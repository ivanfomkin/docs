---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Импортировать файлы

{% note warning %}

Запрос может быть выполнен только если у пользователя есть право на изменение задачи, к которой прикреплены файлы.

{% endnote %}

С помощью запроса вы можете вы можете импортировать в {{ tracker-name }} файлы, прикрепленные к задаче и комментариям под ней.

## Формат запроса {#section_i14_lyb_p1b}

Чтобы импортировать файл, используйте HTTP-запрос с методом `POST`. Файл передается в теле запроса с использованием `multipart/form-data`[RFC-7578]({{ link-rfc7578 }}). Размер файла не должен превышать 1024 Мбит.

{% list tabs %}

- Прикрепить файл к задаче
   
    ```json
    POST /{{ ver }}/issues/<issue_id>/attachments/_import?filename={filename}&createdAt={createdAt}&createdBy={createdBy} 
    Host: {{ host }}
    Authorization: OAuth <токен>
    {{ org-id }}
    Content-Type: multipart/form-data
    <file_data>
    ```
    {% include [headings](../../../_includes/tracker/api/headings.md) %}
    #### Ресурс {#resource}
       
    - **<issue_id>**
        
        Ключ задачи, к которой будет прикреплен файл.
    - **<comment_id>**

        Идентификатор комментария, к которому будет прикреплен файл.

    #### Параметры запроса {#request-parametres}

    - **filename**

       Имя файла, максимальная длина - 255 символов.

    - **createdAt**

       Дата и время прикрепления файла в формате `YYYY-MM-DDThh:mm:ss.sss±hhmm`. Вы можете указать любое значение в интервале времени от создания до последнего обновления задачи.

    - **createdBy**

       Логин или идентификатор автора прикрепленного файла.

 

    - **Content-Type**

        Формат тела запроса. Должен иметь значение `multipart/form-data`.

    #### Тело запроса {#request-body}

    -  **<file_data>**

        Файл в бинарном формате. Размер файла не должен превышать 1024 Мбит.

- Прикрепить файл к комментарию

    ```json
    POST /{{ ver }}/issues/<issue_id>/comments/<comment_id>/attachments/_import?filename={filename}&createdAt={createdAt}&createdBy={createdBy} 
    Host: {{ host }}
    Authorization: OAuth <токен>
    {{ org-id }}
    Content-Type: multipart/form-data
    <file_data>
    ```

    #### Ресурс {#resource}
       
    - **<issue_id>**
        
        Ключ задачи, к которой будет прикреплен файл.
    - **<comment_id>**

        Идентификатор комментария, к которому будет прикреплен файл.

    #### Параметры запроса {#request-parametres}

    - **filename**

       Имя файла, максимальная длина - 255 символов.

    - **createdAt**

       Дата и время прикрепления файла в формате `YYYY-MM-DDThh:mm:ss.sss±hhmm`. Вы можете указать любое значение в интервале времени от создания до последнего обновления задачи.

    - **createdBy**

       Логин или идентификатор автора прикрепленного файла.

    #### Заголовки запроса {#request-headers}

    - **Host**

        Адрес узла, предоставляющего API:
        ```
        {{ host }}
        ```

    - **Authorization**

        OAuth-токен в формате `OAuth <значение токена>`, например:
        ```
        OAuth 0c4181a7c2cf4521964a72ff57a34a07
        ```
    - **X-Org-ID**

        Идентификатор организации.

    - **Content-Type**

        Формат тела запроса. Должен иметь значение `multipart/form-data`.

    #### Тело запроса {#request-body}

    -  **<file_data>**

        Файл в бинарном формате. Размер файла не должен превышать 1024 Мбит.

{% endlist %}

## Формат ответа {#section_xc3_53j_p1b}

{% list tabs %}

- Запрос выполнен успешно

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

    #### Параметры ответа {#answer-parametres}
    
    Параметр | Описание | Тип данных
    -------- | -------- | ----------
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
    -------- | -------- | ----------
    self | Адрес ресурса, соответствующего пользователю, загрузившему файл. | Строка
    id | Логин пользователя. | Строка
    display | Имя пользователя (как в интерфейсе). | Строка


    **Поля объекта** `metadata` {#metadata}

    Параметр | Описание | Тип данных
    -------- | -------- | ----------
    size | Размер изображения в пикселях. | Строка

- Запрос выполнен с ошибкой

    Если запрос не был успешно обработан, ответное сообщение содержит информацию о возникших ошибках:
    
    HTTP-код ошибки | Описание ошибки
    --------------- | ---------------
    400 Bad Request | Один из параметров запроса имеет недопустимое значение или формат данных.
    403 Forbidden | У пользователя или приложения нет прав на доступ к ресурсу, запрос отклонен.
    404 Not Found | Запрашиваемый ресурс не найден.
    413 Request Entity Too Large | Размер файла превышает 1024 Мбит.
    422 Unprocessable Entity | Ошибка валидации, запрос отклонен.
    500 Internal Server Error | Внутренняя ошибка сервиса. Попробуйте повторно отправить запрос через некоторое время.
    503 Service Unavailable | Сервис API временно недоступен.

{% endlist %}