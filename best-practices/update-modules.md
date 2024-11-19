# Update modules

## Update approaches

Bear in mind that there are two approaches to updating entries in a service.

* **Partial Update** - The service updates only specified parameters sent in the API request and other empty parameters will be unchanged. This is the most common approach for APIs.
* **Full Update** - The service requires all parameters to be updated in an update request. If some parameters are omitted, then they will be cleared or overridden to default values in the service. This is extremely user-unfriendly and should be avoided.

## Handling of full update approach

If the API doesn't support a partial update approach, it is needed to add the support on the app's side. Basically, there should be two calls executed instead of only one:&#x20;

* **GET** call - a call that retrieves the current record and saves it in `temp`,
* **UPDATE** call - an update request which contains the user's input merged with the missing parameters from `temp`.

{% hint style="info" %}
Thanks to the handling of the full update approach on the app's side, the user experience will be consistent with all Make apps. Users will not have to handle full updates by themselves or experience data loss.
{% endhint %}

### Example using OR directive

If there are a few parameters available, you can use simple OR `(||)` directive, which ensures that if there is no value in the particular parameter available, the value from `temp` is mapped instead.

#### Communication

```
[
    {
        "url": "/contacts/{{parameters.id}}",
        "method": "GET",
        "response": {
            "temp": {
                "fields": "{{body}}"
            }
        }
    },
    {
        "url": "/contacts/{{parameters.id}}",
        "method": "PUT",
        "body": {
            "name": "{{parameters.name || temp.name}}",
            "email": "{{parameters.email || temp.email}}"
        },
        "response": {
            "output": "{{body}}"
        }
    }
]
```

### Example 2 - IML function

If there are a lot of parameters available, it is worth writing an IML function, which merges the parameters with the output from `temp`.

#### Communication

```javascript
[
    {
        "url": "/contacts/{{parameters.id}}",
        "method": "GET",
        "response": {
            "temp": {
                "fields": "{{body}}"
            }
        }
    },
    {
        "url": "/contacts/{{parameters.id}}",
        "method": "PUT",
        "body": {{updateContact(parameters, temp.fields)}},
        "response": {
            "output": "{{body}}"
        }
    }
]
```

#### IML Function&#x20;

```javascript
function updateContact (parameters, temp) {
     return {
         ...temp,
         ...parameters
     };
}
```

### Example 3 - considerating read-only parameters

There might be read-only parameters, which can't be updated, e. g. `CreatedAt` and `UpdatedAt` parameters. In this case, it is needed to ensure these parameters will be omitted.&#x20;

You can do it by mapping only the parameters, which are allowed, see the [Example using OR Directive](update-modules.md#example-using-or-directive). Or you can implement IML function, see below.

#### IML Function

```javascript
function updates (parameters, temp) {

     function omit(obj, ...props) {
        const result = { ...obj };
        props.forEach(function(prop) {
            delete result[prop];
        });
        return result;
    }

     temp = omit(temp, 'id', 'createdAt', 'updatedAt');
     parameters = omit(temp, 'id');
     //or you can use `iml.omit (temp, 'id', 'createdAt', 'updatedAt')`

     return {
         ...temp,
         ...parameters,
         birthday: parameters.birthday ? iml.formatDate(parameters.birthday, 'YYYY-MM-DD') : temp.birthday
         // additionally you can modify extra fields if necessary. 
     };
}
```
