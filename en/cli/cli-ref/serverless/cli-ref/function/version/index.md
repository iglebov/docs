---
editable: false
sourcePath: en/_cli-ref/cli-ref/serverless/cli-ref/function/version/index.md
---

# yc serverless function version

Manage function versions

#### Command Usage

Syntax: 

`yc serverless function version <command>`

#### Command Tree

- [yc serverless function version create](create.md) — Create new function version
- [yc serverless function version delete](delete.md) — Delete the specified function version
- [yc serverless function version get](get.md) — Show information about the specified function version
- [yc serverless function version get-by-tag](get-by-tag.md) — Get function version by tag
- [yc serverless function version list](list.md) — List function versions
- [yc serverless function version logs](logs.md) — Read function version logs
- [yc serverless function version remove-tag](remove-tag.md) — Remove a tag from the specified function version
- [yc serverless function version set-tag](set-tag.md) — Set a tag on the specified function version

#### Global Flags

| Flag | Description |
|----|----|
|`--profile`|<b>`string`</b><br/>Set the custom configuration file.|
|`--debug`|Debug logging.|
|`--debug-grpc`|Debug gRPC logging. Very verbose, used for debugging connection problems.|
|`--no-user-output`|Disable printing user intended output to stderr.|
|`--retry`|<b>`int`</b><br/>Enable gRPC retries. By default, retries are enabled with maximum 5 attempts.<br/>Pass 0 to disable retries. Pass any negative value for infinite retries.<br/>Even infinite retries are capped with 2 minutes timeout.|
|`--cloud-id`|<b>`string`</b><br/>Set the ID of the cloud to use.|
|`--folder-id`|<b>`string`</b><br/>Set the ID of the folder to use.|
|`--folder-name`|<b>`string`</b><br/>Set the name of the folder to use (will be resolved to id).|
|`--endpoint`|<b>`string`</b><br/>Set the Cloud API endpoint (host:port).|
|`--token`|<b>`string`</b><br/>Set the OAuth token to use.|
|`--impersonate-service-account-id`|<b>`string`</b><br/>Set the ID of the service account to impersonate.|
|`--no-browser`|Disable opening browser for authentication.|
|`--format`|<b>`string`</b><br/>Set the output format: text (default), yaml, json, json-rest.|
|`--jq`|<b>`string`</b><br/>Query to select values from the response using jq syntax|
|`-h`,`--help`|Display help for the command.|
