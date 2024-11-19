# Mappable parameters

## Order of the mappable Parameters

The mappable parameters should follow this priority order:

1. **required** parameters
2. optional parameters
3. **advanced** parameters

{% hint style="warning" %}
**Advanced** parameters should never be **required.**
{% endhint %}

{% tabs %}
{% tab title="Wrong" %}
![Example of Wrong Mappable Parameters](../.gitbook/assets/integromatMappableParamsOrderWrong.png)
{% endtab %}

{% tab title="Right" %}
![Example of Correct Mappable Parameters](../.gitbook/assets/integromatMappableParamsOrderRight.png)
{% endtab %}
{% endtabs %}

When defining the input parameters, try to use the same order as in the integrated service. Place required parameters at the top if it is possible. Position parameters in logical groups.

{% tabs %}
{% tab title="Good practice" %}
```javascript
[
    {
        "name": "firstName"
        "type": "text",
        "label": "First Name"
    },
    {
        "name": "lastName"
        "type": "text",
        "label": "Last Name"
    },
    {
        "name": "email"
        "type": "email",
        "label": "Email"
    },
    {
        "name": "taskId"
        "type": "number",
        "label": "Task ID"
    }
]
```
{% endtab %}

{% tab title="Bad practice" %}
```javascript
[
    {
        "name": "firstName"
        "type": "text"
    },
    {
        "name": "taskId"
        "type": "number"
    },
    {
        "name": "lastName"
        "type": "text"
    },
    {
        "name": "email"
        "type": "email"
    }
]
```
{% endtab %}
{% endtabs %}

### Helps under parameters

Using a help directive, you may specify a hint of what is expected for the parameter when it is not that obvious from the label or the expected value is more complicated. The text should start with a capital letter and end with a period. Supports Markdown, such as  `_italic_`, `**bold**`, `` `monospace` ``, `\n` , or URL `[example](http://example.com)`.

Example:

{% tabs %}
{% tab title="Mappable Parameters" %}
```javascript
{
    "value": "object",
    "label": "Collection or JSON",
    "nested": [
        {
            "name": "metadata",
            "label": "Metadata",
            "help": "Map a Collection or enter JSON in format `{\"key\": \"value\"}` where value can be any type from [Intercom Event Metadata types](https://developers.intercom.com/intercom-api-reference/v1.0/reference#event-metadata-types).\nFor example:\n`{\"order_name\": \"Order123\",\"price\": {\"currency\": \"eur\", \"amount\": 12345}}`\nMaximum 5 entries.",
            "type": "any"
        }
    ]
}
```
{% endtab %}

{% tab title="Appearence in module" %}
![Example of a Help](<../.gitbook/assets/Apps Doc - helpExampleAppearenceGood.png>)
{% endtab %}
{% endtabs %}

### **Advanced parameters** <a href="#advanced-parameters" id="advanced-parameters"></a>

Services like CRMs use large amounts of input parameters. In these cases, you can mark less important parameters as **advanced**_._ When the parameter is marked as advanced, then by default it isn't shown in the GUI. It can be found in the advanced parameters instead after the user clicks on **Show advanced settings**.&#x20;

Example:

```javascript
{
    "name": "externalId",
    "label": "External ID",
    "type": "text",
    "advanced": true
}
```
