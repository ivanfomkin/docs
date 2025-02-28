---
editable: false

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---


# IENDSWITH



#### Syntax {#syntax}


```
IENDSWITH( string, substring )
```

#### Description {#description}
Case-insensitive version of [ENDSWITH](ENDSWITH.md). Returns `TRUE` if `string` ends in `substring`.

**Argument types:**
- `string` — `Boolean | Date | Datetime | Fractional number | Geopoint | Geopolygon | Integer | String | UUID`
- `substring` — `String`


**Return type**: `Boolean`

#### Examples {#examples}

```
IENDSWITH("PETROV IVAN", "Ivan") = TRUE
```

```
IENDSWITH("Lorem ipsum", "SUM") = TRUE
```

```
IENDSWITH("Lorem ipsum", "abc") = FALSE
```


#### Data source support {#data-source-support}

`Materialized Dataset`, `ClickHouse 1.1`, `Microsoft SQL Server 2017 (14.0)`, `MySQL 5.6`, `Oracle Database 12c (12.1)`, `PostgreSQL 9.3`.
