# Manage testing and production app versions

{% hint style="info" %}
The development of testing and production app versions is available in the VS Code extension with the Local Development for Apps feature. To learn about the current `git` versioning support, check the dedicated section.
{% endhint %}

This page describes how to develop an application with the Make Apps Editor, managing production and test versions of the application.

* The developer writes and tests the code with the test application in Make.
* The developer tracks changes in the local `git` repository, pulling changes from the test application.
* &#x20;The developer pushes the changes to the production application from the local testing app when they finish the development and testing.

This process improves the maintenance and stability of the application because the development does not influence the production version of the application. In addition, all changes can be tracked in a `git` repository, providing a clear and organized development workflow.

## Prerequisites

To start the development of testing and production app versions, the following is needed:

* The production version of an app in Make - If you already have an app that is already in use, use it as the production app.&#x20;
* Cloned production version to the local workspace - Clone the app to the local workspace, if you haven't done so yet, by following this [manual](local-development-for-apps/clone-make-app-to-local-workspace.md).
* The testing version of an app in Make - Create a new app in Make, with no content, that will function as the testing version of the app.
* Optional, version control with Git - To properly track all changes in the local app, it is recommended to use a Git repository, for example, GitHub.

## Development flow

Below is a diagram explaining how a developer can develop testing and production app versions.

<figure><img src="../../.gitbook/assets/FigJam basics (4).png" alt="" width="188"><figcaption><p>App development flow diagram</p></figcaption></figure>

## Create a testing version of an app

First, you will need to create a testing version of Make app. Follow the instructions in the article below, to create a new origin to the Make testing app.

{% content-ref url="local-development-for-apps/create-a-new-app-origin.md" %}
[create-a-new-app-origin.md](local-development-for-apps/create-a-new-app-origin.md)
{% endcontent-ref %}

Once the origin for the testing app is successfully created, you will need to deploy the current code from the app, that already exists, which we can call "Production".

1. Right-click on the **makecomapp.json** file and select **Deploy to Make (beta)**.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-09 at 21.47.11.png" alt="" width="432"><figcaption><p>Deploy the app to Make</p></figcaption></figure>

2. In the dialog, select the app origin that represents the testing app.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-09 at 21.50.06.png" alt="" width="461"><figcaption><p>Selecting the Testing app origin</p></figcaption></figure>

3. The content of the local app will now be deployed to Make. Whenever a new component is about to be created, a dialog will prompt for confirmation. Press **Enter** to confirm the creation of the component. If you don't want to create the component, click **Ignore permanently/do not map with remote** option.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-09 at 21.51.55.png" alt="" width="462"><figcaption><p>Confirming creation of new RPC</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-09 at 21.52.16.png" alt="" width="463"><figcaption><p>Confirming creation of new module</p></figcaption></figure>

4. The app has been deployed to Make.&#x20;

## Develop the components in the testing app

Now, you can start developing new components or editing the current components in the Testing app in Make, and thoroughly test the app in Scenario Builder.

## Pull changes from the testing app to the local app

Once you finish the development of new changes and components in the testing app you can push the changes to the local app.

{% content-ref url="local-development-for-apps/pull-changes-from-make-app.md" %}
[pull-changes-from-make-app.md](local-development-for-apps/pull-changes-from-make-app.md)
{% endcontent-ref %}

## Deploy the changes from the local app to the production app

To synchronize changes made to the testing app with the production app, follow the steps outlined in the manual below.

{% content-ref url="local-development-for-apps/deploy-changes-from-local-app-to-make-app.md" %}
[deploy-changes-from-local-app-to-make-app.md](local-development-for-apps/deploy-changes-from-local-app-to-make-app.md)
{% endcontent-ref %}

