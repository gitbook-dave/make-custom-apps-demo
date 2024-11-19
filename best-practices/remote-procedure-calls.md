# Remote Procedure Calls

## Use cases of RPCs

Remote procedures are used to get live data from a service. More information about remote procedures can be found [here](../app-structure/rpcs/).

Use RPCs for every field that accepts parameters like IDs and other stuff that is hard to guess or get for users.

{% tabs %}
{% tab title="Appearence in a Module" %}
<figure><img src="../.gitbook/assets/Screen Shot 2022-09-07 at 14.45.27.png" alt=""><figcaption><p>Example of RPC</p></figcaption></figure>
{% endtab %}

{% tab title="Mapping Mode" %}
<figure><img src="../.gitbook/assets/Screen Shot 2022-09-07 at 14.46.51.png" alt=""><figcaption><p>RPC set to Mapping Mode</p></figcaption></figure>

{% hint style="info" %}
Notice, that in the mapping mode, user has to enter/map option's ID instead of the label.
{% endhint %}
{% endtab %}
{% endtabs %}

Also, RPCs come in handy in a case, when a user only needs to understand the functionality of the module, mostly the list of available parameters in the interface. In this case, the aim is not to offer a complete list of all items, but a sample of the last 100 or so items the user could select from when testing the module or setting up the scenario for the first time, before replacing it with mapped data used in automation.

## Mode edit

When adding an RPC to a **Get**, **Update,** or **Delete** module, it is required to add:

```
"mode": "edit",
```

to the code so when a user first opens the module, they will be able to immediately map the value. However, if needed, they can also switch to getting the value from an RPC.

{% tabs %}
{% tab title="Good Practice" %}
```javascript
{
    "name": "userId",
    "type": "select",
    "label": "User ID",
    "options": "rpc://getUsers",
    "mode": "edit"
}
```
{% endtab %}

{% tab title="Bad Practice" %}
```javascript
{
    "name": "userId",
    "type": "select",
    "label": "User ID",
    "options": "rpc://getUsers"
}
```
{% endtab %}
{% endtabs %}

When it comes to **Search**/**List** modules, it **depends** on the hierarchy level of the entity. If the entity is up in the hierarchy, e.g. a “customer” or a “deal”, and there are not many RPCs in the input, they **should not** have the mode set to “edit”. However, if the entity is low in the hierarchy, e.g. "E-mail attachment", it **should** have the mode set to “edit” since the user will probably not want to list attachments of a single e-mail repeatedly.

<figure><img src="../.gitbook/assets/Screen Shot 2022-09-07 at 14.36.04.png" alt=""><figcaption><p>Example of List Module with RPC with Mode Edit Set</p></figcaption></figure>

Finally, a **Create** module **should not** have the mode set to "edit", **unless it contains a very large number of RPCs in its input**. This is because pre-loading a large number of RPCs would significantly increase the waiting time for the user.

## Pagination and limits

Just like modules, RPCs can use pagination to show more records than just the ones on the first page. However, limits should be also set on how many objects the RPC shows so it doesn't load forever.

The limit should be between 300-500 if the API returns 100 or more objects per page. If the API returns less than 100 per page, then the limit should be 3 times the amount of objects per page.

For example, if API returns 25 records per page, the limit should be 75. You can also set a condition for the pagination to stop further requests when no more data is needed.

{% tabs %}
{% tab title="Right" %}
```json
 {
	"url": "/contacts",
	"method": "GET",
	"qs": {
		"pageSize": 25
	},
	"response": {
		"limit": 75
		"output": {
			"label": "{{item.displayname}}",
			"value": "{{item.id}}"
		},
		"iterate": "{{body.data}}"
	},
	"pagination": {
		"condition": "{{pagination.page <= 3}}",
		"qs": {
			"page": "{{pagination.page}}"
		}
	}
}
```
{% endtab %}

{% tab title="Wrong (no limit)" %}
```json
 {
	"url": "/contacts",
	"method": "GET",
	"qs": {
		"pageSize": 25
	},
	"response": {
		"output": {
			"label": "{{item.displayname}}",
			"value": "{{item.id}}"
		},
		"iterate": "{{body.data}}"
	},
	"pagination": {
		"qs": {
			"page": "{{pagination.page}}"
		}
	}
}
```

![Example of Missing Limit](../.gitbook/assets/integromatRpcsLimitWrong.png)
{% endtab %}
{% endtabs %}
