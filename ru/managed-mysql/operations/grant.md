---
title: "Назначение привилегий и ролей пользователям MySQL"
description: "В Managed Service for MySQL привилегии — это атомарные полномочия пользователя в отношении отдельных объектов базы данных. Роли — это привилегии, предоставляемые пользователю в отношении всех пользовательских объектов какой-либо базы данных. Пользователи могут иметь разные наборы ролей для разных баз данных. Чтобы узнать подробнее про поддерживаемые роли, см. описание ролей."

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---


# Назначение привилегий и ролей пользователям

В **{{ mmy-name }}** _привилегии_ — это атомарные полномочия пользователя в отношении отдельных объектов базы данных. _Роли_ — это привилегии, предоставляемые пользователю в отношении всех пользовательских объектов какой-либо базы данных. Пользователи могут иметь разные наборы ролей для разных баз данных. Чтобы узнать подробнее про поддерживаемые роли, см. [описание ролей](#db-roles).

Пользователь, создаваемый вместе с кластером **{{ mmy-name }}**, автоматически получает роль владельца (`ALL_PRIVILEGES`) первой базы данных в кластере. После этого вы можете [создавать других пользователей](cluster-users.md#adduser) и настраивать их права по своему усмотрению:
- [Изменить список ролей пользователя](#grant-role).
- [Выдать привилегию пользователю](#grant-privilege).
- [Отозвать привилегию у пользователя](#revoke-privilege).

## Изменить список ролей пользователя {#grant-role}

{% list tabs %}

- Консоль управления

  1. Перейдите на страницу каталога и выберите сервис **{{ mmy-name }}**.
  1. Нажмите на имя нужного кластера и выберите вкладку **Пользователи**.
  1. Нажмите значок ![image](../../_assets/horizontal-ellipsis.svg) и выберите пункт **Настроить**.
  1. При необходимости добавьте пользователю нужные базы данных:
     1. Нажмите кнопку **Добавить базу данных**.
     1. Выберите базу данных из выпадающего списка.
     1. Повторите два предыдущих шага, пока не будут выбраны все требуемые базы данных.
     1. Чтобы отозвать доступ к определенной базе, удалите ее из перечня, нажав значок ![image](../../_assets/cross.svg) справа от имени базы данных.
  1. Задайте нужные роли пользователя для каждой из баз данных пользователя:
     1. Нажмите значок ![image](../../_assets/plus-sign.svg) в столбце **Роли**.
     1. Выберите роль, которую вы хотите добавить пользователю из выпадающего списка.
     1. Повторите два предыдущих шага, пока не будут добавлены все требуемые роли.
  1. Чтобы отозвать роль, нажмите значок ![image](../../_assets/cross.svg) справа от ее имени.
  1. Нажмите кнопку **Сохранить**.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  ```bash
  $ {{ yc-mdb-my }} user grant-permission <имя пользователя>
       --cluster-name <имя кластера>
       --database <имя базы данных>
       --permissions <набор ролей через запятую>
  ```

  Имя кластера можно получить при запросе [списка кластеров в каталоге](cluster-list.md), имя базы данных — при запросе [списка баз данных в кластере](databases.md#list-db), имя пользователя — при запросе [списка пользователей в кластере](cluster-users.md#list-users).

  Чтобы выдать пользователю роль `ALL_PRIVILEGES`, передайте в качестве названия роли синоним `ALL`.

- API

  Воспользуйтесь методом API [update](../api-ref/User/update.md) и передайте в запросе:
  - Идентификатор кластера, в котором находится пользователь в параметре `clusterId`. Чтобы узнать идентификатор, [получите список кластеров в каталоге](cluster-list.md#list-clusters).
  - Имя пользователя в параметре `userName`. Чтобы узнать имя, [получите список пользователей в кластере](cluster-users.md#list-users).
  - Имя базы данных, для которой вы хотите изменить список ролей пользователя в параметре `permissions.databaseName`. Чтобы узнать имя, [получите список баз данных в кластере](databases.md#list-db).
  - Массив нового списка ролей пользователя в параметре `permissions.roles`.
  - Список полей конфигурации пользователя подлежащих изменению (в данном случае — `permissions`) в параметре `updateMask`.

  {% note warning %}

  Этот метод API сбросит все настройки пользователя, которые не были явно переданы в запросе, на значения по умолчанию. Чтобы избежать этого, обязательно передайте название поля подлежащего изменению (в данном случае — `permissions`) в параметре `updateMask`.

  {% endnote %}

{% endlist %}

## Выдать привилегию пользователю {#grant-privilege}

1. [Подключитесь](connect.md) к базе данных с помощью учетной записи владельца базы данных.
2. Выполните команду `GRANT`. Подробное описание синтаксиса команды смотрите в [документации {{ MY }}](https://dev.mysql.com/doc/refman/8.0/en/grant.html).

## Отозвать привилегию у пользователя {#revoke-privilege}

1. [Подключитесь](connect.md) к базе данных с помощью учетной записи владельца базы данных.
2. Выполните команду `REVOKE`. Подробное описание синтаксиса команды смотрите в [документации {{ MY }}](https://dev.mysql.com/doc/refman/8.0/en/revoke.html).

{% include [user-ro](../../_includes/mdb/mmy-user-examples.md) %}

## Описание ролей {#db-roles}

  - `ALL_PRIVILEGES` — позволяет совершать любые действия с пользовательскими данными в базе, а также использовать оператор `SHOW SLAVE STATUS`.
  - `ALL` — синоним для роли `ALL_PRIVILEGES`, используемый при управлении ролями через CLI.
  - `ALTER` — позволяет использовать оператор `ALTER TABLE` для изменения структуры любых пользовательских таблиц в базе данных. Требует наличия полномочий `CREATE` и `INSERT`. А для переименования таблиц — `DROP`, `CREATE` и `INSERT`.
  - `ALTER_ROUTINE` — позволяет использовать оператор `ALTER ROUTINE` для изменения или удаления любых пользовательских хранимых процедур и функций в базе данных.
  - `CREATE` — позволяет использовать оператор `CREATE` для создания пользовательских таблиц в базе данных.
  - `CREATE_ROUTINE` — позволяет использовать оператор `CREATE ROUTINE` для создания пользовательских хранимых процедур и функций в базе данных.
  - `CREATE_TEMPORARY_TABLES` — позволяет использовать оператор `CREATE TEMPORARY TABLE` для создания пользовательских временных таблиц в базе данных.
  - `CREATE_VIEW` — позволяет использовать оператор `CREATE VIEW` для создания пользовательских представлений в базе данных.
  - `DELETE` — позволяет удалять записи из любых пользовательских таблиц в базе данных.
  - `DROP` — позволяет удалять таблицы и представления.
  - `EVENT` — позволяет создавать, изменять, удалять или отображать события в [Планировщике Событий (Event Scheduler)](https://dev.mysql.com/doc/refman/8.0/en/events-overview.html).
  - `EXECUTE` — позволяет исполнять любые пользовательские хранимые процедуры и функции.
  - `INDEX` — позволяет создавать и удалять индексы у существующих в базе данных таблиц.
  - `INSERT` — позволяет вставлять записи в пользовательские таблицы в базе данных.
  - `LOCK_TABLES` — позволяет явно использовать оператор `LOCK_TABLES` для создания блокировок на таблицы в базе данных.
  - `PROCESS` — позволяет использовать оператор `SHOW PROCESSLIST` и просматривать статус систем хранения данных (например, `SHOW ENGINE INNODB STATUS`). Кроме того, в {{ mmy-name }} эта роль предоставляет право на чтение таблиц системных баз данных [mysql](https://dev.mysql.com/doc/refman/8.0/en/system-schema.html), [performance_schema](https://dev.mysql.com/doc/refman/8.0/en/performance-schema.html), [sys](https://dev.mysql.com/doc/refman/8.0/en/sys-schema.html).
  - `SELECT` — позволяет читать данные из таблиц в базе данных.
  - `SHOW_VIEW` — позволяет использовать оператор `SHOW CREATE VIEW`.
  - `TRIGGER` — позволяет создавать, удалять, исполнять или отображать триггеры у существующих в базе данных таблиц.
  - `UPDATE` — позволяет обновлять записи в таблицах в базе данных.
