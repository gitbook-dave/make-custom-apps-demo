# Pull changes from Make app

Once you finish the development of new changes and components in the Make app you can push the changes to the local app. To do so, follow the steps below.

1. Go to Visual Studio Code and open the local directory with the local app file.&#x20;

If you are uncertain how to do so, simply follow the steps in the corresponding section in the [article](clone-make-app-to-local-workspace.md).

2. Locate the **makecomapp.json** file and right-click it. In the pop-up menu select **Pull All Components from Make (beta)** option.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 10.52.48.png" alt="" width="449"><figcaption></figcaption></figure>

3. In the dialog, select the testing app origin.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 11.00.31.png" alt="" width="466"><figcaption></figcaption></figure>

4. All changes in the existing components will be pulled into the local components. If there is a new component, a dialog will appear. Either confirm the creation of the component by pressing **Enter** or click **Ignore permanently/do not map with the remote** option.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 11.02.50.png" alt="" width="462"><figcaption></figcaption></figure>

5. To properly track the new version of your local app in a local workspace or git repository, follow the corresponding steps in this [article](commit-the-changes-in-git-repository.md).
