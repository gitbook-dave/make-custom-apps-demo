# Action and search modules

Suppose you want to retrieve all users, that are registered on your service. You can’t use [**Action**](https://integromat.github.io/apps/action.html), because it returns only a single result. You will have to create a [**Search**](https://integromat.github.io/apps/searches.html) module for this.

The communication for [**Search**](https://integromat.github.io/apps/search.html) is the same as for **Action**, except **Search** has an [`iterate`](https://integromat.github.io/apps/search.html#iterate) directive, which specifies where are the items located inside the body.

For the next example, suppose that when you call `/users` on your service, you will get a list of users in `body.data`.

This example will correctly output each user that was returned:

```javascript
{
    "url": "/users",
    },
    "response": {
        "output": "{{item}}",
        "iterate": "{{body.data}}",
        "limit": "{{parameters.limit}}"
    }
}
```

## Iteration and pagination <a href="#iteration-and-pagination" id="iteration-and-pagination"></a>

An [Action](https://docs.integromat.com/apps/app-structure/modules/action) module should never contain `pagination` or the `iterate` directive. If you need to return multiple objects, create a [Search](https://docs.integromat.com/apps/app-structure/modules/search) module instead.

{% tabs %}
{% tab title="Wrong" %}
![Example of Wrong Implementation of Search Endpoint as Action Module](../.gitbook/assets/integromatIterationPaginationWrong.png)
{% endtab %}

{% tab title="Right" %}
![Example of Correct Implementation of Search Module and Pagination Directive](../.gitbook/assets/integromatIterationPaginationRight.png)
{% endtab %}
{% endtabs %}

## Pagination parameters <a href="#pagination-parameters" id="pagination-parameters"></a>

The `pagination` section should only contain parameters directly influencing the actual pagination. These will be merged with the rest of the parameters defined in the `qs` section, so there is no need to define them all again.

{% tabs %}
{% tab title="Wrong" %}
![Example of Wrong Implementation of Pagination Directive](<../.gitbook/assets/integromatPaginationParamsWrong (1).png>)

{% hint style="info" %}
The pagination directive contains `"since"`, `"until"` and `"limit"` parameters that are already defined in query string ("qs").&#x20;
{% endhint %}
{% endtab %}

{% tab title="Right" %}
![Example of Correct Implementation of Pagination Directive](../.gitbook/assets/integromatPaginationParamsRight.png)

{% hint style="info" %}
The pagination contains only the `"offset"` parameter.
{% endhint %}
{% endtab %}
{% endtabs %}

## Limiting output

The modules type Search and Trigger(polling) should return everything including by pagination. However, these modules should also allow users to limit their output, that is, how many bundles they return.

This can be achieved by setting up the [`limit`](https://docs.integromat.com/apps/structure-blocks/api/handling-responses#limit) parameter in the response. By default, this parameter is added to the Trigger (polling) modules and should be required. In Search modules, this parameter should NOT be required so if a user leaves it empty, the Search modules return everything. Its default value should be set to 10.

Search module limit example:

{% tabs %}
{% tab title="Communication" %}
```javascript
{
    "url": "/clients",
    "method": "GET",
    "qs": {
        "per_page": 100
    },
    "response": {
        "limit": "{{parameters.limit}}",
        "output": "{{item}}",
        "iterate": "{{body.clients}}"
    },
    "pagination": {
        "qs": {
            "page": "{{pagination.page}}"
        },
        "condition": "{{body.next_page}}"
    }
}
```
{% endtab %}

{% tab title="Mappable parameters" %}
```javascript
[
    {
        "name": "limit",
        "label": "Limit",
        "type": "uinteger",
        "help": "Number of clients to return",
        "default": 10
    }
]
```

{% hint style="warning" %}
The `limit` parameter should not be set to `"required":true` (except for polling trigger modules).\
The `limit` parameter should never be set to `"advanced":true`.
{% endhint %}
{% endtab %}
{% endtabs %}
