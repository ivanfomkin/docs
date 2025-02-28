---
editable: false

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---


# LOG



#### Syntax {#syntax}


```
LOG( value, base )
```

#### Description {#description}
Returns the logarithm of `value` to base `base`. Returns 'NULL' if the number `value` is less than or equal to 0.

**Argument types:**
- `value` — `Fractional number | Integer`
- `base` — `Fractional number | Integer`


**Return type**: `Fractional number`

#### Examples {#examples}

```
LOG(1, 2.6) = 0.0
```

```
LOG(1024, 2) = 10.0
```

```
LOG(100, 10) = 2.0
```


#### Data source support {#data-source-support}

`Materialized Dataset`, `ClickHouse 1.1`, `Microsoft SQL Server 2017 (14.0)`, `MySQL 5.6`, `Oracle Database 12c (12.1)`, `PostgreSQL 9.3`.
