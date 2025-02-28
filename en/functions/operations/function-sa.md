---

__system: {"dislikeVariants":["No answer to my question","Recomendations didn't help","The content doesn't match title","Other"]}
---
# Using functions to get an IAM token for a service account

If the function version was created with a service account, you can get an IAM token for it from:

* The handler [context](../concepts/function.md#model-desc). The IAM token is in the `access_token` field of the `context` parameter.
* The metadata service in [Google Compute Engine](../../compute/operations/vm-info/get-info.md#gce-metadata) format using the API.

To get an IAM token:

1. [Create](../operations/function/function-create.md) a function.

1. Select the programming language and create a function version:

     {% list tabs %}

     - Node.js
        1. Save the following code to a file named `index.js` to get the IAM token:
            * From the handler context.

                ```js
                exports.main = async function (event, context) {
                    return {
                        'statusCode': 200,
                        'headers': {
                            'Content-Type': 'text/plain'
                        },
                        'isBase64Encoded': false,
                        'body': context.token
                    }
                };
                ```
            * Using the API.

                ```js
                const fetch = require("node-fetch");
                let url = 'http://169.254.169.254/computeMetadata/v1/instance/service-accounts/default/token';
                let headers = {'Metadata-Flavor': 'Google'};
                
                exports.main = async function (event) {
                    const resp = await fetch(url, {
                        headers: headers,
                    });
                    return {
                        code: resp.status,
                        body: await resp.text()
                    };
                };
                ```
        1. Add `index.js` to the `index-js.zip` archive.
        1. [Create](../operations/function/version-manage.md#version-create) a function version. Indicate the following:
            * Runtime environment: `nodejs12`.
            * The service account to get the IAM token for.
            * Entry point: `index.main`.

    - Python
        1. Save the following code to a file named `index.py` to get the IAM token:
            * From the handler context.

                ```py
                def main(event, context):
                
                    return {
                        'statusCode': 200,
                        'headers': {
                            'Content-Type': 'text/plain'
                        },
                        'isBase64Encoded': False,
                        'body': context.token
                    }
                ```
            * Using the API.

                ```py
                import requests
                
                url = 'http://169.254.169.254/computeMetadata/v1/instance/service-accounts/default/token'
                headers = {'Metadata-Flavor': 'Google'}
                
                
                def main(event, context):
                
                    resp = requests.get(url, headers=headers)
                
                    return {
                        'statusCode': 200,
                        'headers': {
                            'Content-Type': 'text/plain'
                        },
                        'isBase64Encoded': False,
                        'body': resp.content.decode('UTF-8')
                    }
                ```
        1. Add `index.py` to the `index-py.zip` archive.
        1. [Create](../operations/function/version-manage.md#version-create) a function version. Indicate the following:
            * Runtime environment: `python37`.
            * The service account to get the IAM token for.
            * Entry point: `index.main`.

    {% endlist %}

1. [Run](../operations/function/function-invoke.md) the function.

    The function response looks like this:

    ```json
    {
        "access_token": "CggVAgAAABoBMRKABHGgpZ......",
        "expires_in": 42299,
        "token_type": "Bearer"
    }
    ```

