# Processing of input parameters

## Mapping parameters

### Mapping all parameters

{% tabs %}
{% tab title="Communication - Bad practice" %}
```json
{
    ...
    "body": {
        "firstName": "{{parameters.firstName}}",
        "lastName": "{{parameters.lastName}}",
        "email": "{{parameters.email}}"
    },
    ...
}
```

{% hint style="info" %}
Notice, that you have to map every single parameter correctly.&#x20;

There is a risk of a typo or omission of a parameter.
{% endhint %}
{% endtab %}

{% tab title="Communication - Good practice" %}
```json
{
    ...
    "body": "{{parameters}}",
    ...
}
```

{% hint style="info" %}
Thanks to this approach, all parameters from the modules will be sent to the API.
{% endhint %}
{% endtab %}

{% tab title="Mapping parameters" %}
```json
[
    {
        "name": "email",
        "type": "email",
        "label": "Email address",
        "required": true
    },
	{
        "name": "firstName",
        "type": "text",
        "label": "First Name",
        "required": true
    },
    {
        "name": "lastName",
        "type": "text",
        "label": "Last Name",
        "required": true
    }
]
```
{% endtab %}
{% endtabs %}

### Using an IML function or omitting a parameter

Sometimes, you don't want to map all parameters in the `body` for some reason:

* the parameter shouldn't be sent at all (technical parameters such as selects, etc.)
* the parameter should be sent somewhere else than in the `body`, e.g. in the `url`
* the parameter has to be wrapped in an IML or custom IML function

{% tabs %}
{% tab title="Communication - Bad practice" %}
```json
{
    "url": "/contact/{{parameters.id}}",
    "method": "PUT",
    "body": {
        "email": "{{parameters.email}}",
        "firstName": "{{parameters.firstName}}",
        "lastName": "{{parameters.lastName}}",
        "registrationDate": "{{formatDate(parameters.registrationDate, 'YYYY-MM-DD')}}"
        
    },
    ...
}
```

{% hint style="info" %}
Notice, that you have to map every single parameter correctly.&#x20;

There is a risk of a typo or omission of a parameter.
{% endhint %}
{% endtab %}

{% tab title="Communication - Good practice" %}
```json
{
    "url": "/contact/{{parameters.id}}",
    "method": "PUT",
    "body": {
        "{{...}}": "{{omit(parameters, 'id', 'registrationDate')}}",
        "registrationDate": "{{formatDate(parameters.registrationDate, 'YYYY-MM-DD')}}"
        
    },
    ...
}
```

{% hint style="info" %}
Notice, that `"{{...}}"` lists all available parameters from the module and allows adding other parameters.&#x20;

The `omit()` function allows the removal of parameters, that are used somewhere else, shouldn't be used, or require special attention.&#x20;

In this case, the `id` parameter is already used in the url, and the `registrationDate` parameter is wrapped in `formatDate` IML function.
{% endhint %}
{% endtab %}

{% tab title="Mapping parameters" %}
```json
[
    {
        "name": "id",
        "type": "string",
        "label": "Contact ID",
        "required": true
    },
    {
        "name": "email",
        "type": "email",
        "label": "Email address"
    },
	{
        "name": "firstName",
        "type": "text",
        "label": "First Name"
    },
    {
        "name": "lastName",
        "type": "text",
        "label": "Last Name"
    },
    {
        "name": "registrationDate",
        "type": "date",
        "label": "Date of Registration"
    }
]
```
{% endtab %}
{% endtabs %}

## Handling arrays, nulls, and empty strings

Make and other third-party services transport values in many different formats. It is important to know how to handle the value types of _arrays, nulls, and empty strings_.

### **Bad practices**

{% tabs %}
{% tab title="Omitting of null or empty string parameteres" %}
```javascript
{
    "url": "/messages.json",
    "method": "POST",
    "body": {
        "status": "active",
        "content": "{{ifempty(parameters.content, undefined)}}"
    },
    ...
}
```

It isn't possible to send a `null` value to a service.

```javascript
{
    "url": "/messages.json",
    "method": "POST",
    "body": {
        "status": "active",
        "content": "{{if(parameters.content, paramteres.content, undefined)}}"
    },
    ...
}
```

It isn't possible to send a `null`, empty string, and 0 (zero) value to a service.
{% endtab %}

{% tab title="Omitting of empty arrays" %}
```javascript
{
    "url": "/tasks.json",
    "method": "POST",
    "body": {
        "status": "active",
        "tags": "{{if(length(parameters.tags) > 0, paramters.tags, undefined)}}"
    },
    ...
}
```

It isn't possible to send empty array to a service. _E.g. User wants to remove all tags from a task._
{% endtab %}
{% endtabs %}

