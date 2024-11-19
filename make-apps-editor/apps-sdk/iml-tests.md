# Write IML tests

{% hint style="warning" %}
When using IML functions, that work with date and time, remember to set the correct **timezone** in extension settings. The accepted format is the [international timezone format](https://en.wikipedia.org/wiki/List\_of\_tz\_database\_time\_zones).

_For example "Europe/Prague"_
{% endhint %}

### Write a test

It's possible to write tests for your custom IML functions. You can use `it` function and `asserts` as you may already know them from Mocha and other testing frameworks.\
Our example function has the following code:

{% tabs %}
{% tab title="Code" %}
```javascript
function exampleFunction(number) {
       return number * 2
       }
```
{% endtab %}

{% tab title="Occurence in VS Code" %}
<figure><img src="../../.gitbook/assets/imgVSCode.avif" alt=""><figcaption><p>Example function</p></figcaption></figure>
{% endtab %}
{% endtabs %}

So, let's write a test for this function. We'll create two blocks.

{% tabs %}
{% tab title="Code" %}
```javascript
it('First test', () => {
    assert.ok(exampleFunction(2) === 4)
    })
it('Second test', () => {
    assert.ok(exampleFunction(2) === 5)
    })
```
{% endtab %}

{% tab title="Occurence in VS Code" %}
![Example test with 2 blocks](../../.gitbook/assets/tests\_test.png)
{% endtab %}
{% endtabs %}

As you can see, the `it` function accepts exactly two parameters, the name of the test and the code to run. In this code, we can verify expected outputs using `assert.ok()` function.

### Run a test

To run a test on a specific function, right-click the function name in the tree and select the **Run IML  test** option.

![Run IML test option](<../../.gitbook/assets/Screen Shot 2022-08-22 at 14.18.24.png>)

The test will start and you'll see the output in the **IML tests** output channel.

![Output from the IML test](../../.gitbook/assets/tests\_result.png)

{% hint style="info" %}
If you need to debug your custom IML function, follow the article below.
{% endhint %}

{% content-ref url="../../debugging-your-app/debugging-of-custom-iml-functions/debug-iml-in-vs-code.md" %}
[debug-iml-in-vs-code.md](../../debugging-your-app/debugging-of-custom-iml-functions/debug-iml-in-vs-code.md)
{% endcontent-ref %}
