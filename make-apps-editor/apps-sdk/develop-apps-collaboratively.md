# Develop apps collaboratively

{% hint style="info" %}
The collaborative development is facilitated by the Git for apps feature in the VS Code extension. The supported operations are documented in this [section](local-development-for-apps/).
{% endhint %}

## Prerequisites

To start the collaborative development, ensure that you have set up the testing and production app versions by following this article.

{% hint style="info" %}
Every collaborating developer should have their testing app in Make, connected to the local app from the Git repository.
{% endhint %}

{% content-ref url="manage-testing-and-production-app-versions.md" %}
[manage-testing-and-production-app-versions.md](manage-testing-and-production-app-versions.md)
{% endcontent-ref %}

## Roles

* Owner of the production app - Every app in Make can be owned by a single Make account. The owner of the production app manages the deployment of the new local app version to the Make app.
* Developers of testing apps - Each developer manages their own testing app in Make, which is connected to the local app from the Git repository.

{% content-ref url="local-development-for-apps/create-a-new-app-origin.md" %}
[create-a-new-app-origin.md](local-development-for-apps/create-a-new-app-origin.md)
{% endcontent-ref %}

## Collaborative development flow

Below is a diagram explaining how developers can collaborate on app development.

<figure><img src="../../.gitbook/assets/FigJam basics (1).png" alt=""><figcaption><p>Development flow diagram</p></figcaption></figure>
