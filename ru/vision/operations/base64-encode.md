---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Кодирование файла в Base64

Чтобы передать файл с изображением в {{ vision-short-name }} API, переведите содержимое файла в текст в формате Base64:

{% include [base64-encode-command](../../_includes/vision/base64-encode-command.md) %}

Передайте содержимое созданного файла `output.txt` в теле запроса в свойстве `content`:

```json
{
    "folderId": "b1gvmob95yysaplct532",
    "analyze_specs": [{
        "content": "iVBORw0KGgo...",
        ...
    }]
}

```