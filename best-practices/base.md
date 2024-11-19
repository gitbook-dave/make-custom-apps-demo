# Base

The Base section should contain data that is common to all (or most) requests. At the very least, this should include the root URL, the authorization headers, the error-handling section, and the sanitization.

{% tabs %}
{% tab title="Right" %}
```javascript
{
    "baseUrl": "https://www.example.com/api/v1",
    "headers": {
        "Authorization": "Bearer {{connection.accessToken}}"
    },
    "response": {
        "error": {
            "message": "[{{statusCode}}] {{body.error.message}} (error code: {{body.error.code}})"
        }
    },
    "log": {
        "sanitize": [
            "request.headers.authorization"
        ]
    }
}
```
{% endtab %}

{% tab title="Wrong" %}
![](<../.gitbook/assets/Screenshot 2018-11-22 at 16.31.53.png>)
{% endtab %}
{% endtabs %}

### Base URL

{% content-ref url="../app-structure/base/base-url.md" %}
[base-url.md](../app-structure/base/base-url.md)
{% endcontent-ref %}

Make sure that the Base URL uses the URL of the API, which is shared among all modules or their majority.

{% hint style="warning" %}
In case of a request for approval of your app by Make, make sure that the base URL is a **production** **endpoint** with a domain that belongs to the app itself.&#x20;

Apps with development or staging URLs, or apps with a domain belonging to a cloud computing service, will not be approved!
{% endhint %}

When the service has a different domain for each user, the domain should be asked for in the connection and then the value should be used in the Base tab.

{% tabs %}
{% tab title="Right" %}
An example from Mailerlite app:

```
{
    "baseUrl": "https://api.mailerlite.com/api/v2"
}
```
{% endtab %}

{% tab title="Right (Different Domain)" %}
An example from Freshsales app:

```
{
    "baseUrl": "https://{{connection.domain}}.freshsales.io"
}
```
{% endtab %}

{% tab title="Wrong (Different Domain)" %}
```
{
    "baseUrl": "https://mydomain.freshsales.io"
}
```

{% hint style="info" %}
The "mydomain" should be a variable used from the Connection.
{% endhint %}
{% endtab %}

{% tab title="Wrong (app will not be approved)" %}
```
{
    "baseUrl": "https://mailerlite.heroku.com/development"
}
```
{% endtab %}
{% endtabs %}

### Authorization and sanitization

{% content-ref url="../app-structure/base/authorization.md" %}
[authorization.md](../app-structure/base/authorization.md)
{% endcontent-ref %}

{% content-ref url="../app-structure/base/sanitization.md" %}
[sanitization.md](../app-structure/base/sanitization.md)
{% endcontent-ref %}

The Base section should also have authorization, which is common for all modules. This authorization should use the API Key, Access Token, or Username and Password entered in the connection. The sanitization should hide all these sensitive parameters.

Examples of possible authorization and sanitization:

{% tabs %}
{% tab title="API Key" %}
```javascript
{
...
    "headers": {
        "Authorization": "Token {{connection.apiKey}}"
    },
    "log": {
        "sanitize": [
            "request.headers.authorization"
        ]
    }
...
}
```
{% endtab %}

{% tab title="Access Token" %}
```javascript
{
...
    "qs": {
        "access_token": "{{connection.accessToken}}"
    },
    "log": {
        "sanitize": [
            "request.qs.access_token"
        ]
    }
...
}
```
{% endtab %}

{% tab title="Basic auth" %}
```javascript
{
...
    "headers": {
        "authorization": "Basic {{base64(connection.username + ':' + connection.password)}}"
    },
    "log": {
        "sanitize": [
            "request.headers.authorization"
        ]
    }
...    
}
```
{% endtab %}

{% tab title="Secret in request body" %}
```javascript
{
...
    "body": "There is something {{parameters.secret}} hidden here.",
    "type": "raw",
    "log": {
        "sanitize": [
            "request.body<parameters.secret>"
        ]
    }
...
}
```
{% endtab %}
{% endtabs %}

### Error handling

Each service sends an error message when an error occurs. This most of the time happens when the request has wrong parameters or values or when the service has an outage. That's why error handling is required.

{% hint style="warning" %}
In case of a request for approval of your app by Make, make sure error handling is correctly implemented!
{% endhint %}

{% content-ref url="../app-structure/base/error-handling.md" %}
[error-handling.md](../app-structure/base/error-handling.md)
{% endcontent-ref %}

The error handling code should correspond to the structure of the server response.\
Let's assume that the JSON response has the following format in the cases where something goes wrong:

```
{
    "error": {
        "code": "E101",
        "message": "The company with the given ID does not exist."
    }
}
```

Here's how the error section should (and should not) look:

{% tabs %}
{% tab title="Right" %}
```javascript
"response": {
    "error": {
        "message": "[{{statusCode}}] {{body.error.message}} (error code: {{body.error.code}})"
    }
}
```

The error object in our example contains the `code` and `message` fields, but not a `text` field. It is also important to show the status code of the error, this can be accessed using the `statusCode` keyword. So in the case of HTTP error 400, the error message could look like this:

`[400] The company with the given ID does not exist. (error code: E101)`
{% endtab %}

{% tab title="Wrong" %}
```javascript
"response": {
    "error": {
        "message": "{{body.error.text}}"
    }
}
```

The error object in our example contains the `code` and `message` fields, but not a `text` field.
{% endtab %}
{% endtabs %}
