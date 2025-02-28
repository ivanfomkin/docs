---

__system: {"dislikeVariants":["Нет ответа на мой вопрос","Рекомендации не помогли","Содержание не соответствует заголовку","Другое"]}
---
# yc serverless trigger create

Create triggers

#### Command Usage

Syntax: 

`yc serverless trigger create <command>`

#### Command Tree

- [yc serverless trigger create timer](timer.md) — Create timer trigger
- [yc serverless trigger create message-queue](message-queue.md) — Create message queue trigger
- [yc serverless trigger create internet-of-things](internet-of-things.md) — Create internet of things trigger
- [yc serverless trigger create object-storage](object-storage.md) — Create object storage trigger
- [yc serverless trigger create container-registry](container-registry.md) — Create container registry trigger
- [yc serverless trigger create cloud-logs](cloud-logs.md) — Create cloud logs trigger

#### Flags

| Flag | Description |
|----|----|
|`--profile`|<b>`string`</b><br/>Set the custom configuration file.|
|`--debug`|Debug logging.|
|`--debug-grpc`|Debug gRPC logging. Very verbose, used for debugging connection problems.|
|`--no-user-output`|Disable printing user intended output to stderr.|
|`--retry`|<b>`int`</b><br/>Enable gRPC retries. By default, retries are enabled with maximum 5 attempts. Pass 0 to disable retries. Pass any negative value for infinite retries. Even infinite retries are capped with 2 minutes timeout.|
|`--cloud-id`|<b>`string`</b><br/>Set the ID of the cloud to use.|
|`--folder-id`|<b>`string`</b><br/>Set the ID of the folder to use.|
|`--folder-name`|<b>`string`</b><br/>Set the name of the folder to use (will be resolved to id).|
|`--token`|<b>`string`</b><br/>Set the OAuth token to use.|
|`--format`|<b>`string`</b><br/>Set the output format: text (default), yaml, json, json-rest.|
|`-h`,`--help`|Display help for the command.|
