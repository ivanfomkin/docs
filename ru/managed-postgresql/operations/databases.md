---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Управление базами данных

Вы можете добавлять и удалять базы данных, а также просматривать информацию о них.

{% include [db-sql](../../_includes/mdb/mdb-db-sql-limits.md) %}

## Получить список баз данных в кластере {#list-db}

{% list tabs %}

- Консоль управления

  1. Перейдите на страницу каталога и выберите сервис **{{ mpg-name }}**.
  1. Нажмите на имя нужного кластера, затем выберите вкладку **Базы данных**.


- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы получить список баз данных в кластере, выполните команду:

  ```
  $ {{ yc-mdb-pg }} database list
       --cluster-name <имя кластера>
  ```

  Имя кластера можно запросить со [списком кластеров в каталоге](cluster-list.md).


- API

  Получить список баз данных кластера можно с помощью метода [list](../api-ref/Database/list.md).

{% endlist %}

## Создать базу данных {#add-db}

В каждом кластере {{ mpg-name }} вы можете создать неограниченное количество баз данных.

{% list tabs %}

- Консоль управления

  Чтобы создать базу данных:

  1. Перейдите на страницу каталога и выберите сервис **{{ mpg-name }}**.
  1. Нажмите на имя нужного кластера.
  1. Если владельцем новой базы данных должен стать еще не существующий пользователь, [создайте его](cluster-users.md#adduser).
  1. Выберите вкладку **Базы данных**.
  1. Нажмите кнопку **Добавить**.
  1. Введите имя для базы данных, выберите ее владельца и задайте нужные локали сортировки и набора символов.

      {% include [db-name-limits](../../_includes/mdb/mpg/note-info-db-name-limits.md) %}

      {% include [postgresql-locale](../../_includes/mdb/mpg-locale-settings.md) %}

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы создать базу данных в кластере:

  1. Посмотрите описание команды CLI для создания БД:

     ```
     $ {{ yc-mdb-pg }} database create --help
     ```

  1. Запросите список пользователей кластера, чтобы выбрать владельца новой базы данных:

     ```
     $ {{ yc-mdb-pg }} user list
          --cluster-name <имя кластера>
     ```

     Если нужного пользователя в списке нет, [создайте его](cluster-users.md#adduser).

  1. Выполните команду создания БД. При необходимости укажите нужные локали сортировки и набора символов (по умолчанию задаются `LC_COLLATE=C` и `LC_CTYPE=C`):

     ```
     $ {{ yc-mdb-pg }} database create <имя базы данных>
          --cluster-name <имя кластера>
          --owner <имя пользователя-владельца>
          --lc-collate <локаль сортировки>
          --lc-type <локаль набора символов>
     ```

     {% include [db-name-limits](../../_includes/mdb/mpg/note-info-db-name-limits.md) %}

     {{ mpg-short-name }} запустит операцию создания базы данных.

  Имя кластера можно запросить со [списком кластеров в каталоге](cluster-list.md).

- Terraform
  
  Чтобы создать базу данных в кластере:
  
    1. Откройте актуальный конфигурационный файл {{ TF }} с планом инфраструктуры.
  
        О том, как создать такой файл, см. в разделе [{#T}](cluster-create.md).
  
    1. Добавьте к описанию кластера {{ mpg-name }} блок `database`. При необходимости укажите нужные локали сортировки и набора символов (по умолчанию задаются `LC_COLLATE=C` и `LC_CTYPE=C`):
  
        ```hcl
        resource "yandex_mdb_postgresql_cluster" "<имя кластера>" {
          ...
          database {
            name       = "<имя базы данных>"
            owner      = "<имя пользователя-владельца: должен быть задан в блоке user>"
            lc_collate = "<локаль сортировки>"
            lc_type    = "<локаль набора символов>"
            ...
          }
        }
        ```
  
        {% include [db-name-limits](../../_includes/mdb/mpg/note-info-db-name-limits.md) %}

    1. Проверьте корректность настроек.
  
        {% include [terraform-validate](../../_includes/mdb/terraform/validate.md) %}
  
    1. Подтвердите изменение ресурсов.
  
        {% include [terraform-apply](../../_includes/mdb/terraform/apply.md) %}
  
  Подробнее см. в [документации провайдера {{ TF }}]({{ tf-provider-mpg }}).

- API

  Создать новую базу данных в кластере можно с помощью метода [create](../api-ref/Database/create.md).

{% endlist %}

## Удалить базу данных {#remove-db}

{% list tabs %}

- Консоль управления

  1. Перейдите на страницу каталога и выберите сервис **{{ mpg-name }}**.
  1. Нажмите на имя нужного кластера и выберите вкладку **Базы данных**.
  1. Нажмите значок ![image](../../_assets/vertical-ellipsis.svg) в строке нужной БД и выберите пункт **Удалить**.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы удалить базу данных, выполните команду:

  ```
  $ {{ yc-mdb-pg }} database delete <имя базы данных>
       --cluster-name <имя кластера>
  ```

  Имя кластера можно запросить со [списком кластеров в каталоге](cluster-list.md).

- Terraform
  
  1. Откройте актуальный конфигурационный файл {{ TF }} с планом инфраструктуры.
  
     О том, как создать такой файл, см. в разделе [{#T}](cluster-create.md).
  
  1. Удалите из описания кластера {{ mpg-name }} блок `database` с именем удаляемой базы данных.
  
  1. Проверьте корректность настроек.
  
      {% include [terraform-validate](../../_includes/mdb/terraform/validate.md) %}
  
  1. Подтвердите изменение ресурсов.
  
      {% include [terraform-apply](../../_includes/mdb/terraform/apply.md) %}
  
  Подробнее см. в [документации провайдера {{ TF }}]({{ tf-provider-mpg }}).

- API

  Удалить базу данных можно с помощью метода [delete](../api-ref/Database/delete.md).

{% endlist %}

{% note warning %}

Прежде чем создать новую базу с тем же именем, дождитесь завершения операции удаления, иначе будет восстановлена удаляемая база. Статус операции можно получить вместе со [списком операций в кластере](cluster-list.md#list-operations).

{% endnote %}
