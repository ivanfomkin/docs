---

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---
# Log group

_A log group_ is a way of grouping messages from the same source. This source can be, for example, a [function](function.md) or [registry](../../iot-core/concepts/index.md#registry) named IoT-core.

You can use the CLI to find out the ID of a log group by its source. To find out a function's log group, run the command:

```
$ yc serverless function get <function_id> | grep log_group_id
```

Result:

```
log_group_id: eol6cgr0************
```

