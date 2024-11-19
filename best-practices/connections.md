# Connections

Every connection should have a way how to check if the used API Key/Token is valid (Validation Endpoint). That means each connection should have a part that uses the used API Key/Token against some endpoint that requires only the API Key/Token to run. For example, User Info endpoint or any endpoint which is used to List data.

The validation endpoint is located:

* OAuth1 and OAuth2 - the `info` directive
* API Key, Basic Auth, Digest Auth, Other - the `url` which is in the Communication tab

{% hint style="info" %}
There are APIs, which don't have a validation endpoint. In this case, it is recommended to call an endpoint, which will work in every case, and if possible will return the account's data, e. g. an endpoint `/about` or `/me`, etc.
{% endhint %}

{% tabs %}
{% tab title="Right API Key" %}
![Coda (beta) connection example](../.gitbook/assets/connectionsUrlExampleOtherRight.png)

The API Key is checked against `/whoami` endpoint which in case of wrong API Key returns an error and the connection won't be created.
{% endtab %}

{% tab title="Right OAuth" %}
```
{
    "authorize": {
        ...
    },
    "token": {
        ...
    },
    "info": {
        "url": "https://api.dropboxapi.com/2/users/get_current_account",
        "method": "POST",
        "headers": {
            "authorization": "Bearer {{connection.accessToken}}"
        },
        "body": "{{null}}",
        "response": {
            "uid": "{{body.account_id}}",
            "metadata": {
                "type": "email",
                "value": "{{body.email}}"
            },
            "error": {
                "message": "[{{statusCode}}] {{if(body.error_summary, body.error_summary, body)}}"
            },
            "data": {
                "root_namespace_id": "{{body.root_info.root_namespace_id}}"
            }
        },
        "log": {
            "sanitize": [
                "request.headers.authorization"
            ]
        }
    },
    "invalidate": {
        ...
    }
}
```



An example of the "info" part of the Dropbox Oauth2 connection.
{% endtab %}

{% tab title="Wrong" %}
![](../.gitbook/assets/connectionsUrlExampleWrong.png)

There is no endpoint to check whether entered credentials like API Key, Username & Password, etc. were correct and will allow the connection to be created with anything, including wrong credentials.
{% endtab %}
{% endtabs %}

### Connection metadata

It is recommended to use the `metadata` parameter to store the account's name or email. This allows users to easily distinguish their stored connections, especially if they don't name their connections in a good manner.

{% tabs %}
{% tab title="Occurence in a module" %}
<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption><p>Example of Connection's Name</p></figcaption></figure>

Notice the value in the brackets after the user's connection name. This value is taken from the `metadata` parameter.
{% endtab %}

{% tab title="Code" %}
```json
...
"response": {
	"metadata": {
            "type": "email", //allowed values are "email" and "text"
            "value": "{{body.data.user.email}}"
        }
},
...
```
{% endtab %}
{% endtabs %}

### Error handling

Error handling can be used from the Base tab and follows the same rules.

The only difference is where to use it in what type of connection. For example, in connection types OAuth 1.0 and OAuth 2.0, the error handling should be in the "info" part.

{% content-ref url="../app-structure/base/error-handling.md" %}
[error-handling.md](../app-structure/base/error-handling.md)
{% endcontent-ref %}
