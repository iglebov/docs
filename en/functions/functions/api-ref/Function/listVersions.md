---
editable: false
sourcePath: en/_api-ref/serverless/functions/v1/functions/api-ref/Function/listVersions.md
---

# Cloud Functions Service, REST: Function.ListVersions

Retrieves the list of versions for the specified function, or of all function versions
in the specified folder.

## HTTP request

```
GET https://serverless-functions.{{ api-host }}/functions/v1/versions
```

## Query parameters {#yandex.cloud.serverless.functions.v1.ListFunctionsVersionsRequest}

#|
||Field | Description ||
|| folderId | **string**

ID of the folder to list function versions for.
To get a folder ID make a [yandex.cloud.resourcemanager.v1.FolderService.List](/docs/resource-manager/api-ref/Folder/list#List) request.

Includes only one of the fields `folderId`, `functionId`. ||
|| functionId | **string**

ID of the function to list versions for.
To get a function ID use a [FunctionService.List](/docs/functions/functions/api-ref/Function/list#List) request.

Includes only one of the fields `folderId`, `functionId`. ||
|| pageSize | **string** (int64)

The maximum number of results per page to return. If the number of available results
is larger than `pageSize`, the service returns a [ListFunctionsVersionsResponse.nextPageToken](#yandex.cloud.serverless.functions.v1.ListFunctionsVersionsResponse)
that can be used to get the next page of results in subsequent list requests.

Default value: 100. ||
|| pageToken | **string**

Page token. To get the next page of results, set `pageToken` to the
[ListFunctionsVersionsResponse.nextPageToken](#yandex.cloud.serverless.functions.v1.ListFunctionsVersionsResponse) returned by a previous list request. ||
|| filter | **string**

A filter expression that filters resources listed in the response.

The expression must specify:
1. The field name. Currently filtering can only be applied to the [Version.status](#yandex.cloud.serverless.functions.v1.Version) and [Version.runtime](#yandex.cloud.serverless.functions.v1.Version) fields.
2. An `=` operator.
3. The value in double quotes (`"`). Must be 3-63 characters long and match the regular expression `[a-z][-a-z0-9]{1,61}[a-z0-9]`.
Example of a filter: `status="ACTIVE"`. ||
|#

## Response {#yandex.cloud.serverless.functions.v1.ListFunctionsVersionsResponse}

**HTTP Code: 200 - OK**

```json
{
  "versions": [
    {
      "id": "string",
      "functionId": "string",
      "description": "string",
      "createdAt": "string",
      "runtime": "string",
      "entrypoint": "string",
      "resources": {
        "memory": "string"
      },
      "executionTimeout": "string",
      "serviceAccountId": "string",
      "imageSize": "string",
      "status": "string",
      "tags": [
        "string"
      ],
      "environment": "object",
      "connectivity": {
        "networkId": "string",
        "subnetId": [
          "string"
        ]
      },
      "namedServiceAccounts": "object",
      "secrets": [
        {
          "id": "string",
          "versionId": "string",
          "key": "string",
          // Includes only one of the fields `environmentVariable`
          "environmentVariable": "string"
          // end of the list of possible fields
        }
      ],
      "logOptions": {
        "disabled": "boolean",
        // Includes only one of the fields `logGroupId`, `folderId`
        "logGroupId": "string",
        "folderId": "string",
        // end of the list of possible fields
        "minLevel": "string"
      },
      "storageMounts": [
        {
          "bucketId": "string",
          "prefix": "string",
          "mountPointName": "string",
          "readOnly": "boolean"
        }
      ],
      "asyncInvocationConfig": {
        "retriesCount": "string",
        "successTarget": {
          // Includes only one of the fields `emptyTarget`, `ymqTarget`
          "emptyTarget": "object",
          "ymqTarget": {
            "queueArn": "string",
            "serviceAccountId": "string"
          }
          // end of the list of possible fields
        },
        "failureTarget": {
          // Includes only one of the fields `emptyTarget`, `ymqTarget`
          "emptyTarget": "object",
          "ymqTarget": {
            "queueArn": "string",
            "serviceAccountId": "string"
          }
          // end of the list of possible fields
        },
        "serviceAccountId": "string"
      },
      "tmpfsSize": "string",
      "concurrency": "string",
      "mounts": [
        {
          "name": "string",
          "mode": "string",
          // Includes only one of the fields `objectStorage`, `ephemeralDiskSpec`
          "objectStorage": {
            "bucketId": "string",
            "prefix": "string"
          },
          "ephemeralDiskSpec": {
            "size": "string",
            "blockSize": "string"
          }
          // end of the list of possible fields
        }
      ],
      "metadataOptions": {
        "gceHttpEndpoint": "string",
        "awsV1HttpEndpoint": "string"
      }
    }
  ],
  "nextPageToken": "string"
}
```

#|
||Field | Description ||
|| versions[] | **[Version](#yandex.cloud.serverless.functions.v1.Version)**

List of versions for the specified folder or function. ||
|| nextPageToken | **string**

Token for getting the next page of the list. If the number of results is greater than
the specified [ListFunctionsVersionsRequest.pageSize](#yandex.cloud.serverless.functions.v1.ListFunctionsVersionsRequest), use `nextPageToken` as the value
for the [ListFunctionsVersionsRequest.pageToken](#yandex.cloud.serverless.functions.v1.ListFunctionsVersionsRequest) parameter in the next list request.

Each subsequent page will have its own `nextPageToken` to continue paging through the results. ||
|#

## Version {#yandex.cloud.serverless.functions.v1.Version}

Version of a function. For details about the concept, see [Function versions](/docs/functions/concepts/function#version).

#|
||Field | Description ||
|| id | **string**

ID of the version. ||
|| functionId | **string**

ID of the function that the version belongs to. ||
|| description | **string**

Description of the version. ||
|| createdAt | **string** (date-time)

Creation timestamp for the version.

String in [RFC3339](https://www.ietf.org/rfc/rfc3339.txt) text format. The range of possible values is from
`0001-01-01T00:00:00Z` to `9999-12-31T23:59:59.999999999Z`, i.e. from 0 to 9 digits for fractions of a second.

To work with values in this field, use the APIs described in the
[Protocol Buffers reference](https://developers.google.com/protocol-buffers/docs/reference/overview).
In some languages, built-in datetime utilities do not support nanosecond precision (9 digits). ||
|| runtime | **string**

ID of the runtime environment for the function.

Supported environments and their identifiers are listed in the [Runtime environments](/docs/functions/concepts/runtime). ||
|| entrypoint | **string**

Entrypoint for the function: the name of the function to be called as the handler.

Specified in the format `<function file name>.<handler name>`, for example, `index.myFunction`. ||
|| resources | **[Resources](#yandex.cloud.serverless.functions.v1.Resources)**

Resources allocated to the version. ||
|| executionTimeout | **string** (duration)

Timeout for the execution of the version.

If the timeout is exceeded, Cloud Functions responds with a 504 HTTP code. ||
|| serviceAccountId | **string**

ID of the service account associated with the version. ||
|| imageSize | **string** (int64)

Final size of the deployment package after unpacking. ||
|| status | **enum** (Status)

Status of the version.

- `STATUS_UNSPECIFIED`
- `CREATING`: Version is being created.
- `ACTIVE`: Version is ready to use.
- `OBSOLETE`: Version will be deleted soon.
- `DELETING`: Version is being deleted. ||
|| tags[] | **string**

Version tags. For details, see [Version tag](/docs/functions/concepts/function#tag). ||
|| environment | **object** (map<**string**, **string**>)

Environment settings for the version. ||
|| connectivity | **[Connectivity](#yandex.cloud.serverless.functions.v1.Connectivity)**

Network access. If specified the version will be attached to specified network/subnet(s). ||
|| namedServiceAccounts | **object** (map<**string**, **string**>)

Additional service accounts to be used by the version. ||
|| secrets[] | **[Secret](#yandex.cloud.serverless.functions.v1.Secret)**

Yandex Lockbox secrets to be used by the version. ||
|| logOptions | **[LogOptions](#yandex.cloud.serverless.functions.v1.LogOptions)**

Options for logging from the function ||
|| storageMounts[] | **[StorageMount](#yandex.cloud.serverless.functions.v1.StorageMount)**

S3 mounts to be used by the version. ||
|| asyncInvocationConfig | **[AsyncInvocationConfig](#yandex.cloud.serverless.functions.v1.AsyncInvocationConfig)**

Config for asynchronous invocations of the version ||
|| tmpfsSize | **string** (int64)

Optional size of in-memory mounted /tmp directory in bytes. ||
|| concurrency | **string** (int64)

The maximum number of requests processed by a function instance at the same time ||
|| mounts[] | **[Mount](#yandex.cloud.serverless.functions.v1.Mount)**

Mounts to be used by the version. ||
|| metadataOptions | **[MetadataOptions](#yandex.cloud.serverless.functions.v1.MetadataOptions)**

Metadata options for the version. ||
|#

## Resources {#yandex.cloud.serverless.functions.v1.Resources}

Resources allocated to a version.

#|
||Field | Description ||
|| memory | **string** (int64)

Amount of memory available to the version, specified in bytes, multiple of 128MB. ||
|#

## Connectivity {#yandex.cloud.serverless.functions.v1.Connectivity}

Version connectivity specification.

#|
||Field | Description ||
|| networkId | **string**

Network the version will have access to.
It's essential to specify network with subnets in all availability zones. ||
|| subnetId[] | **string**

Complete list of subnets (from the same network) the version can be attached to.
It's essential to specify at least one subnet for each availability zones. ||
|#

## Secret {#yandex.cloud.serverless.functions.v1.Secret}

Secret for serverless function.

#|
||Field | Description ||
|| id | **string**

ID of Yandex Lockbox secret. ||
|| versionId | **string**

ID of Yandex Lockbox version. ||
|| key | **string**

Key in secret's payload, which value to be delivered into function environment. ||
|| environmentVariable | **string**

environment variable in which secret's value to be delivered.

Includes only one of the fields `environmentVariable`. ||
|#

## LogOptions {#yandex.cloud.serverless.functions.v1.LogOptions}

#|
||Field | Description ||
|| disabled | **boolean**

Is logging from function disabled. ||
|| logGroupId | **string**

Entry should be written to log group resolved by ID.

Includes only one of the fields `logGroupId`, `folderId`.

Log entries destination. ||
|| folderId | **string**

Entry should be written to default log group for specified folder.

Includes only one of the fields `logGroupId`, `folderId`.

Log entries destination. ||
|| minLevel | **enum** (Level)

Minimum log entry level.

See [LogLevel.Level](/docs/logging/api-ref/Export/run#yandex.cloud.logging.v1.LogLevel.Level) for details.

- `LEVEL_UNSPECIFIED`: Default log level.

  Equivalent to not specifying log level at all.
- `TRACE`: Trace log level.

  Possible use case: verbose logging of some business logic.
- `DEBUG`: Debug log level.

  Possible use case: debugging special cases in application logic.
- `INFO`: Info log level.

  Mostly used for information messages.
- `WARN`: Warn log level.

  May be used to alert about significant events.
- `ERROR`: Error log level.

  May be used to alert about errors in infrastructure, logic, etc.
- `FATAL`: Fatal log level.

  May be used to alert about unrecoverable failures and events. ||
|#

## StorageMount {#yandex.cloud.serverless.functions.v1.StorageMount}

#|
||Field | Description ||
|| bucketId | **string**

Required field. S3 bucket name for mounting. ||
|| prefix | **string**

S3 bucket prefix for mounting. ||
|| mountPointName | **string**

Required field. Mount point directory name (not path) for mounting. ||
|| readOnly | **boolean**

Is mount read only. ||
|#

## AsyncInvocationConfig {#yandex.cloud.serverless.functions.v1.AsyncInvocationConfig}

#|
||Field | Description ||
|| retriesCount | **string** (int64)

Number of retries of version invocation ||
|| successTarget | **[ResponseTarget](#yandex.cloud.serverless.functions.v1.AsyncInvocationConfig.ResponseTarget)**

Required field. Target for successful result of the version's invocation ||
|| failureTarget | **[ResponseTarget](#yandex.cloud.serverless.functions.v1.AsyncInvocationConfig.ResponseTarget)**

Required field. Target for unsuccessful result, if all retries failed ||
|| serviceAccountId | **string**

Service account which can invoke version ||
|#

## ResponseTarget {#yandex.cloud.serverless.functions.v1.AsyncInvocationConfig.ResponseTarget}

Target to which a result of an invocation will be sent

#|
||Field | Description ||
|| emptyTarget | **object**

Target to ignore a result

Includes only one of the fields `emptyTarget`, `ymqTarget`. ||
|| ymqTarget | **[YMQTarget](#yandex.cloud.serverless.functions.v1.YMQTarget)**

Target to send a result to ymq

Includes only one of the fields `emptyTarget`, `ymqTarget`. ||
|#

## YMQTarget {#yandex.cloud.serverless.functions.v1.YMQTarget}

#|
||Field | Description ||
|| queueArn | **string**

Required field. Queue ARN ||
|| serviceAccountId | **string**

Required field. Service account which has write permission on the queue. ||
|#

## Mount {#yandex.cloud.serverless.functions.v1.Mount}

Mount contains an information about version's external storage mount

#|
||Field | Description ||
|| name | **string**

Required field. Unique mount point name. Device will be mounted into /function/storage/<name> ||
|| mode | **enum** (Mode)

Mount's mode

- `MODE_UNSPECIFIED`
- `READ_ONLY`
- `READ_WRITE` ||
|| objectStorage | **[ObjectStorage](#yandex.cloud.serverless.functions.v1.Mount.ObjectStorage)**

Object storage mounts

Includes only one of the fields `objectStorage`, `ephemeralDiskSpec`.

Target mount option ||
|| ephemeralDiskSpec | **[DiskSpec](#yandex.cloud.serverless.functions.v1.Mount.DiskSpec)**

Working disk (worker-local non-shared read-write NBS disk templates)

Includes only one of the fields `objectStorage`, `ephemeralDiskSpec`.

Target mount option ||
|#

## ObjectStorage {#yandex.cloud.serverless.functions.v1.Mount.ObjectStorage}

ObjectStorage as a mount

#|
||Field | Description ||
|| bucketId | **string**

Required field. ObjectStorage bucket name for mounting. ||
|| prefix | **string**

ObjectStorage bucket prefix for mounting. ||
|#

## DiskSpec {#yandex.cloud.serverless.functions.v1.Mount.DiskSpec}

Disk as a mount

#|
||Field | Description ||
|| size | **string** (int64)

The size of disk for mount in bytes ||
|| blockSize | **string** (int64)

Optional block size of disk for mount in bytes ||
|#

## MetadataOptions {#yandex.cloud.serverless.functions.v1.MetadataOptions}

#|
||Field | Description ||
|| gceHttpEndpoint | **enum** (MetadataOption)

Enabled access to GCE flavored metadata

- `METADATA_OPTION_UNSPECIFIED`: Option is default
- `ENABLED`: Option is enabled
- `DISABLED`: Option is disabled ||
|| awsV1HttpEndpoint | **enum** (MetadataOption)

Enabled access to AWS flavored metadata (IMDSv1)

- `METADATA_OPTION_UNSPECIFIED`: Option is default
- `ENABLED`: Option is enabled
- `DISABLED`: Option is disabled ||
|#