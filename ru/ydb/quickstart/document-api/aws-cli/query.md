---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Выборка данных

Чтобы выбрать данные из таблицы `series` по ключу `series_id`:

{% list tabs %}

* AWS CLI

    Выполните команду, заменив `https://your-database-endpoint` эндпоинтом вашей БД:

    {% note warning %}

    Для работы с AWS CLI из Windows рекомендуется использовать [WSL](https://docs.microsoft.com/ru-ru/windows/wsl/).

    {% endnote %}

    ```bash
    endpoint="https://your-database-endpoint"
    aws dynamodb query \
        --table-name series \
        --key-condition-expression "series_id = :name" \
        --expression-attribute-values '{":name":{"N":"2"}}' \
        --endpoint $endpoint
    ```

   Результат выполнения:

    ```text
    {
        "Items": [
            {
                "series_id": {
                    "N": ".2e1"
                },
                "title": {
                    "S": "Silicon Valley"
                },
                "release_date": {
                    "S": "2014-04-06"
                },
                "series_info": {
                    "S": "Silicon Valley is an American comedy television series created by Mike Judge, John Altschuler and Dave Krinsky. The series focuses on five young men who founded a startup company in Silicon Valley."
                }
            }
        ],
        "Count": 1,
        "ScannedCount": 1,
        "ConsumedCapacity": null
    }
    ```
