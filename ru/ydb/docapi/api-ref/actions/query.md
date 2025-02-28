---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Метод Query

Находит элементы на основе заданных значений первичного ключа.

В параметре `KeyConditionExpression` задается условие, определяющее значения ключей разделов выбираемых элементов. Чтобы сузить область поиска, можно указать значение ключа сортировки и оператор сравнения.

Для дальнейшей фильтрации результатов используется `FilterExpression`. Это условие применяется после первоначальной выборки, но до финального возврата результатов. В этом параметре нельзя указывать атрибуты ключа раздела или сортировки. Эти атрибуты необходимо указывать `KeyConditionExpression`.

Операция всегда возвращает набор результатов. Если подходящие элементы не найдены, набор результатов будет пустым. Пустые запросы потребляют минимальное количество единиц емкости чтения для этого типа операции чтения.

Единицы потребляемой мощности рассчитываются на основе размера элемента, а не объема данных. Количество потребляемых единиц мощности не зависит от того, запрашиваете ли вы все атрибуты или часть.

Результаты всегда сортируются по значению ключа сортировки. Если у ключа сортировки числовой тип данных, то результаты возвращаются в числовом порядке; в остальных случаях результаты сортируются в порядке байтов UTF-8. 
Порядок сортировки задается параметром `ScanIndexForward`.

За один раз метод считывает максимум 1 Мб данных или то количество элементов, которое указано в параметре `Limit`. И только затем применяются фильтры, указанные в параметре `FilterExpression`.

По умолчанию метод выполняет последовательное чтение из таблицы. Если нужно использовать строгое согласованное чтение, то необходимо установить параметр `ConsistentRead=true`.

## Запрос

Запрос содержит данные в формате JSON.

```json
{
   "AttributesToGet": [ "string" ],
   "ConditionalOperator": "string",
   "ConsistentRead": boolean,
   "ExclusiveStartKey": { 
      "string" : { 
         "B": blob,
         "BOOL": boolean,
         "BS": [ blob ],
         "L": [ 
            "AttributeValue"
         ],
         "M": { 
            "string" : "AttributeValue"
         },
         "N": "string",
         "NS": [ "string" ],
         "NULL": boolean,
         "S": "string",
         "SS": [ "string" ]
      }
   },
   "ExpressionAttributeNames": { 
      "string" : "string" 
   },
   "ExpressionAttributeValues": { 
      "string" : { 
         "B": blob,
         "BOOL": boolean,
         "BS": [ blob ],
         "L": [ 
            "AttributeValue"
         ],
         "M": { 
            "string" : "AttributeValue"
         },
         "N": "string",
         "NS": [ "string" ],
         "NULL": boolean,
         "S": "string",
         "SS": [ "string" ]
      }
   },
   "FilterExpression": "string",
   "KeyConditionExpression": "string",
   "KeyConditions": { 
      "string" : { 
         "AttributeValueList": [ 
            { 
               "B": blob,
               "BOOL": boolean,
               "BS": [ blob ],
               "L": [ 
                  "AttributeValue"
               ],
               "M": { 
                  "string" : "AttributeValue"
               },
               "N": "string",
               "NS": [ "string" ],
               "NULL": boolean,
               "S": "string",
               "SS": [ "string" ]
            }
         ],
         "ComparisonOperator": "string"
      }
   },
   "Limit": number,
   "ProjectionExpression": "string",
   "QueryFilter": { 
      "string" : { 
         "AttributeValueList": [ 
            { 
               "B": blob,
               "BOOL": boolean,
               "BS": [ blob ],
               "L": [ 
                  "AttributeValue"
               ],
               "M": { 
                  "string" : "AttributeValue"
               },
               "N": "string",
               "NS": [ "string" ],
               "NULL": boolean,
               "S": "string",
               "SS": [ "string" ]
            }
         ],
         "ComparisonOperator": "string"
      }
   },
   "ReturnConsumedCapacity": "string",
   "ScanIndexForward": boolean,
   "Select": "string",
   "TableName": "string"
}
```

### Параметры

