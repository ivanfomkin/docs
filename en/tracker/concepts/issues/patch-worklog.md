---

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---
# Edit a record of time spent

Use this request to edit a record of the time spent on an issue.

## Request format {#section_q5n_mtk_gfb}

To edit records of time spent on issues, use an HTTP `PATCH` request: Request parameters are passed in the request body in JSON format:

```json
PATCH /{{ ver }}/issues/<issue-id>/worklog/<worklog-id>
Host: {{ host }}
Authorization: OAuth <token>
X-Org-ID: <organization ID>

{
    "duration": "P3W",
    "comment": "time changed!"
}
```

#### Resource {#req-resource}

- **\<issue-id\>**

    Issue ID or key.

- **\<worklog-id\>**

    ID of the record of time spent.

#### Headers {#req-headers}

- **Host**

    Address of the node that provides the API:

    ```
    {{ host }}
    ```

- **Authorization**

    OAuth token in `OAuth <token value>` format. For example:

    ```
    OAuth 0c4181a7c2cf4521964a72ff57a34a07
    ```

- **X-Org-ID**

    Organization ID.

#### Request body {#req-body-params}

The request body contains the issue parameters:

| Parameter | Description | Data type |
| -------- | -------- | ---------- |
| duration | Time spent, in ```PnYnMnDTnHnMnS, PnW``` format, according to the [ISO 8601]({{ link-iso-8601 }}). | String |
| comment | Text of the comment to the record. The comment is saved to the Time Spent report. | String |

## Response format {#section_gvv_tdl_gfb}

{% list tabs %}

- Request executed successfully

    If the request is successful, the API returns a response with code 200. The response body contains a JSON object with an updated record of the time spent on the issue.

    #### Response body {#answer-body}

    ```json
    {
      "self": "https://api.tracker.yandex.net/v2/issues/TEST-324/worklog/1",
      "id": 1,
      "version": 1402121720882,
      "issue": {
        "self": "https://api.tracker.yandex.net/v2/issues/TEST-324",
        "id": "515ec9eae4b09cfa984e2047",
        "key": "TEST-324",
        "display": "important issue"
      },
      "comment": "important comment",
      "createdBy": {
        "self": "https://api.tracker.yandex.net/v2/users/1120000000014909",
        "id": "veikus",
        "display": "Artem Veikus"
      },
      "updatedBy": {
        "self": "https://api.tracker.yandex.net/v2/users/1120000000014909",
        "id": "veikus",
        "display": "Artem Veikus"
      },
      "createdAt": "2014-06-06T08:42:06.258+0000",
      "updatedAt": "2014-06-06T08:42:06.258+0000",
      "start": "2014-06-06T08:41:58.000+0000",
      "duration": "P3W"
    }
    ```

    #### Response parameters {#answer-params}

    | Parameter | Description | Data type |
    | -------- | -------- | ---------- |
    | self | Address of the API resource with a record of the time spent on the issue. | String |
    | id | ID of the record of time spent. | String |
    | version | Record version. Each change to the record increases its version number. | String |
    | [issue](#issue) | Block with information about the issue. | Object |
    | comment | Text of the comment to the record. The comment is saved to the Time Spent report. | String |
    | [createdBy](#createdBy) | Object with information about the user who added the record. | Object |
    | [updatedBy](#updatedBy) | Object with information about the user who edited the record. | Object |
    | createdAt | Record creation date and time in ```YYYY-MM-DDThh:mm:ss.sss±hhmm``` format | String |
    | updatedAt | Record update date and time in ```YYYY-MM-DDThh:mm:ss.sss±hhmm``` format | String |
    | start | Date and time when work on the issue started, in ```YYYY-MM-DDThh:mm:ss.sss±hhmm``` format | String |
    | duration | Time spent, in ```PnYnMnDTnHnMnS, PnW``` format, according to the [ISO 8601]({{ link-iso-8601 }}). | String |

    **Object fields** `issue` {#issue}

    | Parameter | Description | Data type |
    | -------- | -------- | ---------- |
    | self | Address of the API resource with information about the issue. | String |
    | id | Issue ID. | String |
    | key | Issue key. | String |
    | display | Issue name displayed. | String |

    **Object fields** `createdBy` {#createdBy}

    | Parameter | Description | Data type |
    | -------- | -------- | ---------- |
    | self | Address of the API resource with information about the user. | String |
    | id | User ID. | String |
    | display | User's name displayed. | String |

    **Object fields** `updatedBy` {#updatedBy}

    | Parameter | Description | Data type |
    | -------- | -------- | ---------- |
    | self | Address of the API resource with information about the user. | String |
    | id | User ID. | String |
    | display | User's name displayed. | String |

- Request failed

    If the request is processed incorrectly, the API returns a message with error details:

    | HTTP error code | Error description |
    | --------------- | --------------- |
    | 400 Bad Request | One of the request parameters has an invalid value or data format. |
    | 403 Forbidden | The user or application has no access rights to the resource, the request is rejected. |
    | 404 Not Found | The requested resource not found. |
    | 422 Unprocessable Entity | JSON validation error, the request is rejected. |
    | 500 Internal Server Error | Internal service error. Try again later. |
    | 503 Service Unavailable | The API service is temporarily unavailable. |

{% endlist %}

