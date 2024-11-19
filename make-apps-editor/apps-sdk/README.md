# Develop apps in VS Code

{% hint style="info" %}
**You can get the Make Apps Editor extension from the** [**VS Code Marketplace**](https://marketplace.visualstudio.com/items?itemName=Integromat.apps-sdk).
{% endhint %}

Make supports writing custom apps in Visual Studio Code (VS Code) with the Make Apps Editor extension. You can get the VS Code extension from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=Integromat.apps-sdk) or install it in the **Extensions** tab in VS Code.

You write and edit the custom app configuration with the VS Code extension as you would edit a JSON file on your PC. The custom app configuration is downloaded to your PC when you open it from VS Code and uploaded to Make when you save it. The custom app configuration is stored on your PC as temporary files. The temporary files are deleted after you close the configuration.

The custom app configuration is associated with your account in Make. The communication with the VS Code extension and your Make account is authorized with an API key. To set up the VS Code extension you must provide an API key with the appropriate API key scopes. Generate a new Make API key if you don't have one:

{% content-ref url="generation-of-your-api-key.md" %}
[generation-of-your-api-key.md](generation-of-your-api-key.md)
{% endcontent-ref %}

{% hint style="info" %}
If you encounter any bug in the Make Apps Editor, feel free to contact our support.
{% endhint %}