Параметр | Описание
----- | -----
`TableName` | Имя таблицы, содержащей запрашиваемые элементы.<br/>Может содержать путь в иерархии каталогов вида path/to/table.<br/><br/>**Тип**: Строка<br/>**Длина**: 3 - 255 символов<br/>**Шаблон**: [a-zA-Z0-9_.-]+<br/>**Обязательно**: Да
`ConsistentRead` | Определение модели согласованности чтения.<br/>Если `true`, то используется строго согласованное чтение; если `false` (по умолчанию), то используется последовательное чтение.<br/>Параметр не поддерживается для глобальных вторичных индексов. Если попытаться просканировать вторичный индекс со значением `true`, то метод вернет исключение `ValidationException`.<br/><br/>**Тип**: Boolean<br/>**Обязательно**: Нет
`ExclusiveStartKey` | Первичный ключ элемента, с которого метод начнет поиск.<br/>Если в предыдущем запросе метод вернул `LastEvaluatedKey`, то используйте это значение чтобы продолжить поиск с того места, на котором метод остановился в прошлый раз.<br/><br/>**Тип**: Объект типа `AttributeValue`<br/>**Длина ключа**: максимальная длина 65535.<br/>**Обязательно**: Нет
`ExpressionAttributeNames` | Заполнитель (placeholder), который можно использовать в выражении вместо имени атрибута. Заполнитель должен начинаться с символа решетки `#`.<br/> В каких случаях это может пригодиться:<ul><li>Если нужно указать атрибут, имя которого конфликтует с зарезервированным словом.<li>В качестве переменной, если имя атрибута используется в выражении несколько раз.<li>Для предотвращения неправильной интерпретации специальных символов в имени атрибута.</ul>Например, имя атрибута `Percentile` конфликтует с зарезервированным словом, и его нельзя в явном виде использовать в выражении. Чтобы обойти эту проблему, нужно в параметре `ExpressionAttributeNames` указать заполнитель: `{"#P":"Percentile"}`. И затем вместо настоящего имени атрибута использовать `#P`.<br/><br/>**Тип**: Строка<br/>**Длина**: 1 - 65535 символов.<br/>**Обязательно**: Нет
`ExpressionAttributeValues` | Заполнитель (placeholder), который можно использовать в выражении вместо значения атрибута, аналогично `ExpressionAttributeNames`. Заполнитель должен начинаться с символа двоеточия `:`.<br/>Например, нужно проверить, было ли значение атрибута `ProductStatus` одним из следующих: `Available | Backordered | Discontinued`. Для этого сначала объявить заполнители : `{ ":avail":{"S":"Available"}, ":back":{"S":"Backordered"}, ":disc":{"S":"Discontinued"} }`. А потом их можно использовать в выражении: `ProductStatus IN (:avail, :back, :disc)`<br/><br/>**Тип**: Строка типа `AttributeValue`<br/>**Обязательно**: Нет
`FilterExpression` | Условия, которые применятся после первоначальной выборки данных.<br/>Элементы, не соответствующие этому условию, не вернутся в итоговом ответе.<br/>**Тип**: Строка<br/>**Обязательно**: Нет
`KeyConditionExpression` | Условие, определяющее значения ключей выбираемых элементов.<br/>Условие должно выполнять проверку на равенство для одного значения ключа раздела.<br/>Дополнительно можно выполнить сравнение для одного значения ключа сортировки. Это позволяет получить элемент с заданным значением ключа раздела и значением ключа сортировки или несколько элементов, которые имеют одинаковое значение ключа раздела, но разные значения ключа сортировки.<br/>Проверку на равенство необходимо указывать в формате: `partitionKeyName = :partitionkeyval`.<br/>Если нужно указать условие для ключа сортировки, его необходимо объединить с условием для ключа сортировки, например: `partitionKeyName = :partitionkeyval AND sortKeyName = :sortkeyval`.<br/>Возможные сравнения для условия ключа сортировки:<ul><li>`sortKeyName = :sortkeyval` — истина, если значение ключа сортировки равно `:sortkeyval`.<li>`sortKeyName < :sortkeyval` — истина, если значение ключа сортировки меньше `:sortkeyval`.<li>`sortKeyName <= :sortkeyval` — истина, если значение ключа сортировки меньше или равно `:sortkeyval`.<li>`sortKeyName > :sortkeyval` — истина, если значение ключа сортировки больше `:sortkeyval`.<li>`sortKeyName >= :sortkeyval` — истина, если значение ключа сортировки больше или равно `:sortkeyval`.<li>`sortKeyName BETWEEN :sortkeyval1 AND :sortkeyval2` — истина, если значение ключа сортировки больше или равно `:sortkeyval1` и меньше или равно `:sortkeyval2`.<li>`begins_with ( sortKeyName, :sortkeyval )` — истина, если значение ключа сортировки начинается с определенного операнда. Функцию нельзя использовать с ключом сортировки числового типа. Имя функции чувствительно к регистру.</ul><br/>**Тип**: Строка<br/>**Обязательно**: Нет
`Limit` | Максимальное количество элементов, которые будут оценены для выборки.<br/>Когда метод обработает указанное количество элементов, он останавливается и возвращает результат до того места, на котором остановился. При этом в параметре `LastEvaluatedKey` вернется последний ключ, на котором он остановился. Его можно использовать чтобы продолжить сканирование с того места, на котором остановился метод.<br/><br/>**Тип**: Целое число<br/>**Диапазон**: минимальное значение 1.<br/>**Обязательно**: Нет
`ProjectionExpression` | Выражение, определяющие атрибуты для извлечения. Атрибуты в выражении должны быть разделены запятыми.<br/>Если имена атрибутов не указаны явно, то возвращаются все атрибуты элемента.<br/><br/>**Тип**: Строка<br/>**Обязательно**: Нет
`ReturnConsumedCapacity` | Нужно ли возвращать информацию о потребляемой мощности.<ul><li>`TOTAL` - Вернуть информацию.<li>`NONE` - Не возвращать информацию.</ul><br/>**Тип**: Строка<br/>**Возможные значения**: `TOTAL | NONE`<br/>**Обязательно**: Нет
`ScanIndexForward` | Задает порядок обхода индекса.<ul><li>`true` — обход выполняется в возрастающем порядке (по умолчанию)<li>`false` — обход выполняется в порядке убывания.</ul><br/>**Тип**: логический<br/>**Обязательно**: Нет
`Select` | Атрибуты, которые нужно вернуть.<br/>Может принимать значения:<ul><li>ALL_ATTRIBUTES — возвращает все атрибуты элемента из таблицы или индекса (по умолчанию).<li>COUNT — возвращает только количество совпадающих атрибутов.</ul><br/>**Тип**: Строка<br/>**Допустимые значения**: `ALL_ATTRIBUTES | COUNT`<br/>**Обязательно**: Нет

