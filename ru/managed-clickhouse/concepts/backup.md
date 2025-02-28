---
title: Резервные копии ClickHouse
description: {{ mch-short-name }} обеспечивает автоматическое и ручное резервное копирование баз данных. Резервные копии занимают место в объеме хранилища, выделенном для кластера. Резервные копии автоматически создаются раз в день.
keywords:
  - бекап
  - backup
  - резервное копирование
  - резервное копирование ClickHouse
  - backup ClickHouse
  - ClickHouse

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---


# Резервные копии

{{ mch-short-name }} обеспечивает автоматическое и ручное резервное копирование баз данных.

Резервная копия автоматически создается раз в день и хранится 7 дней. Отключить автоматическое создание резервных копий и изменить их срок хранения нельзя.

Чтобы восстановить кластер из резервной копии, [следуйте инструкциям](../operations/cluster-backups.md#restore).

## Создание резервной копии {#size}

Резервные копии могут быть созданы автоматически и вручную, в обоих случаях используется инкрементальная схема:

* При создании очередной резервной копии [куски данных](https://clickhouse.tech/docs/ru/engines/table-engines/mergetree-family/mergetree/#mergetree-data-storage) проверяются на уникальность.
* Если идентичные [куски данных](https://clickhouse.tech/docs/ru/engines/table-engines/mergetree-family/mergetree/#mergetree-data-storage) уже есть в одной из существующих резервных копий и они не старше {{ mch-dedup-retention }} дней, то они не дублируются.

В резервной копии хранятся данные только для движков семейства `MergeTree`. Для остальных движков хранятся только схемы таблиц. Подробнее про движки см. в [документации {{ CH }}](https://clickhouse.tech/docs/ru/engines/table-engines/).

Время начала резервного копирования задается при [создании](../operations/cluster-create.md) или [изменении](../operations/update.md#change-additional-settings) кластера. По умолчанию время начала — 22:00 UTC (Coordinated Universal Time). Резервное копирование начнется в течение получаса от указанного времени.

Резервные копии создаются только на работающих кластерах. Если вы используете кластер {{ mch-short-name }} не круглосуточно, проверьте [настройки времени начала резервного копирования](../operations/update.md#change-additional-settings).

О том, как вручную создать резервную копию, читайте в разделе [{#T}](../operations/cluster-backups.md).

## Хранение резервной копии {#storage}

Особенности хранения резервных копий в {{ mch-name }}:

* Резервные копии хранятся в объектном хранилище в виде бинарных файлов и шифруются с помощью [GPG](https://ru.wikipedia.org/wiki/GnuPG). У каждого кластера свои ключи шифрования.

* Все резервные копии (автоматические и созданные вручную) хранятся {{ mch-backup-retention }} дней.

* {% include [no-quotes-no-limits](../../_includes/mdb/backups/no-quotes-no-limits.md) %}

* {% include [using-storage](../../_includes/mdb/backups/storage.md) %}

    Подробнее см. в разделе [Правила тарификации для {{ mch-short-name }}](../pricing.md#rules-storage).

## Проверка резервной копии {#verify}

### Проверка целостности резервной копии {#integrity}

Целостность резервных копий проверяется на синтетических данных интеграционными тестами сервиса.

### Проверка восстановления из резервной копии {#capabilities}

Для проверки возможностей резервного копирования [восстановите кластер из резервной копии](../operations/cluster-backups.md) и проверьте целостность ваших данных.