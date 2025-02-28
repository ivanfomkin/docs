---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Создание пользовательского сертификата

Чтобы создать пользовательский сертификат:

{% list tabs %}

- Консоль управления

    1. В [консоли управления]({{ link-console-main }}) выберите каталог, в котором будет создан сертификат.
    1. В списке сервисов выберите **{{ certificate-manager-name }}**.
    1. Нажмите кнопку **Добавить сертификат**.
    1. В открывшемся меню выберите **Пользовательский сертификат**.
    1. В открывшемся окне в поле **Имя** введите имя сертифката.
    1. (опционально) В поле **Описание** введите описание сертификата.
    1. В поле **Сертификат** нажмите кнопку **Добавить сертификат**.
        1. Выберите способ добавления: **Файл** или **Текст**.
        1. Нажмите кнопку **Добавить**.
    1. В поле **Цепочка промежуточных сертификатов** нажмите кнопку **Добавить цепочку**.
        1. Выберите способ добавления: **Файл** или **Текст**.
        1. Нажмите кнопку **Добавить**.
    1. В поле **Приватный ключ** нажмите кнопку **Добавить приватный ключ**.
        1. Выберите способ добавления: **Файл** или **Текст**.
        1. Нажмите кнопку **Добавить**.
    1. Нажмите кнопку **Создать**.

- CLI

    {% include [cli-install](../../../_includes/cli-install.md) %}

    {% include [default-catalogue](../../../_includes/default-catalogue.md) %}

    1. Посмотрите описание команды:

        ```bash
        yc certificate-manager certificate create --help
        ```

    1. Выполните команду:

        ```bash
        yc certificate-manager certificate create \
          --name mycert \
          --chain mycert.pem \
          --key mykey.pem
        ```

        Параметры команды:

          - `--name` — имя сертификата.
          - `--chain` — путь к файлу цепочки сертификатов.
          - `--key` — путь к файлу закрытого ключа сертификата.

        Результат команды:

        ```bash
        id: fpqmg47avvimp7rvmp30
        folder_id: b1g7gvsi89m34qmcm3ke
        created_at: "2020-09-15T06:54:44.916325Z"
        name: mycert
        type: IMPORTED
        domains:
        - example.com
        status: ISSUED
        issuer: CN=example.com
        subject: CN=example.com
        serial: c32fd55592a376635fa53d9aea677caae6bf08f
        updated_at: "2020-09-15T06:54:44.916325Z"
        issued_at: "2020-09-15T06:54:44.916325Z"
        not_after: "2021-09-15T06:48:26Z"
        not_before: "2020-09-15T06:48:26Z"
        ```

- API
  
    Чтобы создать сертификат, воспользуйтесь методом [create](../../api-ref/Certificate/create.md) для ресурса [Certificate](../../api-ref/Certificate/).

{% endlist %}

В списке сертификатов появится новый сертификат со статусом `Issued`.
