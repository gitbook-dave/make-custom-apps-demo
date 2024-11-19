# Search modules

## Support for query and filtering options

Certain APIs provide support for custom queries or filters when searching records, such as invoices. In Make, our goal is to offer query and filter capabilities to both regular and advanced users.

Therefore, we have implemented two methods of achieving this functionality, and ideally, users should be able to choose between the two options.

#### A predefined query

We have utilized the familiar filter setup format found in Scenario Builder. With this approach, users are not required to learn the query format. Instead, they can simply set up the query in a manner similar to configuring filters.&#x20;

When the module is executed, a custom IML function constructs the query, adhering to the specified format.

#### A custom query

Users have the option to manually compose their own queries. This feature is particularly valuable when the API supports new operators that are not yet available within the module.

To assist users in leveraging the query field effectively, the following helpful information should be provided:

* Query format: The guidelines for structuring the query.
* Example of a functional query: An illustrative sample query as reference.
* API documentation URL: Direct access to the API documentation with query specification.

{% tabs %}
{% tab title="Filters in a module" %}
<figure><img src="../.gitbook/assets/Screenshot 2023-05-17 at 12.25.59 (1).png" alt=""><figcaption><p>Example of filters</p></figcaption></figure>

{% hint style="info" %}
Notice, that the operators are grouped by a category.
{% endhint %}
{% endtab %}

{% tab title="Query in a module" %}
<figure><img src="../.gitbook/assets/Screenshot 2023-05-17 at 12.24.57.png" alt=""><figcaption><p>Example of a query</p></figcaption></figure>

{% hint style="info" %}
Notice the available `AND` rule.
{% endhint %}
{% endtab %}

{% tab title="Custom query in a module" %}
<figure><img src="../.gitbook/assets/Screenshot 2023-05-17 at 12.28.38.png" alt=""><figcaption><p>Example of a custom query</p></figcaption></figure>

{% hint style="info" %}
Notice the help containing the query pattern and the valid query example together with a link to available docs.
{% endhint %}
{% endtab %}

{% tab title="Mappable parameters" %}
```json
[
   {
      "name":"type",
      "label":"Search by",
      "type":"select",
      "required":true,
      "mappable":false,
      "options":[
         {
            "label":"field",
            "value":"filter",
            "nested":[
               {
                  "name":"filter",
                  "label":"Filter",
                  "type":"filter",
                  "grouped":false,
                  "options":{
                     "logic":"and", // --> to support AND only
                     // "logic": "or", --> to support OR only
                     // do not use "logic" parameter --> to support both
                     "store":[
                        {
                           "label":"Status",
                           "value":"Status"
                        },
                        {
                           "label":"Invoice number",
                           "value":"invoiceNumber"
                        }
                     ],
                     "operators":[
                        {
                           "label":"Text",
                           "options":[
                              {
                                 "label":"Contains",
                                 "value":"CTSTR"
                              },
                              {
                                 "label":"Equals",
                                 "value":"EQ"
                              }
                           ]
                        },
                        {
                           "label":"Number",
                           "options":[
                              {
                                 "label":"Less than",
                                 "value":"LT"
                              },
                              {
                                 "label":"More than",
                                 "value":"GT"
                              }
                           ]
                        }
                     ]
                  }
               }
            ]
         },
         {
            "label":"user-defined condition",
            "value":"query",
            "nested":[
               {
                  "name":"query",
                  "label":"Query",
                  "type":"text",
                  "help":"Example: `{FIELD_NAME}~{OPERATOR}~{VALUE}|AND|{FIELD_NAME}~{OPERATOR}~{VALUE}`. E.g. `customer_id~GT~1234|AND|status~EQ~Open`. More examples how to use filters are in [docs](https://myapi.com/how-to-use-filters).",
                  "required":true
               }
            ]
         }
      ]
   },
   {
      "name":"limit",
      "label":"Maximum number of returned invoices",
      "default":10,
      "type":"uinteger"
   }
]
```

{% hint style="info" %}
Notice the parameter `logic` that defines the logical relationship between different conditions within a query.

Supported values are `AND` and/or `OR.`
{% endhint %}
{% endtab %}

{% tab title="Communication" %}
```json
{
    ...
    "qs": {
        "filter": "{{if(parameters.type === 'filter', filter(parameters.filter), parameters.query)}}"
    },
    ...
```

{% hint style="info" %}
Notice that a custom IML function `filter` is used in order to properly build the query.
{% endhint %}
{% endtab %}

{% tab title="Custom IML Function" %}
```javascript
function filter(filter) {

    if(!filter) return;

    return filter[0].map(and => {
        if(!and.a && !and.o && !and.b) return;
        return `${and.a}~${and.o}~${and.b}`;
    }).join('|AND|');

}
```

{% hint style="info" %}
The parameters `a`, `o`, and `b` represent the following:

`a` = name of the parameter, e.g. `status`

`o` = operator, e.g. `EQ`

`b` = value, e.g. `open`

Example of the output query:

`invoiceNumber~GT~1234|AND|status~EQ~Open`
{% endhint %}
{% endtab %}
{% endtabs %}
