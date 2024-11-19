# Modules

## Module types <a href="#module-types" id="module-types"></a>

Modules should be associated with the correct type, depending on their functionality. Detailed descriptions of different types of modules can be found in our [Modules](../app-structure/modules/) docs as well as in the [Best Practices](names-labels-and-descriptions.md) guide.

{% tabs %}
{% tab title="Wrong" %}
![Module of Type Action](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LC12sgBWZWwjEbbd84M%2F-LRuXwrtWjHjwWlxs\_yH%2F-LRulzHYv4JleXbJ9kkJ%2Fimage.png?alt=media\&token=8939e884-a574-4004-924e-ceea29507739)

The module can return more than one campaign object, so it should be of the type [Search](https://docs.integromat.com/apps/app-structure/modules/search).
{% endtab %}

{% tab title="Right" %}
![Module of Type Search](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LC12sgBWZWwjEbbd84M%2F-LRuXwrtWjHjwWlxs\_yH%2F-LRunBR7fs5Nfzi060G3%2FScreenshot%202018-11-22%20at%2010.41.40.png?alt=media\&token=040eafea-f976-4d57-8f93-edbf2ffaa71b)

The module can return more than one campaign object, so it should be of type [Search](https://docs.integromat.com/apps/app-structure/modules/search).
{% endtab %}
{% endtabs %}

## Universal module

Each app should have a universal module. This module is there to allow users to use not supported API endpoints using their connection created to the app.

More about this module can be found [here](../app-structure/modules/universal-module/).

Make sure this module has:

* correct label and description,
* correct `url` which starts with the base URL,
* correct connection.

## Using the base URL <a href="#using-the-base-url" id="using-the-base-url"></a>

All of the modules should build on top of `baseURL` from the Base section (simply by starting with a forward slash `/`). It is very unlikely that a single module will need to have a completely different URL than the rest.

{% tabs %}
{% tab title="Wrong" %}
![Example of Wrong URL](../.gitbook/assets/integromatModulesUrlWrong.png)

The underlined part which is the same for each module should be in the Base tab.
{% endtab %}

{% tab title="Right" %}
![Example of Correct URL](<../.gitbook/assets/integromatModulesUrlRight (1).png>)

Modules "url" should start with forward slash `/`
{% endtab %}
{% endtabs %}
