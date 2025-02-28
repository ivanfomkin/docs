---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Репликация и отказоустойчивость {{ MG }}

{{ mmg-name }} поддерживает репликацию по умолчанию: если в кластере есть больше 1 активного хоста, среди них автоматически выбирается первичная реплика (мастер), обрабатывающая запросы на запись.

При [переключении первичной реплики](../operations/stepdown.md) вручную {{ MG }} автоматически выберет новую из доступных хостов.

{% include [non-replicating-hosts](../../_includes/mdb/non-replicating-hosts.md) %}

Подробнее о том, как организована репликация в {{ MG }}, читайте в [документации СУБД](https://docs.mongodb.com/manual/replication/).

## Отказоустойчивость {#Fault-tolerance}

Чтобы хосты кластера могли при необходимости автоматически выбирать первичную реплику, абсолютное большинство хостов должно быть работоспособно. Поэтому используя {{ mmg-name }}, экономичнее разворачивать кластеры с нечетным количеством хостов. Например, кластер с 3 хостами может потерять 1 хост и продолжить работу, но кластер с 4 хостами также может потерять не более 1 хоста — при потере второго хоста оставшихся не хватит, чтобы выбрать новую первичную реплику.

Кластер из 2 хостов не обеспечивает полной отказоустойчивости по той же причине: единственный оставшийся хост не сможет назначить себя первичной репликой самостоятельно. В этой ситуации кластер может обрабатывать только операции чтения.
