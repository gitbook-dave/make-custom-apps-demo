# Create an app in VS Code

1. When you have successfully logged in and have the environment set, it's time to develop your first app. To start, click the `+` icon in the header of `My apps` section or call the `>New app` command directly from the command palette.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-02 at 14.15.07.png" alt="" width="461"><figcaption><p>Section My Apps</p></figcaption></figure>

2. First, you will be asked to fill in a label. That's the app's name the users will see in the Scenario builder.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-02 at 14.25.45.png" alt="" width="563"><figcaption><p>Entering new app's label</p></figcaption></figure>

3. Next, the app ID will be generated for you. It will be used in URL paths. However, it should be clear to which app it leads. It has to match `(^[a-z][0-9a-z-]+[0-9a-z]$)` regular expression.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-02 at 14.27.21.png" alt="" width="563"><figcaption><p>Entering new app's name</p></figcaption></figure>

4. Then, you'll be asked to enter the app's version. Currently, the version 1 is only supported.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-02 at 14.30.30.png" alt="" width="563"><figcaption><p>Entering new app's version</p></figcaption></figure>

5. Next, you'll be prompted to enter the description of your app.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-02 at 14.30.42.png" alt="" width="563"><figcaption><p>Entering new app's description</p></figcaption></figure>

6. Then, enter a color theme for your app. This is the color the app's modules will be seen as in scenarios. The theme is in hexadecimal format. For example, the Make app's color is `#6e21cc`.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-02 at 14.30.51.png" alt="" width="563"><figcaption><p>Entering new app's theme</p></figcaption></figure>

7. The next prompt will ask for the app language. That is the language of the interface of the app. Most of the apps in Make are currently in English.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-02 at 14.42.42.png" alt="" width="563"><figcaption><p>Selecting new app's language</p></figcaption></figure>

8. The last prompt is for countries where the app will be available. If you don't pick any country, the app will be considered global.

{% hint style="info" %}
Currently, this selection does not affect the availability of the app.
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-02 at 14.31.09.png" alt="" width="563"><figcaption><p>Selecting countries.</p></figcaption></figure>

And that is it. After you confirm the last dialog, your brand-new app will appear in the `My Apps` view and you can start coding.

![New custom app in Make](../../.gitbook/assets/firstApp\_07.png)
