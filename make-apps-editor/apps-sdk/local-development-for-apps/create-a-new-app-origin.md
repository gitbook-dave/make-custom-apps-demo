# Create a new app origin

In the app development process, there are situations where it can be highly beneficial to push changes to multiple app origins. This is especially useful when managing different versions of an app, such as maintaining both a testing and a production app.

In this manual, the steps to create a new app origin for a testing app version are described.

1. If you haven't cloned the production app to a local workspace, do so by following the [manual](clone-make-app-to-local-workspace.md).
2. If you haven't created a testing app in Make, do so by creating a new app in Make and naming it `<App Label> Testing` so it is obvious it is the Testing version.
3. Go to the **makecomapp.json** file in the local app repository. Locate the `origins` array of the collection and enter a new item by copying the code below and editing the values as instructed under the code.

{% hint style="warning" %}
If the local app is shared among multiple developers, the `origins`array will contain records for each connection between their local and Make (remote) app. Do not edit the current records to prevent breaking the connections.
{% endhint %}

<figure><img src="../../../.gitbook/assets/Screenshot 2024-05-10 at 10.09.57.png" alt="" width="563"><figcaption><p>Creating a new origin for testing app</p></figcaption></figure>

```json
"origins": [
    { /* --- Existing origin --- */ },
    {
        "label": "Testing",
        "baseUrl": "https://eu1.make.com/api",
        "appId": "my-first-app-test",
        "appVersion": 1,
        "apikeyFile": "../.secrets/apikey"
    }
]
```

* `label` - the label of the local origin
* `baseUrl` - the URL to the origin's zone
* `appId` - the name of the app

4. Save the changes in the **makecomapp.json** file.
