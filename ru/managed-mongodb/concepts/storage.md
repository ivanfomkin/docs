---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Типы хранилища

{{ mmg-name }} позволяет использовать для кластеров баз данных сетевое и локальное хранилища. Сетевое хранилище реализовано на базе сетевых блоков — виртуальных дисков в инфраструктуре {{ yandex-cloud }}. Локальное хранилище организуется на дисках, которые физически размещаются в серверах хостов БД.

{% include [storage-type.md](../../_includes/mdb/storage-type.md) %}

## Особенности локального хранилища {#Local-storage-features}

Локальное хранилище не обеспечивает отказоустойчивости хранения данных, а также влияет на тарификацию кластера в целом:

* Локальное хранилище в кластере из 1 хоста не обеспечивает отказоустойчивости: при отказе локального диска данные теряются безвозвратно. Поэтому при создании нового кластера {{ mmg-name }} с использованием локального хранилища автоматически настраивается отказоустойчивая конфигурация из 3 хостов.
* Кластер с локальным хранилищем тарифицируется, даже если он остановлен. Подробнее — в [правилах тарификации](../pricing.md).
