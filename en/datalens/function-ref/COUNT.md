---
editable: false

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---


# COUNT

_Function `COUNT` is also available as a [window function](COUNT_WINDOW.md)._

#### Syntax {#syntax}


```
COUNT(  [ value ] )
```

#### Description {#description}
Returns the number of items in the group.

**Argument types:**
- `value` — `Any`


**Return type**: `Integer`

#### Examples {#examples}

```
COUNT()
```

```
COUNT([OrderID])
```


#### Data source support {#data-source-support}

`Materialized Dataset`, `ClickHouse 1.1`, `Microsoft SQL Server 2017 (14.0)`, `MySQL 5.6`, `Oracle Database 12c (12.1)`, `PostgreSQL 9.3`.
