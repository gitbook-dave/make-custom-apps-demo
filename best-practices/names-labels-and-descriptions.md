# Names, labels & descriptions

## Module names

{% hint style="warning" %}
A name of a module, an RPC, or a custom IML function should not match with any reserved word in JavaScript. See the list of reserved words in JavaScript [here](https://www.w3schools.com/js/js\_reserved.asp).&#x20;
{% endhint %}

## Module labels

Every module should have a label that precisely describes the module's use. For each type of module, there is a standard naming convention. But it may change depending on the functionality of the module. The label should be composed of the verb expressing the intended action (Create, Update, Watch, etc.) and the name of the entity being processed (Customer,  Invoice,  Table, etc.).

Names of modules follow the English format - they are capitalized - Specifically, they use Title Case - refer to [Chicago Manual of Style](https://en.wikipedia.org/wiki/Title\_case#Chicago\_Manual\_of\_Style). Basically, every word is capitalized except for articles, prepositions, and conjunctions.

{% tabs %}
{% tab title="Good practice" %}
* Watch Events
* Create a Report
* Update a Record
* List Photos
* Search Files
* Add Members to a Group
* Get a Group's Info
{% endtab %}

{% tab title="Bad practice" %}
* Watch events
* Create a report
* Make a call
* List photos
* Search files
* Add members to Group
* Get group info
{% endtab %}
{% endtabs %}

### Triggers and instant triggers (webhooks) <a href="#triggers-and-instant-triggers-webhooks" id="triggers-and-instant-triggers-webhooks"></a>

These modules watch for new data in a given service and return it. Compose the label according to this pattern **Watch \<watched node>**

Examples:

* Watch Events
* Watch Photos
* Watch Deleted Files

### Actions <a href="#actions" id="actions"></a>

These modules write data into a service, modify data in the service, or retrieve a single result. Compose the label using simple verbs like **Create, Get, Update** and **Delete** and the modified or created node. Use the naming convention of the service you are implementing.

Examples:

* Create a Note
* Update a File
* Get a User
* Delete a Task

### &#x20;Searches <a href="#searches" id="searches"></a>

These modules retrieve data from the service and allow retrieving one or more results. Compose the label using simple verbs like **Search** or **List**. Use the naming convention of the service you are implementing.

Examples:

* Search Files
* List Tasks

## Module descriptions

In a few words, describe the functionality of the module. Write the description in the third person and capitalize only the first letter of the first word in the description (like a normal sentence structure).&#x20;

Example: Description for the module **Update a Time Entry:**

{% tabs %}
{% tab title="Good practice" %}
> Updates a time entry for a specific user.
{% endtab %}

{% tab title="Bad practice" %}
> Update a Time Entry for a Specific User.

{% hint style="info" %}
The description is missing "s" for word "Update". The "Time Entry" and "Specific User" should be lowercase.
{% endhint %}
{% endtab %}
{% endtabs %}

**Triggers** use the "Triggers when..." in the descriptions. For example, the description for the module **Watch New Users** should be: **"**Triggers when a new user is created."

## Names and labels of input and output parameters <a href="#names-and-labels-of-input-and-output-parameters" id="names-and-labels-of-input-and-output-parameters"></a>

For labels, try to use the same names and conventions as in the integrated service. It helps users to use the app in Make and not be confused.

For variable names, use the same names that come from the service API. It helps when debugging for both advanced Make users and support agents. Ideally, the output of the module should be the same as the response from the API.

Example:

{% tabs %}
{% tab title="Output parameters" %}
```javascript
[
    {
        "name": "id",
        "label": "ID",
        "type": "text"
    },
    {
        "name": "note",
        "label": "Note",
        "type": "text"
    },
    {
        "name": "firstName",
        "label": "First Name",
        "type": "text"
    },
    {
        "name": "shortUrl",
        "label": "Short URL",
        "type": "url"
    }
]
```
{% endtab %}

{% tab title="API response" %}
```javascript
{
    "id": "59b1396a4a22a7a3bfc78e22",
    "note": "Hey",
    "firstName": "John",
    "shortUrl": "https://trello.com/c/LdcrM4wa"
}
```
{% endtab %}
{% endtabs %}

### Abbreviations

Be sure to use the correct uppercase for abbreviated words, such as ID, IDs, URL, GPS, VAT, etc.
