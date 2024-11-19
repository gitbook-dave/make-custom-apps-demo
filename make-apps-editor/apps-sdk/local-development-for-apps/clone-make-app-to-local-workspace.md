# Clone Make app to local workspace

{% hint style="warning" %}
Please be advised that this feature is in beta, meaning, it may encounter occasional bugs or inconsistencies, so proceed with an awareness of potential functionality limitations.
{% endhint %}

To start the development of an app in a local directory or git repository, or start tracking changes in your app, you need to clone the Make app to the local workspace.

## Open the local folder

First, you need to open the folder where you intend to store the app, in Visual Studio Code.&#x20;

{% hint style="info" %}
Below, please, follow the section that corresponds to your development setup and choose:&#x20;

* 'Local Directory' if you are working directly on your computer's file system
* 'Git Repository' if you are using version control with Git

The 'Git Repository' section describes the development in the Git repository using the [GitHub Desktop](https://desktop.github.com/) app. Yet it's not obligatory,  any preferred [GUI tool](https://git-scm.com/downloads/guis) or CLI can be used.
{% endhint %}

<details>

<summary>Local directory</summary>

1. Open Visual Studio Code and navigate to **File > Open Folder**

<img src="../../../.gitbook/assets/Screenshot 2024-07-15 at 15.23.42.png" alt="" data-size="original">

2. In the file manager, choose the folder where the folder with the app should be cloned.
3. In the pop-up window, click "Yes, I trust the authors" option.

<img src="../../../.gitbook/assets/Screenshot 2024-07-15 at 15.28.06.png" alt="" data-size="original">

4. Now, the current local directory in Visual Studio is set.&#x20;

</details>

<details>

<summary>Git repository using GitHub Desktop app</summary>

1. Navigate to the GitHub Desktop app and open the repository where you intend to store the app.
2. Click **Open in Visual Studio Code** button**.**&#x20;

<img src="../../../.gitbook/assets/Screenshot 2024-07-16 at 10.05.59 (1).png" alt="" data-size="original">

3. In the pop-up window, click "Yes, I trust the authors" option.

<img src="../../../.gitbook/assets/Screenshot 2024-05-09 at 21.25.32.png" alt="Dialog window requesting the confirmation of trusting the authors of the code" data-size="original">

4. Now, the current repository in Visual Studio is set.&#x20;

</details>

## Clone the app to the local folder

Once the repository in Visual Studio is set, you can proceed to cloning the app to the local folder.

1. In the opened window of Visual Studio Code, go to Make Apps Editor and right-click the app you wish to save to your repository. Select **Clone to Local Folder (beta)**.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-09 at 7.20.45.png" alt="" width="260"><figcaption><p>Clone to Local Folder (beta) feature</p></figcaption></figure>

2. Read the text in the dialog window and confirm reading by clicking **Continue**.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-09 at 7.22.01.png" alt="" width="404"><figcaption><p>Dialog window requesting the confirmation of recommendations</p></figcaption></figure>

3. Enter the workspace subdirectory name, where the app should be cloned to. If the subdirectory doesn't exist yet, it will be created. The default subdirectory is set to `src`. Click **Enter**.

{% hint style="info" %}
If you are going to store more than one app in the repository, you can create a subfolder by using the `src/app-name` path, where the `app-name` is the name of the app folder.
{% endhint %}

<figure><img src="../../../.gitbook/assets/Screenshot 2024-07-16 at 10.10.10.png" alt=""><figcaption><p>Setting the workspace subdirectory where the app should be cloned to</p></figcaption></figure>

4. A dialog window asking whether[ common data](https://docs.make.com/apps/app-structure/connections#common-data) should be included or not will pop up.&#x20;

* **Exclude (more secure)** - Select, if your app contains sensitive data, such as Client ID and Secret. Common data will not be stored in your local workspace or a repository.
* **Include (for advanced users only) -** Select, if you want to store the common data in your local workspace or a repository. Be aware that storing common data outside of Make could potentially expose the app to vulnerabilities.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-24 at 12.03.06.png" alt="" width="282"><figcaption><p>Include/Exclude common data dialog</p></figcaption></figure>

5. The app is now cloned to the local folder.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-07-16 at 10.14.19.png" alt="" width="367"><figcaption><p>Local folder with the cloned apps</p></figcaption></figure>

## Start versioning the local app

{% hint style="info" %}
Versioning is only available if you are using version control with Git.

This manual describes the development in the Git repository using the [GitHub Desktop](https://desktop.github.com/) app. Yet it's not obligatory,  any preferred [GUI tool](https://git-scm.com/downloads/guis) can be used.
{% endhint %}

{% hint style="info" %}
The `.secrets` file with your Make API keys is only stored in the local folder. By default, the file is excluded from the git versioning.
{% endhint %}

To properly start the versioning of your app in the git repository, follow the steps below:

1. Go to the GitHub Desktop app and open the repository where you deployed the current version of your app. You will see a list of new files.
2. Enter the Summary of the commit and click **Commit to main**.
3. Now, the first version of your app is logged. Every new change or a new component in the app will be considered a new change.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-07-16 at 10.18.34.png" alt="" width="563"><figcaption><p>Created new change log record</p></figcaption></figure>

4. Optionally, click **Publish branch**.
