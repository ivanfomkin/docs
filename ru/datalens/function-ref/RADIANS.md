---
editable: false

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---


# RADIANS



#### Синтаксис {#syntax}


```
RADIANS( degrees )
```

#### Описание {#description}
Преобразует градусы `degrees` в радианы.

**Типы аргументов:**
- `degrees` — `Дробное число | Целое число`


**Возвращаемый тип**: `Дробное число`

#### Примеры {#examples}

```
RADIANS(0) = 0.0
```

```
RADIANS(180) = 3.14159
```


#### Поддержка источников данных {#data-source-support}

`Материализованный датасет`, `ClickHouse 1.1`, `Microsoft SQL Server 2017 (14.0)`, `MySQL 5.6`, `Oracle Database 12c (12.1)`, `PostgreSQL 9.3`.
