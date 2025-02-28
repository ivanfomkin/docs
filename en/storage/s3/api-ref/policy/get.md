---

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---
# GetBucketPolicy method

Returns the access policy for the specified bucket.

## Request {#request}

```http
GET /{bucket}?policy HTTP/1.1
```

### Path parameters {#path-parameters}

Parameter | Description
--- | ---
`bucket` | Bucket name.

### Query parameters {#request-params}

Parameter | Description
--- | ---
`policy` | Required parameter that indicates the type of operation.

### Headings {#request-headers}

Use the necessary [common request headers](../common-request-headers.md) in requests.

## Response {#response}

### Headings {#response-headers}

Responses can only contain [common response headers](../common-response-headers.md).

### Data schema {#response-scheme}

Data is transmitted in JSON format. For more information, see [{#T}](scheme.md).

### Response codes {#response-codes}

For a list of possible responses, see [{#T}](../response-codes.md).