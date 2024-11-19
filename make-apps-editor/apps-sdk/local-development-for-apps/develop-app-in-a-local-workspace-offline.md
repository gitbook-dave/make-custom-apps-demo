# Develop app in a local workspace (offline)

Unlike online development within Make Apps Editor or web code editor, local development doesn't provide access to advanced features such as prefilled code templates, IML object suggestions, and seamless integration with Scenario Builder for continuous testing.&#x20;

Instead, it offers a self-contained environment for app creation and modification, ideal for situations where internet connectivity is unreliable or where comprehensive testing within Scenario Builder isn't required. Additionally, local development allows synchronization with Git repositories and provides full search capabilities across the entire codebase.

{% hint style="info" %}
If you prefer app development in the App Editor, follow this [manual](../manage-testing-and-production-app-versions.md), which describes online development, instead.
{% endhint %}

## Develop a new or edit a current component in a local app

1. If you don't have an app cloned yet, do so by following this manual:

{% content-ref url="clone-make-app-to-local-workspace.md" %}
[clone-make-app-to-local-workspace.md](clone-make-app-to-local-workspace.md)
{% endcontent-ref %}

2. The structure of the app is very similar to the one in Make Apps Editor. Each group of components, such as RPCs, modules, or custom IML functions, contains the component directories with corresponding code files.

{% tabs %}
{% tab title="Make App in Make Apps Editor" %}
<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 13.02.42.png" alt="" width="563"><figcaption><p>Make App Structure - Modules > module > Communication</p></figcaption></figure>
{% endtab %}

{% tab title="Local App in App' local development (beta)" %}
<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 12.59.05.png" alt="" width="563"><figcaption><p>Local App Structure - modules > module > communication</p></figcaption></figure>

{% hint style="info" %}
Each file within a local app component has a name in this format:

`component's-name.app's-block.iml.json`

for example:

`execute-rule.communication.iml.json` where `execute-rule` is the name of the module and `communication` is the name of the module's block.
{% endhint %}
{% endtab %}
{% endtabs %}

3. If you need to edit the current code, click the file you want to edit and develop your changes in the opened tab. Save the changes.
4. If you need to create a new component, right-click the corresponding components' folder and select **New Local Component: \<component's name> (beta)**, for example, New Local Component: Module (beta).&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 13.12.48.png" alt=""><figcaption><p>Creation of a new component</p></figcaption></figure>

5. Follow the dialog and enter the component's name, label, and other corresponding parameters as you are used to from Make Apps Editor.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 13.15.54.png" alt=""><figcaption><p>One of the dialog questions - Enter the Label of a new module</p></figcaption></figure>

6. Once all the questions are answered in the dialog, a new component with the corresponding files is created.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 13.25.30.png" alt="" width="431"><figcaption><p>New module Create a House with all corresponding files</p></figcaption></figure>

7. Write the code in the corresponding files and save the changes.

## Commit the changes in the Git repository

{% content-ref url="commit-the-changes-in-git-repository.md" %}
[commit-the-changes-in-git-repository.md](commit-the-changes-in-git-repository.md)
{% endcontent-ref %}

## Deploy the changes from the local app to the Make app

The changes in components or new components can be partially deployed to Make, or the app as a whole can be deployed to Make.

{% content-ref url="deploy-changes-from-local-app-to-make-app.md" %}
[deploy-changes-from-local-app-to-make-app.md](deploy-changes-from-local-app-to-make-app.md)
{% endcontent-ref %}
