---
editable: false

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---


# BETWEEN



#### Syntax {#syntax}


```
value [ NOT ] BETWEEN low AND high
```

#### Description {#description}
Returns `TRUE` if `value` is in the range from `low` to `high`.

The option `value NOT BETWEEN low AND high` returns the opposite value.

**Argument types:**
- `value` — `Date | Datetime | Fractional number | Integer | String`
- `low` — `Date | Datetime | Fractional number | Integer | String`
- `high` — `Date | Datetime | Fractional number | Integer | String`


**Return type**: `Boolean`

#### Examples {#examples}

```
3 BETWEEN 1 AND 100 = TRUE
```

```
3 NOT BETWEEN 1 AND 100 = FALSE
```


#### Data source support {#data-source-support}

`Materialized Dataset`, `ClickHouse 1.1`, `Yandex.Metrica`, `Microsoft SQL Server 2017 (14.0)`, `MySQL 5.6`, `Oracle Database 12c (12.1)`, `PostgreSQL 9.3`.
