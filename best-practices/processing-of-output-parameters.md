# Processing of output parameters

## How to process the API response <a href="#how-to-process-the-api-response" id="how-to-process-the-api-response"></a>

The best approach is to return the API response as it is. In many cases, the response varies based on the user who is using the app, as responses can contain different custom fields, etc. If the response returned is unchanged, and if still all the parameters aren't described in the **output parameters**, Make will automatically learn additional parameters from actual incoming data and propose them for mapping.

{% tabs %}
{% tab title="Good practice (Search)" %}
```javascript
"response": {
    "output": "{{item}}",
    "iterate": "{{body}}"
}
```
{% endtab %}

{% tab title="Bad practice (Search)" %}
```javascript
"response": {
    "output": {
        "id": "{{item.id}}",
        "name": "{{item.name}}"
    },
    "iterate": "{{body}}"
}
```
{% endtab %}

{% tab title="Good practice (Action)" %}
```javascript
"response": {
    "output": "{{body}}"
}
```
{% endtab %}

{% tab title="Bad practice (Action)" %}
```javascript
"response": {
    "output": {
        "id": "{{body.id}}",
        "name": "{{body.name}}"
    }
}
```
{% endtab %}
{% endtabs %}

## Response output <a href="#response-output" id="response-output"></a>

A module's response output should be defined for the case when a request is fulfilled successfully. The output definition should under no conditions contain error messages (this belongs in the Base section's error handling) nor the additional metadata which may arrive bundled with the actual response information.

{% tabs %}
{% tab title="Wrong" %}
No matter the module type, the output shouldn't be defined like this:

![](../.gitbook/assets/integromatResponseOutputWrong.png)
{% endtab %}
{% endtabs %}

## Showing dates correctly

{% hint style="warning" %}
Requires IML functions enabled.
{% endhint %}

There are multiple ways how a date can be returned from the service, either as a timestamp or in any format the service finds fit. It is important to parse this date to our ISO 8601 format so it is shown in an output of the module as a date using the users' localization and timezone.

Make is using ISO 8601 format: **YYYY-MM-DDTHH:mm:ss.sssZ**

Any other format, even just without milliseconds won't be shown correctly in the output and needs to be parsed using an IML function.

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

## Interface

The interface describes the structure of output bundles and specifies the parameters which are seen in the next modules. It should contain the full response from the API, including nested parameters.&#x20;

You can generate an interface using our **Interface Generator**, learn how in [#interface-generator](../app-blocks/interface.md#interface-generator "mention") section.

{% content-ref url="../app-blocks/interface.md" %}
[interface.md](../app-blocks/interface.md)
{% endcontent-ref %}
