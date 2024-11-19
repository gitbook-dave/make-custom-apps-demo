# Action modules

## Responsiveness approaches

Bear in mind that there are two approaches to responsiveness in a service.

* **Synchronous** - The service upon an action request returns a result, which can then be processed in the following modules in a scenario.
* **Asynchronous** - The service doesn't return anything at all, or doesn't return useful output, e. g. a processed file.

## Comparison of synchronous and asynchronous approaches

<table><thead><tr><th width="159">Attribute/ Approach</th><th>Synchronous</th><th>Asynchronous</th></tr></thead><tbody><tr><td><strong>Advantage</strong></td><td>The result is returned right away. Ability to proceed the result to the following modules.</td><td>Comes in handy when we need to process a large amount of data, e. g. file conversion.</td></tr><tr><td><strong>Disadvantage</strong></td><td>Regarding the type of job and its severity, the job can take too long. This might cause a timeout (default 40 sec). E. g. file conversion. The default timeout can be prolonged depending on the valid cases.</td><td>The scenario is not fluent. It is needed to create at least 2 scenarios - one for triggering the job, and another one for proceeding with the result from the first scenario. The second scenario, if possible, should start with an instant trigger that triggers once the job finishes.</td></tr><tr><td><strong>Module Example</strong></td><td><a href="https://eu1.make.com/apps/cloudconvert/2/modules/ConvertFile/communication">CloudConvert > Convert a File</a></td><td><a href="https://eu1.make.com/apps/cloudconvert/2/modules/CreateJob/communication">CloudConvert > Create a Job (advanced)</a></td></tr><tr><td><strong>Example Scenarios</strong></td><td><p><a href="https://www.make.com/en/templates/3064-convert-files-from-google-drive-in-cloudconvert-and-upload-the-output-to-google-drive">Convert files from Google Drive in CloudConvert</a> </p><p>The scenario contains <a href="https://eu1.make.com/apps/cloudconvert/2/modules/ConvertFile/communication">Convert a File</a> module, which has the synchronous logic implemented on app's side.</p></td><td><ol><li><a href="https://www.make.com/en/templates/3074-advanced-create-a-job-in-cloudconvert-archive-export-per-1-file">Create an archive job in CloudConvert</a></li><li><a href="https://www.make.com/en/templates/3062-advanced-create-a-new-job-for-export-url-tasks-download-files-from-export-url-tasks-in-cloudconvert">Download files from the job in CloudConvert</a> </li></ol><p>The first scenario contains <a href="https://eu1.make.com/apps/cloudconvert/2/modules/CreateJob/communication">Create a Job (advanced)</a> module which has asynchronous approach by default. The only result is the job's ID.</p></td></tr></tbody></table>

## Handling of asynchronous approach

When a web service doesn't support a synchronous approach and the common use case of the module requires support, it should be added on the app's side. Basically, there should be two (or more calls) executed instead of only one:

* **create a job call** - a call that requests for the job, e. g. conversion of a file, file upload,
* **periodically check the status of the job -** execute repeated calls to obtain the job's status**,**
* **ask for the result of the job -** once the status call returns the awaited status, request the result, e. g. result file.

### Example

After importing a JSON file to a web service, it requires a certain period of time to process the file. In this case, we have to keep checking if the status of the entity changed from `processing` to `completed`. In this case, when the status is `completed`, the result is already part of the response.

{% hint style="warning" %}
When the repeat directive is used, the **condition** and **limit** should always be provided to **prevent** **infinite** **loops**. Learn more about the [repeat](../app-blocks/api/making-requests.md#repeat) directive.
{% endhint %}

```javascript
[
	{
		"url": "/v3/activities/contacts_json_import",
		"method": "POST",
		"body": "{{encodeParameters(parameters)}}",
		"response": {
			"temp": "{{parseResponse(body)}}"
		}
	},
	{
		"url": "{{temp._links.self.href}}",
		"method": "GET",
		"repeat": {
			"condition": "{{body.state != 'completed'}}",
			"delay": 1000,
			"limit": 300
		},
		"response": {
			"temp": "{{body}}"
		}
	},
	{
		"response": {
			"valid": "{{length(temp.activity_errors) = 0}}",
			"error": {
				"message": "{{join(temp.activity_errors, '\n')}}"
			},
			"output": "{{parseResponse(temp)}}"
		}
	}
]
```
