# Use general controls

### Edit the source code

To start editing the source code, find the item you want to edit in the left menu and click it. A new editor will appear and the current source will be downloaded from Make.\
You can edit it as a normal file. If your app contains some RPCs or IML functions, they will be provided to you.

![Adding a new funtion from list of available functions](../../.gitbook/assets/ctrl\_src\_01.png)

After pressing the shortcut `CTRL+S`, the source code will be automatically uploaded back to Make.

### Add a new item

To add a new item, such as a module, connection, webhook, etc., right-click the corresponding folder and click the **New \<item>** option.

![Adding a new module](<../../.gitbook/assets/Screen Shot 2022-08-22 at 13.51.12.png>)

Each time the prompt will appear, you will be asked to fill in information about the newly created item. Just go through it. Your new items will always appear under the corresponding folder.

![A new module](<../../.gitbook/assets/Screen Shot 2022-08-22 at 13.54.01.png>)

### Edit metadata

To edit metadata (for example to change a label of a module), right-click the desired item and select the **Edit metadata** option from the menu.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-09 at 6.10.18.png" alt=""><figcaption><p>Editing metadata of a module</p></figcaption></figure>

The prompt will appear allowing you to change allowed values. If you don't want to change a value, skip the field by pressing the Enter key.

### Change the connection or webhook

To change the attached connection or webhook of an item, right-click the item and select the **Change connection (or webhook)** option from the menu.

![Change connection or webhook option](<../../.gitbook/assets/Screen Shot 2022-08-22 at 13.56.39.png>)

The prompt will appear allowing you to change the connection or webhook. If possible, there will also be an option to unassign the current connection without assigning a new one.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-09 at 6.16.57.png" alt=""><figcaption><p>Changing a primary connection</p></figcaption></figure>

Also, the prompt to assign an alternative (secondary) connection will appear. Please note, that the alternative connection should not be the same as the main connection. You can leave it empty.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-09 at 6.18.28.png" alt=""><figcaption><p>Changing a secondary connection</p></figcaption></figure>

### Delete an item

To delete an item, right-click it and choose the `Delete` option.

![Delete option](<../../.gitbook/assets/Screen Shot 2022-08-22 at 14.08.27.png>)

You will be asked to confirm the deletion. If you answer `Yes`, the item will be deleted from the app.

![Deletion dialog](<../../.gitbook/assets/Screen Shot 2022-08-22 at 14.14.26.png>)

{% hint style="warning" %}
Deleting items is only possible in private apps. Once an app is published, the capability to delete items within the app is disabled. For further details regarding apps' visibility and the deletion of items, please refer to [this article](../../app-visibility.md).
{% endhint %}

### Generate the interface code

Utilize the Interface Generator to generate an interface. Familiarize yourself with the Generator's functionality by following the steps described in the Interface Generator article below.

{% content-ref url="../../app-blocks/interface.md" %}
[interface.md](../../app-blocks/interface.md)
{% endcontent-ref %}
