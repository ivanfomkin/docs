---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# HTTP-роутер

HTTP-роутер определяет правила маршрутизации HTTP-запросов в [группы бэкендов](backend-group.md), позволяет модифицировать заголовки запросов и ответов, а также формировать небольшие статические ответы прямо на балансировщике нагрузки. Можно создать пустой HTTP-роутер, а потом добавить в него маршруты.

Маршруты внутри HTTP-роутера объединены в [виртуальные хосты](#virtual-host). Маршрутизация происходит в два этапа. 

1. На основе заголовка `Host` (`:authority` в случае HTTP/2) выбирается наиболее подходящий виртуальный хост. 
1. Выбирается первый маршрут, предикату которого удовлетворяет запрос. Порядок виртуальных хостов внутри роутера не важен, а порядок маршрутов внутри виртуального хоста важен — наиболее специфичные маршруты должны быть первыми в списке.

## Виртуальные хосты {#virtual-host}

Виртуальные хосты объединяют [маршруты](#routes), относящиеся к одному набору доменов — значений заголовков `Host` HTTP-запроса. Поддерживаются как точные совпадения, так и символы подстановки. При получении входящего запроса балансировщик по очереди проверяет предикаты маршрутов и выбирает первый, удовлетворяющий запросу. 

Также на уровне виртуального хоста настраиваются модификации HTTP-заголовков запросов и ответов.

## Маршруты {#routes}

Маршруты состоят из набора условий (предиката), на основании которых балансировщик выбирает маршрут для запроса, и действия над запросом. Условия могут требовать точного или частичного совпадения URI запроса или определенных HTTP-методов. В качестве действия можно выбрать: 

* генерируемый балансировщиком прямой ответ;
* HTTP-перенаправление с выбранным кодом и модификациями URL запроса;
* передачу запроса в [группу бэкендов](backend-group.md) для обработки. В этом случае есть возможность настроить таймауты на обработку запроса, поддержку WebSocket или изменение URI перед передачей запроса в бэкенды.