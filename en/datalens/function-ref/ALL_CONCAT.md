---
editable: false

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---


# ALL_CONCAT



#### Syntax {#syntax}


```
ALL_CONCAT( expression [ , separator ] )
```

#### Description {#description}
Returns a string that contains all grouped values of `expression` delimited by `separator` (if `separator` is not specified, a comma is used).

**Argument types:**
- `expression` — `Boolean | Date | Datetime | Fractional number | Geopoint | Geopolygon | Integer | String | UUID`
- `separator` — `String`


**Return type**: `String`

{% note info %}

Only constant values are accepted for arguments (`separator`).

{% endnote %}


#### Examples {#examples}

```
ALL_CONCAT([Profit])
```

```
ALL_CONCAT([Profit], '; ')
```


#### Data source support {#data-source-support}

`Materialized Dataset`, `ClickHouse 1.1`, `PostgreSQL 9.3`.
