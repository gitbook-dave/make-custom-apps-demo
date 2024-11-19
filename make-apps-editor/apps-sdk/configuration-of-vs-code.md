# Configure VS Code

1. Install the Make Apps Editor. You can get the Make Apps Editor from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=Integromat.apps-sdk) or install it in the **Extensions** tab in VS code.
2. Click the Make icon on the VS code sidebar. Clicking on the Make icon activates the Make Apps Editor. You get notified in a pop-up window that you haven't yet set up a development environment.

![Pop-up about missing environments](../../.gitbook/assets/firstLaunch\_envAdd\_01.png)

3. Click the **Add environment** button to launch the environment setup or execute the command: `>Make Apps: Add SDK Environment` from the command palette.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-02 at 13.36.23.png" alt=""><figcaption><p>Command palette</p></figcaption></figure>

4. Fill in the API URL in the next pop-up window. The API URL depends on your Make zone. For example, the US1 Make zone has the API URL: `us1.make.com/api`.

{% hint style="warning" %}
If the app, you want to access, originates from a different zone than your account, enter the app's zone to access its content.
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-02 at 13.41.25.png" alt=""><figcaption><p>Filling account's /app's zone</p></figcaption></figure>

5. Fill in the label for the environment in the next pop-up window. Press Enter to confirm the environment label.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-02 at 13.42.45.png" alt=""><figcaption><p>Entering environment name</p></figcaption></figure>

6. Copy your Make API key in the last pop-up window. If you don't have an API key, follow the procedure to [create a Make API key](generation-of-your-api-key.md).

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-02 at 13.43.38.png" alt=""><figcaption><p>Entering Make API key</p></figcaption></figure>

The Make Apps Editor extension restarts with the environment configuration.

A new sidebar appears in VS code with a list of your custom apps and Make open-source apps. If you previously created any, your custom apps are listed in the block My apps. The Make open-source apps are listed in the **Open source apps** field at the bottom of the VS code sidebar.

{% hint style="warning" %}
The open-source apps' code is only available in the EU1 zone.

If your zone is different and you want to access their code, create a new environment with `eu1.make.com/api` environment URL by following the steps starting from the 5th.
{% endhint %}

### Switching among environments

In Make Apps Editor, you can work across multiple environments.

Easily identify the active environment by checking the indicator in the bottom status bar.

Upon clicking the environment indicator, you can switch among multiple environments.

<figure><img src="../../.gitbook/assets/image (62).png" alt="" width="540"><figcaption><p>Environment indicator</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-08 at 17.19.51.png" alt=""><figcaption><p>Switching among multiple environments</p></figcaption></figure>

You can add another environment by issuing the `>Add SDK environment` again (follow the steps starting from the 5th).

### Useful settings

You can add extra settings in **Extensions > Make Apps Editor > Extension Settings > settings.json** file.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-03 at 10.10.33.png" alt="" width="563"><figcaption><p>Extension Settings in Make Apps Editor app</p></figcaption></figure>

Here are some settings for better performance and experience:

* Set `editor.formatOnSave` to `true` in VS Code settings. Source codes will be formatted automatically when you save them.
* Set `editor.quickSuggetions.strings` to `true` in VS Code settings. Keyword recommendations will automatically show up while you're typing in IML strings too.

### Log out and log in to an environment

You can log out using the `>Logout` command and log back in by the `>Login` command.&#x20;

When you log out, the API key is removed from the `settings.json` file. To log in again, you will need to enter your API key.

{% hint style="info" %}
You can use this flow to change your API key in an environment.
{% endhint %}
