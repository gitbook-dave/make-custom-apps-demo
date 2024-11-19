# Groups

If the app has over 10 modules, the modules should be put into special groups. These groups should be named after the entity with which the modules work, or after the type of the job, the modules are executing.

<div>

<figure><img src="../.gitbook/assets/Screen Shot 2022-08-26 at 18.13.30.png" alt=""><figcaption><p>Example of groups - App CloudConvert</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/Screen Shot 2022-08-26 at 18.14.52.png" alt=""><figcaption><p>Example of groups - App SugarCRM</p></figcaption></figure>

</div>

Also, the modules inside these groups should follow this order:

1. Trigger module
2. Create module
3. Update module
4. Get module
5. Download/Upload Module
6. List/Search module
7. Delete module

The universal module should be left inside "Other" group.

More about groups can be found [here](../app-structure/groups.md).