## Ответ

В случае успеха вернется HTTP с кодом 200.
Запрос возвращает данные в формате JSON.

```json
{
   "ConsumedCapacity": { 
      "CapacityUnits": number,
      "GlobalSecondaryIndexes": { 
         "string" : { 
            "CapacityUnits": number,
            "ReadCapacityUnits": number,
            "WriteCapacityUnits": number
         }
      },
      "LocalSecondaryIndexes": { 
         "string" : { 
            "CapacityUnits": number,
            "ReadCapacityUnits": number,
            "WriteCapacityUnits": number
         }
      },
      "ReadCapacityUnits": number,
      "Table": { 
         "CapacityUnits": number,
         "ReadCapacityUnits": number,
         "WriteCapacityUnits": number
      },
      "TableName": "string",
      "WriteCapacityUnits": number
   },
   "Count": number,
   "Items": [ 
      { 
         "string" : { 
            "B": blob,
            "BOOL": boolean,
            "BS": [ blob ],
            "L": [ 
               "AttributeValue"
            ],
            "M": { 
               "string" : "AttributeValue"
            },
            "N": "string",
            "NS": [ "string" ],
            "NULL": boolean,
            "S": "string",
            "SS": [ "string" ]
         }
      }
   ],
   "LastEvaluatedKey": { 
      "string" : { 
         "B": blob,
         "BOOL": boolean,
         "BS": [ blob ],
         "L": [ 
            "AttributeValue"
         ],
         "M": { 
            "string" : "AttributeValue"
         },
         "N": "string",
         "NS": [ "string" ],
         "NULL": boolean,
         "S": "string",
         "SS": [ "string" ]
      }
   },
   "ScannedCount": number
}
```

### Параметры

Параметр | Описание
----- | -----
`ConsumedCapacity` | Единицы мощности, потребленные операцией удаления.<br/>Возвращается только в том случае, если в запросе был указан параметр `ReturnConsumedCapacity` со значением `TOTAL`.<br/><br/>**Тип**: объект типа `ConsumedCapacity`
`Count` | Количество элементов в ответе.<br/>Если в запросе вы использовали `FilterExpression`, тогда это количество элементов, возвращенных после применения фильтра.<br/><br/>**Тип**: целое число
`Items` | Массив атрибутов, подходящих под критерии сканирования.<br/>Каждый элемент в массиве состоит из имени и значения этого атрибута.<br/><br/>**Тип**: массив объектов типа `AttributeValue`<br/>**Длина ключа**: 1 - 65535 символов.
`LastEvaluatedKey` | Первичный ключ элемента, на котором остановилось сканирование. Используйте это значение, чтобы продолжить с того места, на котором остановились. Если в `LastEvaluatedKey` пусто, значит метод обработал все элементы и больше нечего возвращать.<br/><br/>**Тип**: ассоциативный массив типа `AttributeValue`<br/>**Длина ключа**: 1 - 65535 символов.
`ScannedCount` | Количество элементов, найденных до применения фильтров `FilterExpression`.<br/><br/>**Тип**: целое число

## Ошибки

Параметр | Описание
----- | -----
`InternalServerError` | Произошла внутренняя ошибка на стороне сервера.<br/><br/>**Код состояния HTTP**: 500<br/>
`ProvisionedThroughputExceededException` | Вы слишком часто отправляете запросы. Попробуйте увеличить интервалы между запросами.<br/>Если таких запросов будет не слишком много, {{ ydb-name }} постарается обработать их все.<br/><br/>**Код состояния HTTP**: 400
`RequestLimitExceeded` | Пропускная способность превышает квоту.<br/><br/>**Код состояния HTTP**: 400
`ResourceNotFoundException` | Указанная таблица не существует.<br/><br/>**Код состояния HTTP**: 400

Также могут возникать [Общие ошибки](../common-errors), одинаковые для всех методов.