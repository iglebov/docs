---
editable: false
sourcePath: en/_cli-ref/cli-ref/serverless/cli-ref/trigger/index.md
---

# yc serverless trigger

Manage triggers

#### Command Usage

Syntax: 

`yc serverless trigger <group|command>`

#### Command Tree

- [yc serverless trigger add-labels](add-labels.md) — Add labels to specified trigger
- [yc serverless trigger delete](delete.md) — Delete the specified trigger
- [yc serverless trigger get](get.md) — Show information about the specified trigger
- [yc serverless trigger list](list.md) — List triggers
- [yc serverless trigger list-operations](list-operations.md) — Show history of the tag for the specified trigger
- [yc serverless trigger pause](pause.md) — Pause the specified trigger
- [yc serverless trigger remove-labels](remove-labels.md) — Remove labels from specified trigger
- [yc serverless trigger resume](resume.md) — Resume the specified trigger
- [yc serverless trigger create](create/index.md) — Create triggers
	- [yc serverless trigger create billing-budget](create/billing-budget.md) — Create billing budget trigger
	- [yc serverless trigger create container-registry](create/container-registry.md) — Create container registry trigger
	- [yc serverless trigger create internet-of-things](create/internet-of-things.md) — Create internet of things trigger
	- [yc serverless trigger create iot-broker](create/iot-broker.md) — Create IoT broker trigger
	- [yc serverless trigger create logging](create/logging.md) — Create logging trigger
	- [yc serverless trigger create mail](create/mail.md) — Create Mail trigger
	- [yc serverless trigger create message-queue](create/message-queue.md) — Create message queue trigger
	- [yc serverless trigger create object-storage](create/object-storage.md) — Create object storage trigger
	- [yc serverless trigger create timer](create/timer.md) — Create timer trigger
	- [yc serverless trigger create yds](create/yds.md) — Create YDS trigger
- [yc serverless trigger update](update/index.md) — Update the specified trigger
	- [yc serverless trigger update billing-budget](update/billing-budget.md) — Update billing budget trigger
	- [yc serverless trigger update container-registry](update/container-registry.md) — Update container registry trigger
	- [yc serverless trigger update internet-of-things](update/internet-of-things.md) — Update internet of things trigger
	- [yc serverless trigger update iot-broker](update/iot-broker.md) — Update IoT broker trigger
	- [yc serverless trigger update logging](update/logging.md) — Update logging trigger
	- [yc serverless trigger update mail](update/mail.md) — Update Mail trigger
	- [yc serverless trigger update message-queue](update/message-queue.md) — Update message queue trigger
	- [yc serverless trigger update object-storage](update/object-storage.md) — Update object storage trigger
	- [yc serverless trigger update timer](update/timer.md) — Update timer trigger
	- [yc serverless trigger update yds](update/yds.md) — Update YDS trigger

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
