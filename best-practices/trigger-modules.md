# Trigger modules

## Epoch in polling trigger

The trigger module has an Epoch section that defines what "Choose where to start" looks like. This section is an RPC that uses everything in COMMUNICATION including the pagination. This means there can be an issue if the user has too many objects which could be returned by this RPC so that is why a `"limit"` parameter should be specified here.

‌ The "limit" parameter should be a static number which should be at max 300 or 3 \* number of objects per page.

{% tabs %}
{% tab title="Wrong" %}
![No "limit" parameter](../.gitbook/assets/integromatTriggerEpochWrong.png)
{% endtab %}

{% tab title="Right" %}
![](../.gitbook/assets/integromatTriggerEpochRight.png)
{% endtab %}
{% endtabs %}

## API endpoint requires `from` and/or `to` date parameters

Some API services require `date` parameters that define the interval of records to be retrieved, e.g. `from` and `to`, `fromDate` and `toDate`, etc.

In this case, it is important to handle the `date` parameters correctly.

{% tabs %}
{% tab title="Wrong" %}
<figure><img src="../.gitbook/assets/Screenshot 2023-06-22 at 15.33.27.png" alt=""><figcaption><p>From and To parameters required from the user</p></figcaption></figure>

{% hint style="info" %}
Notice the `From` and `To` parameters that are required.

Since triggers don't allow mapping/functions, the user has to "hardcode" the `From` and `To` dates. Therefore, Make will always request the same interval of records.
{% endhint %}
{% endtab %}

{% tab title="Right" %}
<figure><img src="../.gitbook/assets/Screenshot 2023-06-22 at 13.24.37.png" alt=""><figcaption><p>Start Date and End Date are not available to user</p></figcaption></figure>

{% hint style="info" %}
Notice there is no `From` or `To` available to the user.
{% endhint %}
{% endtab %}

{% tab title="Communication Code" %}
```javascript
...
"qs": {
         "from": "{{data.lastDate}}",
         "to": "{{now}}"
      },
...

```

{% hint style="info" %}
Notice  the mapped `data.lastDate` [IML variable](https://docs.integromat.com/apps/app-structure/modules/trigger#available-iml-variables) that is available in polling triggers.&#x20;

This variable is available to the user in **Choose where to start** setting.
{% endhint %}

<figure><img src="../.gitbook/assets/Screenshot 2023-06-22 at 13.41.16 (1).png" alt=""><figcaption><p>Choose where to start feature</p></figcaption></figure>

**The behavior of the supported options:**

* **From now on** - The current date will be sent.
* **Since specific date** - The date provided will be sent.
* **Choose manually** - The date of the chosen item will be sent.
* **All** - The default date `1970-01-01` will be sent.
{% endtab %}
{% endtabs %}

