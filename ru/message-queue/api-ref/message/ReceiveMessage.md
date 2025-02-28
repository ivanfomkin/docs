---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# ReceiveMessage

Метод для приема от одного до десяти сообщений из указанной очереди. С помощью параметра `WaitTimeSeconds` выполняются long-polling запросы.

Стандартное поведение метода — это short polling, при котором делается попытка получения сообщений из одного шарда очереди, выбранного при вызове `ReceiveMessage`. Если в очереди немного сообщений, будет возвращено меньшее количество сообщений, чем указано в параметре `MaxNumberOfMessages`. Если в очереди слишком мало сообщений, то в ответе на запрос может не вернуться ни одного сообщений, если они не попали в шард очереди. Если ни одно сообщение не удалось получить, повторите запрос.

Если при получении сообщений из пустой очереди в нее поступит новое сообщений, оно будет получено с задержкой на время одной попытки получения.

Для каждого из полученных сообщений возвращаются следующие параметры:

* `MessageId` — идентификатор сообщения.
* `ReceiptHandle` — идентификатор для удаления полученного сообщения или изменения его [таймаута видимости](../../concepts/visibility-timeout.md).
* `Body` — тело сообщения.
* `MD5OfBody` — MD5-хэш тела сообщения.
* `Attributes` — набор атрибутов сообщения, указывающих время отправки, количество приемов сообщения, время отправки.

При вызове метода можно передать параметр `VisibilityTimeout`, который установит получаемым сообщениям указанный таймаут видимости. Если параметр не задан, сообщения получат таймаут видимости, указанный для очереди по умолчанию.

При получении сообщений из очереди FIFO, из одной группы сообщений за один вызов `ReceiveMessage` будет принято только одно сообщение.

## Запрос {#request}

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный<br>параметр | Описание
----- | ----- | ----- | -----
`MaxNumberOfMessages` | **string** | Нет | Максимальное количество сообщений, которое будет принято. Возможные значения: от 1 до 10. Значение по умолчанию: 1.
`MessageAttributeName.N` | **array** | Нет | Массив имен атрибутов сообщения, которые требуется вернуть в ответе на запрос. Имя может содержать буквы и цифры, а также дефисы, нижние подчеркивания и точки. Имена атрибутов чувствительны к регистру и уникальны в пределах одного сообщения. Имена атрибутов не могут начинаться или оканчиваться точками. Имена атрибутов не должны содержать несколько точек подряд. Максимальная длина имени атрибута — 256 символов. Можно получить все атрибуты сразу, указав слово All или `.*` в запросе. Также можно использовать префиксы для получения нужных атрибутов.
`QueueUrl` | **string** | Да | URL очереди, в которой находится сообщение.
`ReceiveRequestAttemptId` | **string** | Нет | Идентификатор для повтора попытки получения сообщений из FIFO-очереди. Подробнее см. [Дедупликация](../../concepts/deduplication.md#request-attempts).
`VisibilityTimeout` | **string** | Нет | [Таймаут видимости](../../concepts/visibility-timeout.md) получаемого сообщения.
`WaitTimeSeconds` | **string** | Нет | Время ожидания доставки сообщения в очередь в секундах. Если в очереди появятся сообщения, вызов будет сделан раньше, чем указано в `WaitTimeSeconds`. Если сообщения не появились после истечения `WaitTimeSeconds` будет возвращен пустой список.

#### Атрибуты {#attributes}

Список имен атрибутов сообщения. Атрибуты передаются в параметре `Attributes`.

```
Attribute.N.Name (атрибут)
Attribute.N.Value (значение атрибута)
```

Атрибут | Описание
----- | -----
`All` | Все значения.
`ApproximateFirstReceiveTimestamp` | Время получения сообщения из очереди.
`ApproximateReceiveCount` | Число получений сообщения из очереди без его удаления.
`SenderId` | Идентификатор отправителя — субъекта IAM.
`SentTimestamp` | Время отправки сообщения в очередь.
`MessageDeduplicationId` | Идентификатор токена для дедупликации сообщений, используется в очередях FIFO. Каждое сообщение должно иметь уникальный `MessageDeduplicationId`. Если `MessageDeduplicationId` не указан, отправка сообщения в очередь не будет выполнена. Максимальная длина — 128 символов. Разрешено использование цифр, больших и маленьких латинских букв и знаков пунктуации. Подробнее см. [Дедупликация](../../concepts/deduplication.md).
`MessageGroupId` | Идентификатор группы сообщений, используется в очередях FIFO. Подробнее см. [Дедупликация](../../concepts/deduplication.md).
`SequenceNumber` | Номер сообщения, используется в очередях FIFO в рамках группы сообщений с одинаковым MessageGroupId.

## Ответ {#response}

### Поля успешного ответа {#response-parameters}

Поле | Тип | Описание
----- | ----- | -----
`Message` | **array** | Массив [Message](../data-types/Message.md).

### Ошибки ReceiveMessage {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [{#T}](../common-errors.md).

Код HTTP | Идентификатор ошибки | Описание
----- | ----- | -----
403 | `OverLimit` | Операция превысила один из установленных [лимитов](../../concepts/limits.md).

## Пример запроса {#request-example}

```
Action=ReceiveMessage
&Version=2012-11-05
&QueueUrl=https://message-queue.api.cloud.yandex.net/b1g8ad42m6he1ooql78r/dj600000000000le07ol/sample-queue
&AttributeName.1=All
&MessageAttributeName.1=All
&VisibilityTimeout=15
```

Подробнее о формировании запросов см. в разделе [Общий вид запросов к API](../index.md#api-request).

## Пример ответа {#response-example}

```xml
<ReceiveMessageResponse>
    <ReceiveMessageResult>
        <Message>
            <MessageId>cddcbbe4-b0571f5c-d7b94ce4-1523191</MessageId>
            <ReceiptHandle>EAEgrOGOhogtKAA</ReceiptHandle>
            <MD5OfBody>3e25960a79dbc69b674cd4ec67a72c62</MD5OfBody>
            <Body>Hello world</Body>
            <Attribute>
                <Name>ApproximateFirstReceiveTimestamp</Name>
                <Value>1548348534956</Value>
            </Attribute>
            <Attribute>
                <Name>ApproximateReceiveCount</Name>
                <Value>1</Value>
            </Attribute>
            <Attribute>
                <Name>SentTimestamp</Name>
                <Value>1548347797419</Value>
            </Attribute>
        </Message>
    </ReceiveMessageResult>
    <ResponseMetadata>
        <RequestId>213c792a-2afa2234-4759dbc3-e5b8ef8-fc90fde14cdc1371b11d6453cc55a75b</RequestId>
    </ResponseMetadata>
</ReceiveMessageResponse>
```
