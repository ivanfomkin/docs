---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Обновление данных

Чтобы обновить данные в таблице `series`:

{% list tabs %}

* AWS CLI

    Выполните команду, заменив `https://your-database-endpoint` эндпоинтом вашей БД:

    {% note warning %}

    Для работы с AWS CLI из Windows рекомендуется использовать [WSL](https://docs.microsoft.com/ru-ru/windows/wsl/).

    {% endnote %}

    ```bash
    endpoint="https://your-database-endpoint"
    aws dynamodb update-item \
        --table-name series \
        --key '{"series_id": {"N": "2"}, "title": {"S": "Silicon Valley"}}' \
        --update-expression "SET series_info = :newval" \
        --expression-attribute-values '{":newval":{"S":"Silicon Valley is an American comedy television series created by Mike Judge, John Altschuler and Dave Krinsky. The series focuses on five young men who founded a startup company in Silicon Valley."}}' \
        --return-values ALL_NEW \
        --endpoint $endpoint
    ```

    Результат выполнения:

    ```text
    {
        "Attributes": {
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
    }
    ```