Let users decide what parameters they want to send to the service. Make has a feature to show how to process values. This feature allows users to define exactly how Make should behave when the value is "empty". For example, if a user defines that they want to send a specific field  to a service even if the value is `null` , empty string, or an empty array,  it will be sent to the service. In module communication, config passes parameters without any modification.

## Date parameters

When a field is a type "date", it should be possible to use our keyword "now" as a value, which means, the field should accept ISO-8601 date format and if the service requires only the date (no time) or a different format like timestamp, this formatting should happen inside the module.

{% hint style="warning" %}
Users of the app should never be prompted to format the date inputs the way API requires! Such apps will not be approved by Make.
{% endhint %}

{% tabs %}
{% tab title="Good Practice" %}
**Communication**:

```javascript
{
    "url": "/api/users",
    "method": "POST",
    "body": {
        "name": "{{parameters.name}}",
        "birthday": "{{formatDate(parameters.birthday, 'YYYY-MM-DD')}}",
        "due_date": "{{formatDate(parameters.due_date, 'X')}}"
    },
    "response": {
        "output": "{{body}}"
    }
}
```

{% hint style="success" %}
Parameter `birthday` is required to have format YYYY-MM-DD and parameter `due_date` is required to be a timestamp by the service, so the formatting happens inside the Communication part of the module.
{% endhint %}

**Parameters**:

```javascript
[
    {
        "name": "name",
        "type": "text",
        "label": "Name"
    },
    {
        "name": "birthday",
        "type": "date",
        "label": "Birthday"
    },
    {
        "name": "due_date",
        "type": "date",
        "label": "Due Date"
    }
]
```

{% hint style="success" %}
The parameters `birthday` and `due_date` are correctly **date** typed and don't need to be formatted by the user, he can freely work with `now` keyword.
{% endhint %}
{% endtab %}

{% tab title="Bad Practice" %}
**Communication**:

```javascript
{
    "url": "/api/users",
    "method": "POST",
    "body": {
        "name": "{{parameters.name}}",
        "birthday": "{{parameters.birthday}}",
        "due_date": "{{parameters.due_date}}"
    },
    "response": {
        "output": "{{body}}"
    }
}
```



{% hint style="danger" %}
Parameter `birthday` is required to have format YYYY-MM-DD and parameter `due_date` is required to be a timestamp but nothing is done with the value.
{% endhint %}



**Parameters**:

```javascript
[
    {
        "name": "name",
        "type": "text",
        "label": "Name"
    },
    {
        "name": "birthday",
        "type": "date",
        "label": "Birthday",
        "help": "Format YYYY-MM-DD"
    },
    {
        "name": "due_date",
        "type": "integer",
        "label": "Due Date",
        "help": "Enter a timestamp"
    }
]
```

{% hint style="danger" %}
The parameter `due_date` is an incorrect type and `birthday` is required to be formated by the user.
{% endhint %}
{% endtab %}
{% endtabs %}

## Query String (QS)

The query string parameters should be defined using the `qs` object in order not to be embedded directly in the URL. Embedded parameters are those parameters that are after a question mark.

This will enforce the correct encoding of both static and dynamic parameters.

{% tabs %}
{% tab title="Wrong" %}
![Example of Wrong Implementation of Parameters in URL](../.gitbook/assets/integromatQueryStringWrong.png)
{% endtab %}

{% tab title="Right" %}
![Example of Correct Implementation of Parameters in QS](../.gitbook/assets/integromatQueryStringRight.png)
{% endtab %}
{% endtabs %}

If you need to specify a query string parameter, you can do:

```javascript
{
    "url": "http://yourservice.com/api/users/{{parameters.userId}}?includeAdvanced={{parameters.advanced}}"
}
```

But a better way is to use a special `qs` collection.

The `headers`, `qs`, and `body` collections represent request headers, query string parameters, and body payload. The key is the variable/header name and the value is the variable/header value. You don’t need to escape values inside those collections.

The above request can be rewritten as:

```javascript
{
    "url": "http://yourservice.com/api/users/{{parameters.userId}}",
    "qs": {
        "includeAdvanced": "{{parameters.advanced}}"
    }
}
```

{% hint style="info" %}
**NOTE**: `qs` and `headers` are single-level collections, meaning that you cannot specify nested objects in their parameters:
{% endhint %}

```
{
    "qs": {
        "someProp": {
            "anotherOne": {
                "and-one-more": "THIS WILL NOT WORK"
            }
        }
    }
}
```

**The example above will not work**. But if you want dot notation for some reason, you can use it directly in the parameter name:

```javascript
{
    "qs": {
        "someProp.anotherOne.and-one-more": "THIS WILL WORK"
    }
}
```

This will create a query string that looks like this: `?someProp.anotherOne.and-one-more=THIS%20WILL%20WORK`

