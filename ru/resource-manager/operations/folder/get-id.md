---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Получение идентификатора каталога

{% list tabs %}

- Консоль управления

  1. Откройте страницу каталога. Вы можете выбрать каталог на [стартовой странице]({{ link-console-main }}) консоли управления. На этой странице отображаются каталоги для выбранного облака. Если необходимо, [переключитесь на другое облако](../cloud/switch-cloud.md).
  1. Получите идентификатор каталога из URL страницы каталога в консоли управления:
      ```
      https://console.cloud.yandex.ru/folders/b1gd129pp9ha0vnvf5g7
      ```
      `b1gd129pp9ha0vnvf5g7` — это идентификатор каталога.

- CLI

  Если вы знаете имя каталога, получите его идентификатор с помощью команды `get`:

  ```
  $ yc resource-manager folder get my-folder

  id: b1gd129pp9ha0vnvf5g7
  ...
  ```

  Если вы не знаете имя каталога, получите список каталогов с идентификаторами для облака по умолчанию:

  ```
  $ yc resource-manager folder list

  +----------------------+--------------------+------------------+--------+
  |          ID          |        NAME        |      LABELS      | STATUS |
  +----------------------+--------------------+------------------+--------+
  | b1gd129pp9ha0vnvf5g7 | my-folder          |                  | ACTIVE |
  | b1g66mft1vopnevbn57j | default            |                  | ACTIVE |
  +----------------------+--------------------+------------------+--------+
  ```

  Чтобы посмотреть список каталогов в другом облаке, укажите идентификатор каталога в `cloud-id`:

  ```
  $ yc resource-manager folder list --cloud-id b1glku4lgd6g31h5onqs
  ```

- API

  Чтобы получить список каталогов с идентификаторами, воспользуйтесь методом [list](../../api-ref/Folder/list.md) для ресурса [Folder](../../api-ref/Folder/index.md).

{% endlist %}
