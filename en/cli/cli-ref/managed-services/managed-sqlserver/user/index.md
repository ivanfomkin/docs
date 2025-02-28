---

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---
# yc managed-sqlserver user

Manage SQLServer users

#### Command Usage

Syntax: 

`yc managed-sqlserver user <command>`

Aliases: 

- `users`

#### Command Tree

- [yc managed-sqlserver user get](get.md) — Show information about the specified SQLServer user
- [yc managed-sqlserver user list](list.md) — List users for the specified SQLServer cluster
- [yc managed-sqlserver user create](create.md) — Create a SQLServer user
- [yc managed-sqlserver user update](update.md) — Update the specified SQLServer user
- [yc managed-sqlserver user delete](delete.md) — Delete the specified SQLServer user
- [yc managed-sqlserver user grant-permission](grant-permission.md) — Grant database access to the specified SQLServer user
- [yc managed-sqlserver user revoke-permission](revoke-permission.md) — Revoke database access from the specified SQLServer user

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
