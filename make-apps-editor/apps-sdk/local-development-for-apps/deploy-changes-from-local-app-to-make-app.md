# Deploy changes from local app to Make app

The changes in components or new components can be partially deployed to Make, or the app as a whole can be deployed to Make.

1. Follow the instruction, that fits your case, below.

{% tabs %}
{% tab title="Deploy a code file" %}
To deploy only a specific code file in a component to Make, right-click the code file and select **Deploy to Make (beta)**.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 14.29.43.png" alt=""><figcaption><p>Deploying a communication file of create-house module</p></figcaption></figure>
{% endtab %}

{% tab title="Deploy a component directory" %}
To deploy a component to Make, right-click the component directory and select **Deploy to Make (beta)**.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 14.33.39.png" alt=""><figcaption><p>Deploying a component directory of create-house module</p></figcaption></figure>
{% endtab %}

{% tab title="Deploy an app" %}
To deploy the whole app to Make, right-click the **makecomapp.json** file and select **Deploy to Make (beta)**.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 14.35.49.png" alt=""><figcaption><p>Deploying app to Make</p></figcaption></figure>
{% endtab %}
{% endtabs %}

2. In the dialog, select the origin where the changes should be deployed.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 15.23.39.png" alt=""><figcaption><p>Selecting the app origin for deploying changes</p></figcaption></figure>

3. The changes or new components are now available in the Make app. The new app version can be thoroughly tested in Scenario Builder. If you utilize testing and production apps, you can deploy the changes or new components to the production, after the testing app passes the testing phase.
