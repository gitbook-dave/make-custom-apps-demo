# Develop apps in Make UI

When you create your app in the Make platform, you are using the web code editor. The web code editor has a bunch of handy features to make your app development easier:

1. Hints with links to the apps platform documentation with more details.
2. Code reformat button with a label showing the data format. The available editor box data formats are:
   * `jsonc`
   * `json`
   * `javascript`
   * `markdown`
3. Context aware code suggestions for the `jsonc` data format. The web code editor gives you hints what parameters or properties you can add to the custom app code. The code suggestions work even for RPCs.
4. Hints displayed when hovering over the custom app configuration.
5. Custom app code validation for the `jsonc` data format. If you misspell a code property name, or if you place a property in an invalid code section, the web code editor highlights the error.
6. One button to save changes in all editor boxes on the page.

<figure><img src="../.gitbook/assets/web-editor-final.png" alt=""><figcaption><p>Make apps platform web code editor with callouts.</p></figcaption></figure>

7. Hovering over [built-in IML functions](https://docs.integromat.com/apps/app-components/iml#built-in-iml-functions) shows their docs.

<figure><img src="../.gitbook/assets/Screenshot 2024-05-24 at 10.53.46.png" alt="" width="434"><figcaption><p>Hovering over built-in IML function</p></figcaption></figure>

8. Hovering over [custom IML functions](https://docs.integromat.com/apps/app-structure/iml-functions) provides a link to the function definition.

<figure><img src="../.gitbook/assets/Screenshot 2024-05-24 at 10.56.14.png" alt="" width="563"><figcaption><p>Hovering over custom IML function</p></figcaption></figure>

9. Controls to expand and collapse the code. To view the controls, hover over the space between your code and editor line numbers.

<figure><img src="../.gitbook/assets/Screenshot 2024-05-24 at 10.58.17.png" alt="" width="563"><figcaption><p>Colapsing the code</p></figcaption></figure>

10. The editor highlights the IML syntax so it's distinct from the rest of the code.

## Web code editor keybindings

The web code editor is built on the same backend as the Visual Studio Code. If you know your way around Visual Studio Code, you will find that some keybindings also work in the web code editor. Some of the most useful web code editor keybindings are:

For **Windows** users:

* **Ctrl + Shift + H**: shows a cheat sheet with selected shortcuts
* **Ctrl + S**: save your changes to all of the editor boxes on the page
* **Ctrl + F**: search in the editor box content
* **Ctrl + H**: search and replace in the editor box content
* **Ctrl + Space**: show a list of code suggestions valid in the current cursor context
* **Shift + Alt + F**: format code
* **Ctrl + /**: toggle line comments
* **F1**: display web code editor command and keybindings reference

For **MacOS** users:

* **Ctrl + Shift + H**: shows a cheat sheet with selected shortcuts
* **Cmd + S**: save your changes to all of the editor boxes on the page
* **Cmd + F**: search in the editor box content
* **Opt + Cmd + F**: search and replace in the editor box content
* **Ctrl + Space**: show a list of code suggestions valid in the current cursor context
* **Shift + Opt + F**: format code
* **F1**: display web code editor command and keybindings reference

For a full reference of the web code editor keybindings check the official [VSCode documentation](https://code.visualstudio.com/docs/getstarted/keybindings#\_keyboard-shortcuts-reference) and the official VSCode keybindings cards:

* [MacOS](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
* [Windows](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)

{% hint style="info" %}
Note that your browser might intercept some keybindings in the official reference or might not make sense in the context of a web code editor. For example, the keybinding Ctrl + N creates a new file in VSCode, but in Google Chrome the keybinding creates a new browser window instead.
{% endhint %}
