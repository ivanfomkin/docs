---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# Политика развертывания

При создании группы виртуальных машин можно выбрать, каким образом будут развертываться ВМ в группе.

Политика развертывания представляет собой набор ограничений и определяется в YAML-файле, в ключе `deploy_policy`. Каждое ограничение задается в собственном ключе, в виде пары `ключ:значение`.

Пример записи в YAML-файле:

```
...
deploy_policy:
    max_creating: 10
    max_deleting: 10
    max_unavailable: 10
    max_expansion: 0
    startup_duration: 30s
...
```

Ключи:

Ключ | Значение
----- | -----
`max_creating` | Максимальное количество одновременно создаваемых ВМ.<br>Допустимые значения — от 0 до 100. Значение 0 — любое количество ВМ в рамках допустимых значений.
`max_deleting` | Максимальное количество одновременно удаляемых ВМ.<br>Допустимые значения — от 0 до 100. Значение 0 — любое количество ВМ в рамках допустимых значений.
`max_unavailable` | Максимальное количество ВМ в статусе `RUNNING`, на которое можно уменьшить целевой размер группы.<br>Допустимые значения — от 0 до 100.
`max_expansion` | Максимальное количество ВМ, на которое можно превысить целевой размер группы. Если ключ `max_unavailable` не указан или равен нулю, ключу `max_expansion` должно быть установлено ненулевое значение.<br>Допустимые значения — от 0 до 100.
`startup_duration` | Время запуска ВМ в группе. ВМ начнет получать нагрузку только после того, как истечет время запуска, и будут пройдены все проверки состояния.<br>Допустимые значения — от 0 до 3600 секунд.

## Стратегии остановки виртуальных машин {#strategy}

В {{ ig-name }} есть две стратегии остановки ВМ при обновлении или [автоматическом масштабировании](../scale.md#auto-scale) группы: принудительная (`PROACTIVE`) и деликатная (`OPPORTUNISTIC`).

Если выбрана принудительная стратегия, {{ ig-name }} самостоятельно выбирает, какие ВМ остановить. 

При деликатной стратегии {{ ig-name }} не останавливает ВМ, а ожидает выполнения хотя бы одного из условий:
* Пользователь [остановил](../../../operations/vm-control/vm-stop-and-start.md#stop) ВМ в сервисе {{ compute-name }}.
* Приложение или пользователь остановили ВМ изнутри.
* ВМ не прошла [проверку](../autohealing.md#functional-healthcheck) состояния приложения.

Например, вы создали группу ВМ с автоматическим масштабированием по [пользовательской метрике](../scale.md#custom-metrics), где метрикой является количество задач в очереди. {{ ig-name }} создает группу ВМ, которая выполняет задачи из очереди. Как только в очереди закончились задачи, {{ ig-name }} должен уменьшить размер группы с фактического до целевого согласно [политике масштабирования](scale-policy.md).
  * При этом, если выбрана принудительная остановка, {{ ig-name }} изменит целевой размер группы и уменьшит фактическое количество ВМ в группе до целевого.
  * При деликатной стратегии {{ ig-name }} изменит целевой размер группы, но не остановит ВМ до момента самостоятельной остановки или остановки пользователем.

Пример записи в YAML-файле:

```
...
deploy_policy:
    strategy: OPPORTUNISTIC
...
```

Ключи:

Ключ | Значение
----- | -----
`strategy` | Стратегия остановки ВМ в группе.<br>Возможные значения:<br>- `PROACTIVE` — {{ ig-name }} самостоятельно выбирает, какие ВМ остановить.<br>- `OPPORTUNISTIC` — {{ ig-name }} ожидает, когда ВМ остановятся самостоятельно или будут остановлены пользователем.<br>Значение по умолчанию: `PROACTIVE`.