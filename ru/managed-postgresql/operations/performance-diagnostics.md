# Диагностика производительности

{{ mpg-name }} предоставляет встроенный инструмент для диагностики производительности кластера СУБД. Этот инструмент помогает анализировать метрики производительности {{ PG }} для [сессий](#get-sessions) и [запросов](#get-queries).

{% note info %}

Эта функциональность находится в режиме [Preview](../../overview/concepts/launch-stages.md).

{% endnote %}

## Активировать сбор статистики {#activate-stats-collector}

Чтобы воспользоваться инструментом диагностики, включите опцию **Сбор статистики** при [создании кластера](cluster-create.md) или [изменении его настроек](update.md#change-additional-settings) (по умолчанию опция отключена). 

При необходимости задайте интервалы сбора статистики для сессий и запросов.

## Получить информацию о сессиях {#get-sessions}

Для сессий доступна история запросов, выполненных в рамках сессии, а также статистика по сессиям:
- График количества сессий для выбранного среза данных. Можно скрыть или показать отдельные категории на графике, нажав на имя категории в легенде графика.
- Таблица со статистикой по сессиям и запросам.

Подробнее про отображаемые сведения см. [в документации {{ PG }}](https://www.postgresql.org/docs/current/monitoring-stats.html#MONITORING-PG-STAT-ACTIVITY-VIEW).

{% list tabs %}

- Статистика по сессиям

  1. В консоли управления перейдите на страницу каталога и выберите сервис **{{ mpg-name }}**.
  1. Нажмите на имя нужного кластера, затем выберите вкладку **Диагностика производительности**.
  1. Выберите вкладку **Сессии → Статистика**.
  1. Задайте интересующий интервал времени, при необходимости настройте фильтры.
  1. Выберите нужный [срез данных](https://www.postgresql.org/docs/current/monitoring-stats.html#MONITORING-PG-STAT-ACTIVITY-VIEW) из списка.

- История запросов

  1. В консоли управления перейдите на страницу каталога и выберите сервис **{{ mpg-name }}**.
  1. Нажмите на имя нужного кластера, затем выберите вкладку **Диагностика производительности**.
  1. Выберите вкладку **Сессии → История**.
  1. Задайте интересующий интервал времени, при необходимости настройте фильтры.
  
{% endlist %}

## Получить информацию о запросах {#get-queries}

Для запросов доступна статистика, а также сравнение статистических данных за два временных интервала.

Например, пусть в первом интервале было выполнено 10 запросов `SELECT * FROM cities`, а во втором — 20. Тогда при сравнении статистических данных разница по метрике «количество запросов» (столбец `Calls` в таблице) будет равняться `+100%`.

Подробнее про отображаемые сведения см. [в документации {{ PG }}](https://www.postgresql.org/docs/current/pgstatstatements.html#id-1.11.7.38.6).

{% list tabs %}

- Статистика запросов

  1. В консоли управления перейдите на страницу каталога и выберите сервис **{{ mpg-name }}**.
  1. Нажмите на имя нужного кластера, затем выберите вкладку **Диагностика производительности**.
  1. Выберите вкладку **Запросы → Интервал**.
  1. Задайте интересующий интервал времени, при необходимости настройте фильтры.

- Сравнение запросов

  1. В консоли управления перейдите на страницу каталога и выберите сервис **{{ mpg-name }}**.
  1. Нажмите на имя нужного кластера, затем выберите вкладку **Диагностика производительности**.
  1. Выберите вкладку **Запросы → 2 Интервала**.
  1. Задайте интересующие интервалы времени, при необходимости настройте фильтры.

{% endlist %}