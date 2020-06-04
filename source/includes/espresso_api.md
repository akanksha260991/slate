# Espresso API

BrowserStack provides support for the Espresso testing framework for Android. You can run your Espresso tests written in both Java and Kotlin. 

In order to get started with Espresso you need to make use of our Espresso API to perform the following steps:
<br>
<br>
1. Upload your app <br>
2. Upload your test-suite <br>
3. Execute your build <br>

Once the build execution is completed, the Espresso build and sessions APIs can be used to view the execution details.

<aside class="notice">Note: Each device execution in Espresso is treated as a session.
</aside> 


<!------------APPS APIS----------------->

## Apps

<p>In order to test your native and hybrid apps on BrowserStack, you need to upload your Android apps and Espresso test-suite to BrowserStack using our REST API. There are two ways to upload an app:</p>

### Upload an app

> Example Request

```shell
curl -u "USERNAME:ACESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/espresso/v2/upload"
```

> Example Response

```json
{
   "app_url":"bs://c8ddcb5649a8280ca800075bfd8f151115bba6b3",
   "custom_id":"SampleApp",
   "shareable_id":"akanksha48/SampleApp"
}
```

Upload your Espresso app on BrowserStack. There are two ways to upload the apps:

1. Upload an app from local machine
2. Upload an app using a public URL


**REQUEST**

<span style="color:darkred">**POST**</span> &nbsp;&nbsp;&nbsp; `app-automate/espresso/v2/upload`

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  file <br><sub><sup>required</sup></sub> | string | The path to the app file in your local system. <br> <b>Example</b> `/Users/Desktop/Appium/app-debug.apk` |
|  custom_id <br><sub><sup>optional</sup></sub> | string | Constant name for the uploaded app. You can upload multiple apps using the same custom id. <br> <b>Example</b>  `SampleApp` |

<br>

**RESPONSE**

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  app_url     | string | App url of the app uploaded on BrowserStack. <br> <b>Example</b> `bs://5649a8280ca800075bfd8f151115bba6b3` |
|  custom_id     | string | Unique name identifier for your app. <br> <b>Example</b> `SampleApp` |
|  shareable_id  | string | ID which can be used by other users of your team. <br> <b>Example</b>  `steve/SampleApp` |


<br>
<br>


### Get app details

> Example Request

```shell
curl -u "USERNAME:ACESS_KEY" \
-X GET "https://api-cloud.browserstack.com/app-automate/espresso/v2/apps/c8ddcb5649a8280ca800075bfd8f151115bba6b3" 
```

> Example Response

```json
{
    "app_name": "app-debug.apk",
    "app_version": "1.2.0",
    "app_url": "bs://c8ddcb5649a8280ca800075bfd8f151115bba6b3",
    "app_id": "c8ddcb5649a8280ca800075bfd8f151115bba6b3",
    "uploaded_at": "2020-05-05 14:52:54 UTC",
    "custom_id": "SampleApp",
    "shareable_id": "steve/SampleApp"
}
```

View the details about any app uploaded on BrowserStack. You need to pass the `app_id` to fetch the details of any app.


**REQUEST**

<span style="color:darkred">**POST**</span> &nbsp;&nbsp;&nbsp; `app-automate/espresso/v2/apps/<app_id>`

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  app_id <br><sub><sup>required</sup></sub> | string | Unique ID of the test-suite uploaded on BrowserStack. <br> <b>Example</b> `c8ddcb5649a8280ca800075bfd8f151115bba6b3` |

<br>

**RESPONSE**


| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  app_name     | string | Name of the .apk file. <br> <b>Example</b> `app-debug.apk` |
|  app_version     | string | The version of your app. <br> <b>Example</b> `1.2.0` |
|  app_url  | string | App url of the app uploaded on BrowserStack. <br> <b>Example</b>  `bs://c8ddcb5649a8280ca800075bfd8f151115bba6b3` |
|  app_id     | string | Unique ID of the app uploaded on BrowserStack. <br> <b>Example</b> `c8ddcb5649a8280ca800075bfd8f151115bba6b3` |
|  uploaded_at     | string | Timestamp value at which the app was uploaded on BrowserStack servers.. <br> <b>Example</b> `2020-05-05 14:52:54 UTC` |
|  custom_id     | string | Constant name for the app. <br> <b>Example</b> `SampleApp` |
|  shareable_id  | string | ID which can be used by other users of your team to access the app. <br> <b>Example</b>  `steve/SampleApp` |


<br>
<br>

### List recent apps

> Example Request

```shell
curl -u "USERNAME:ACESS_KEY" \
-X GET "https://api-cloud.browserstack.com/app-automate/espresso/v2/apps"
```

> Example Response

```json
[
  {
    "app_name": "Calculator.ipa",
    "app_version": "1.0",
    "app_url": "bs://8f724079dc940b3e1c4a6a4e3008f724079dcefa5",
    "app_id": "8f724079dc940b3e1c4a6a4e3008f724079dcefa5",
    "uploaded_at": "2020-05-21 13:45:31 UTC"
  },
  {
     "app_name": "app-debug.apk",
    "app_version": "1.2.0",
    "app_url": "bs://c8ddcb5649a8280ca800075bfd8f151115bba6b3",
    "app_id": "c8ddcb5649a8280ca800075bfd8f151115bba6b3",
    "uploaded_at": "2020-05-05 14:52:54 UTC",
    "custom_id": "SampleApp",
    "shareable_id": "steve/SampleApp"
  }
]
```

 Fetch a list of your recently uploaded apps and its details such as app_url, custom ID, shareable ID and upload timestamp for each app.

<br>

**REQUEST**

<span style="color:darkgreen">**GET**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/espresso/v2/apps`

<br>

**RESPONSE**

The response is an array of the app details object.

<br>
<br>
<br>

### Delete an app

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X DELETE "https://api-cloud.browserstack.com/app-automate/espresso/v2/apps/<app_id>"
```

> Example Response

```json
{
    "success": {
        "message": "App was deleted."
    }
} 
```


We automatically delete your uploaded apps after 30 days from the day of upload. You can also use our REST API to explicitly delete an app before this 30 day time period. The app can be deleted using the app_id.

<br>

**REQUEST**

<span style="color:darkred">**DELETE**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/espresso/v2/apps/<app_id>`

**Path Parameter** <br>

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  app_id     | string | App ID of the app uploaded on BrowserStack. <br> <b>Example</b> `f7c874f21852ba57957a3fdc33f47514288c4ba4` |

<br>

**RESPONSE**

There will a **success** or **error** object depending on the success/failure of the delete test-suite request.

<br>
<br>




<!------------TEST-SUITE APIS----------------->

## Test suites
In order to test your android apps using Espresso framework, you need to upload your Android app and the Espresso test-suite on BrowserStack. Using the Espresso Test-Suite API endpoints, you can perform the following:

1. View the recent test-suite uploads <br>
2. View the test-suite info <br>
3. Delete any test-suite <br>


### Upload a test-suite

> Example Request

```shell
# Upload test-suite from local machine
curl -u "USERNAME:ACCESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/espresso/v2/test-suite" \
-F "file=@/path/to/test/file/app-debug-androidTest.apk" \
-F 'data={"custom_id": "SampleTest"}'


# Upload test-suite using a public URL
curl -u "USERNAME:ACESS_KEY"  \
-X POST "https://api-cloud.browserstack.com/app-automate/espresso/v2/test-suite" \
-F 'data={"url": "https://www.browserstack.com/app-automate/sample-apps/android/CalculatorTest.apk"}'

```

> Example Response

```json
{
    "test_url":"bs://f7c874f21852ba57957a3fdc33f47514288c4ba4",
    "custom_id":"SampleTest",
    "shareable_id":"steve/SampleTest"
}
```

Upload your Espresso test-suite on BrowserStack. There are two ways to upload the test-suite:
<br>
<br>
1. Upload a test-suite from local machine <br>
2. Upload a test-suite using a public URL <br>

<br>

**REQUEST**

<span style="color:darkred">**POST**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/espresso/v2/test-suite`
<br>

**Request Parameters** <br>
Upload a test-suite from local machine

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  file <br><sub><sup>required</sup></sub> | string | Path to your test-suite. <br> <b>Example</b> `/Users/Desktop/Appium/app-debug-androidTest.apk` |
|  custom_id <br><sub><sup>optional</sup></sub> | string | Specify a constant name for the test-suite. You can upload multiple test-suites using the same custom ID. <br> <b>Example</b>  `SampleTest` |

<br>
Upload a test-suite using a public URL

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  url <br><sub><sup>required</sup></sub> | string | Remote public URL to the test-suite file. <br> <b>Example</b> `https://www.browserstack.com/app-automate/sample-apps/android/CalculatorTest.apk` |
|  custom_id <br><sub><sup>optional</sup></sub> | string | Specify a constant name for the test-suite. You can use the same custom ID for multiple versions of a test-suite you upload. <br> <b>Example</b>  `SampleTest` |

<br>

**RESPONSE**

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  test_url     | string | Test url of the test uploaded on BrowserStack. <br> <b>Example</b> `bs://f7c874f21852ba57957a3fdc33f47514288c4ba4` |
|  custom_id     | string | Constant name for the test-suite. You can use the same custom ID for multiple versions of a test-suite you upload. <br> <b>Example</b> `SampleTest` |
|  shareable_id  | string | ID which can be used by other users of your team for accessing the test-suite. <br> <b>Example</b>  `steve/MyTest` |

<br>
<br>
<br>

### Get test-suite details

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/espresso/v2/test-suite/<test_suite_id>" 
```

> Example Response

```json
{
    "test_suite_name": "app-debug-androidTest.apk",
    "test_suite_url": "bs://f7c874f21852ba57957a3fdc33f47514288c4ba4",
    "test_suite_id": "f7c874f21852ba57957a3fdc33f47514288c4ba4",
    "uploaded_at": 1591254892,
    "custom_id": null,
    "framework": "espresso"
}
```

View the details about any test-suite uploaded on BrowserStack. You need to pass the `test_suite_id` to fetch the details of any test-suite file.

<br>

**REQUEST**

<span style="color:darkred">**POST**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/espresso/v2/test-suite/<test_suite_id>`
<br>

**Path Parameter** <br>

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  test_suite_id <br><sub><sup>required</sup></sub> | string | Unique ID of the test-suite uploaded on BrowserStack. <br> <b>Example</b> `f7c874f21852ba57957a3fdc33f47514288c4ba4` |

<br>

**RESPONSE**

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  test_suite_name     | string | Name of the test-suite file. <br> <b>Example</b> `app-debug-androidTest.apk` |
|  test_suite_url     | string |  Test url obtained after successful upload of test-suite on BrowserStack. <br> <b>Example</b> `bs://f7c874f21852ba57957a3fdc33f47514288c4ba4` |
|  test_suite_id  | string | Unique ID of the test-suite uploaded on BrowserStack. <br> <b>Example</b>  `f7c874f21852ba57957a3fdc33f47514288c4ba4` |
|  uploaded_at     | timestamp | Timestamp value at which the app was uploaded on BrowserStack servers. <br> <b>Example</b> `1591254892`|
|  custom_id     | string | Constant name for the test-suite. <br> <b>Example</b> `SampleTest` |
|  framework     | string | Name of the framework. <br> <b>Value</b> `espresso` |

<br>
<br>
<br>



### List recent test-suites

> Example Request

```shell
curl -u "USERNAME:ACESS_KEY" \
-X GET "https://api-cloud.browserstack.com/app-automate/espresso/v2/test-suites"
```

> Example Response

```json
[
  {
    "test_suite_name": "app-debug-androidTest.apk",
    "test_suite_url": "bs://f7c874f21852ba57957a3fdc33f47514288c4ba4",
    "test_suite_id": "f7c874f21852ba57957a3fdc33f47514288c4ba4",
    "uploaded_at": 1590083493,
    "custom_id": "SampleTest",
    "framework": "espresso"
  },
  {
    "test_suite_name": "app-debugTest.apk",
    "test_suite_url": "bs://d819081c97b4a61f6250b441cbe3efaea4c99210",
    "test_suite_id": "d819081c97b4a61f6250b441cbe3efaea4c99210",
    "uploaded_at": 1589900729,
    "custom_id": "ShardTest",
    "framework": "espresso"
  }
]
```


 Fetch a list of your recently uploaded test-suites and its details such as test_url, custom ID, shareable ID and upload timestamp for each test-suite.

<br>

**REQUEST**

<span style="color:darkgreen">**GET**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/espresso/v2/test-suites`

<br>

**RESPONSE**

The response is an array of the test-suite details object.


<br>
<br>
<br>


### Delete a test-suite

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X DELETE "https://api-cloud.browserstack.com/app-automate/espresso/v2/test-suites/<test_suite_id>"
```

> Example Response

```json
{
    "success": {
        "message": "Test-suite was deleted."
    }
} 
```


We automatically delete your uploaded test-suites after 30 days from the day of upload. You can also use our REST API to explicitly delete a test-suite before this 30 day time period. The test-suite can be deleted using the test-suite's `test_url`.

<br>

**REQUEST**

<span style="color:darkred">**DELETE**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/espresso/v2/test-suites/<test_suite_url>`

**Path Parameter** <br>

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  test_suite_id     | string | Test suite ID of the test-suite uploaded on BrowserStack. <br> <b>Example</b> `f7c874f21852ba57957a3fdc33f47514288c4ba4` |

<br>

**RESPONSE**

There will a **success** or **error** object depending on the success/failure of the delete test-suite request.

<br>
<br>





<!------------BUILD APIS----------------->

## Builds
<p>An Espresso build represents your test-suite execution on Browserstack. Once you upload your Android app and Espresso test-suite, you can use the Build REST API endpoints, to perform the following actions:</p>
<p>
1. Execute the build <br>
2. Get details about your build executions <br>
3. Delete an Espresso build 
</p>

### Execute a build

> Example Request

```shell
# Execute build
curl -u "USERNAME:ACCESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/espresso/v2/build" \
-d {"app": "bs://3b79f7f0390dbe5f3550b544514bddcaa8197abe", "testSuite": "bs://832ge0b1c3d8bacef95ad71c09c65ad2a0008499","project" : "Espresso_Test" "devices": ["Samsung Galaxy S20-10.0","Google Pixel 3-9.0"]} \
-H "Content-Type: application/json"

# Execute build using auto shard
curl -u "USERNAME:ACCESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/espresso/v2/build" \
-d {"app": "bs://3b79f7f0390dbe5f3550b544514bddcaa8197abe", "testSuite": "bs://84189ecbca832832ge0b1c3d8bacef95ad71c09c65ad2a00084995a5255dc86cab5f051e10f2","project" : "Espresso_Shard_Test" "devices": ["Samsung Galaxy S20-10.0","Google Pixel 3-9.0"], "shards" : {"numberOfShards" : 2}} \
-H "Content-Type: application/json"

# Execute build using shard mapping strategy
curl -u "USERNAME:ACCESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/espresso/v2/build" \
-d {"app": "bs://3b79f7f0390dbe5f3550b544514bddcaa8197abe", "testSuite": "bs://832ge0b1c3d8bacef95ad71c09c65ad2a0008499","project" : "Espresso_Shard_Test" "devices": ["Samsung Galaxy S20-10.0","Google Pixel 3-9.0"], "shards" : {"numberOfShards" : 2, "mapping" : [{"name" : "InputTests", "strategy" : "class", "values" : ["com.sample.browserstack.samplecalculator.EnsureInputTests", "com.sample.browserstack.samplecalculator.EnsureOperationTests"]},{"name" : "RandomTests", "strategy" : "class", "values" : ["com.sample.browserstack.samplecalculator.EnsureRandomTests", "com.sample.browserstack.samplecalculator.ExampleInstrumentedTest"]}]}\
-H "Content-Type: application/json"

```

> Example Response

```json
{
    "message": "Success",
    "build_id": "235ab4338cec13ae6b8f7a6977344556ac00bccd6"
}

```


<p>The Build API allows you to start the Espresso test execution on BrowserStack. As part of the API request, you must specify the app you want to test, the test-suite that contains your Espresso test cases and device(s) list. </p>
<p><b>Sharding the test-suite:</b> In order to speed up your Espresso test executions, you can also split and execute the test-suite in multiple shards using the <b>shard</b> object parameter in the build API. There are different strategies available for sharding the test-suite on BrowserStack:</p>
1. Shard tests using package,class,annotation or size strategy
2. Shard tests using package,class,annotation or size strategy along with `deviceSelection` value as `any`/`all`
3. Shard tests using autoShard strategy 


<aside class="notice"> To know more about how to split your test-suite using shards, refer to our documentation - /docs/espresso/shards </aside>

**REQUEST**

<span style="color:darkred">**POST**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/espresso/v2/build`

**Request Parameters** <br>

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  app <br><sub><sup>required</sup></sub> | string | App url of app uploaded on BrowserStack. <br> <b>Example</b> `bs://3b79f7f0390dbe5f3550b544514bddcaa8197abe` |
|  testSuite <br><sub><sup>required</sup></sub> | string | Test url of test uploaded on BrowserStack. <br> <b>Example</b>  `bs://832ge0b1c3d8bacef95ad71c09c65ad2a0008499` |
|  devices <br><sub><sup>required</sup></sub> | string | Array of devices on which you want the test-suite execution. <br> <b>Example</b>  `["Samsung Galaxy S8-7.0","Google Pixel 3-9.0"]` |
|  project <br><sub><sup>optional</sup></sub> | string | Name of the project. It can be used as a constant to list multiple build executions under same project name. <br> <b>Example</b>  `Espresso_Test` |
|  shards <br><sub><sup>optional</sup></sub>  | object | Shard object to split and execute the test-suite in shards. You can specify the `numberOfShards` and `mapping` object as shown in example request. |

<br>

**RESPONSE** <br>
Once the build is successfully started, an object containing the `build_id` will be returned. 



<br>
<br>

### Get build summary

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" 
  -X GET "https://api-cloud.browserstack.com/app-automate/espresso/v2/builds/{build_id}"
```

> Example Response

```json
{
    "id": "235ab4338cec13ae6b8f7a6977344556ac00bccd6",
    "framework": "espresso",
    "duration": 83,
    "status": "failed",
    "input_capabilities": {
        "devices": [
            "Samsung Galaxy S20-10.0",
            "OnePlus 7-9.0",
            "Google Pixel 3-9.0"
        ],
        "project": "Espresso_Test",
        "app": "bs://4a79f7f0390dbe5f3550b544514bddcaa8197abe",
        "testSuite": "bs://410fe0b1c3d8bacef95ad71c09c65ad2a0008499"
    },
    "start_time": "2020-06-04 07:43:49 UTC",
    "app_details": {
        "url": "bs://4a79f7f0390dbe5f3550b544514bddcaa8197abe",
        "bundle_id": "com.sample.browserstack.samplecalculator",
        "version": "1.0",
        "name": "app-debug.apk"
    },
    "test_suite_details": {
        "url": "bs://410fe0b1c3d8bacef95ad71c09c65ad2a0008499",
        "bundle_id": "com.sample.browserstack.samplecalculator.test",
        "version": "",
        "name": "app-debugTest.apk"
    },
    "devices": [
        {
            "device": "Samsung Galaxy S20",
            "os": "android",
            "os_version": "10.0",
            "sharding": false,
            "sessions": [
            {
                "id": "71c55a08d7e33651d962ad676c7d6a0a09f02702",
                "status": "failed",
                "start_time": "2020-06-04 07:44:07 +0000",
                "duration": 62,
                "testcases": {
                    "count": 9,
                    "status": {
                        "passed": 3,
                        "failed": 6,
                        "skipped": 0,
                        "timedout": 0,
                        "error": 0,
                        "running": 0,
                        "queued": 0
                    }
                }
            }]
        },
        {
            "device": "OnePlus 7",
            "os": "android",
            "os_version": "9.0",
            "sharding": false,
            "sessions": [
            {
                "id": "225c3cb7d1f7560635f6c83eafe418a2fabbef0d",
                "status": "failed",
                "start_time": "2020-06-04 07:44:10 +0000",
                "duration": 59,
                "testcases": {
                    "count": 9,
                    "status": {
                        "passed": 3,
                        "failed": 6,
                        "skipped": 0,
                        "timedout": 0,
                        "error": 0,
                        "running": 0,
                        "queued": 0
                    }
                }
            }]
        },
        {
            "device": "Google Pixel 3",
            "os": "android",
            "os_version": "9.0",
            "sharding": false,
            "sessions": [
            {
                "id": "a92460f7f5fd21f73673060d4046199e6a94d9e6",
                "status": "failed",
                "start_time": "2020-06-04 07:44:08 +0000",
                "duration": 62,
                "testcases": {
                    "count": 9,
                    "status": {
                        "passed": 3,
                        "failed": 6,
                        "skipped": 0,
                        "timedout": 0,
                        "error": 0,
                        "running": 0,
                        "queued": 0
                    }
                }
            }]
        }
    ]
}
```
Get the details about your test-suite execution. You can view the details related any build exceution like devices, shards, build status etc. 


**REQUEST**

<span style="color:darkgreen">**GET**</span> &nbsp;&nbsp;&nbsp;&nbsp; `app-automate/espresso/v2/builds/{build_id}`

**Path Parameter** <br>

Name | Type | Description
--------- | ------- | -----------
build_id <br><sub><sup>required</sup></sub> | string |The unique ID of your Espresso build execution. <br> <b>Example</b> `8d3f5scd2dfa35ddb1265d7ebb4e6bc55d46` |

<br>
<br>

**RESPONSE**

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  id     | string | ID of the build. <br> <b>Example</b> `235ab4338cec13ae6b8f7a6977344556ac00bccd6` |
|  framework | string | Name of the framework. <br> <b>Value</b> `espresso` |
|  duration | string | Duration of the build in ms. <br> <b>Example</b> `83` |
|  status  | array[string] | The overall status of the build. <br> <b>Values</b> `passed`/`failed`/`error`/`running`/`timedout`/`queued`/`skipped` |
|  input_capabilities  | object | Details of all the input parameters provided by the user inside build execution API.|
|  start_time | string | Time at which test execution was started. <br> <b>Example</b> `2020-06-04 07:43:49 UTC` |
|  app_details     | object | Details about the app uploaded on BrowserStack. |
|  test_suite_details | object | Details about the test-suite uploaded on BrowserStack. |
|  devices | array[object] | Details about each device execution in the build. |

<br>
<br>


### List recent builds

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/espresso/v2/builds"


# List builds using the project filter
curl -u "USERNAME:ACCESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/espresso/v2/builds?project=<project_name>"
```

> Example Response

```json
{
    "builds": [
        {
            "build_id": "8d3f5scd2dfa35ddb1265d7ebb4e6bc55d46",
            "start_time": "2019-11-06 13:07:45 UTC"    
        },
        {
            "build_id": "235ab4338cec13ae6b8f7a6977344556ac00bccd6",
            "start_time": "2020-06-04 07:43:49 UTC"    
        }
    ]
}

```

Fetch the list of last 20 test builds which will be sorted by timestamp. You can also use the `project` filter, which will return the last 20 test builds for that project name. If no test builds are found, the list will be empty.


**REQUEST**

<span style="color:darkgreen">**GET**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/espresso/v2/builds`

**Query Parameter** <br>

For getting the list of builds using the project filter:

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  app <br><sub><sup>required</sup></sub> | object | App url of app uploaded on BrowserStack. <br> <b>Example</b> `bs://3b79f7f0390dbe5f3550b544514bddcaa8197abe` |

<aside class="notice"> To know more about how to split your test-suite using shards, refer to our documentation - /docs/espresso/shards </aside>


**RESPONSE**

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  builds | array[object] | List of builds containing build ID and their timestamp. |

<br>
<br>

### Delete a build

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X DELETE "https://api-cloud.browserstack.com/app-automate/espresso/v2/builds/<build_id>"
```

> Example Response

```json
{
    "success": {
        "message": "Build was deleted."
    }
} 
```

Delete the build using the build ID.


**REQUEST**

<span style="color:darkred">**DELETE**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/espresso/v2/builds/<build_id>`

**Query Parameter** <br>


| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  build_id <br><sub><sup>required</sup></sub> | string | Build ID of the build to be deleted. <br> <b>Example</b> `235ab4338cec13ae6b8f7a6977344556ac00bccd6` |

<br>

**RESPONSE**

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  builds | array[object] | List of builds containing build ID and their timestamp. |

<br>
<br>




<!------------SESSION APIS----------------->

## Sessions
<p> Each execution of test-suite on individual device(s) is treated as a session on Browserstack.</p>
<p><b> Shards:</b> In case you are using the shards to split your Espresso test-suite in the build API endpoint, then each shard execution on a device represents an individual session.</p>
<p> You can use the Session REST API endpoints, to perform the following actions:
1. Get the session details
2. Get the JUnit report for the session
3. Get the code coverage report for the session


### Get session details

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X DELETE "https://api-cloud.browserstack.com/app-automate/espresso/v2/builds/57dd68e05f76ca3c9c0d4600fd78ae064fa537bb/sessions/c9215a31aace1d2b885f1c7a9f5d73bce55b4543"
```

> Example Response

```json
{
    "id": "c9215a31aace1d2b885f1c7a9f5d73bce55b4543",
    "status": "failed",
    "start_time": "2020-06-04 07:44:20 +0000",
    "duration": 43,
    "testcases": {
        "count": 6,
        "status": {
            "passed": 0,
            "failed": 6,
            "skipped": 0,
            "timedout": 0,
            "error": 0,
            "running": 0,
            "queued": 0
        },
        "data": [
            {
                "class": "EnsureOperationTests",
                "testcases": [
                    {
                        "name": "ensureMultiplicationWorks",
                        "start_time": "2020-06-04 07:44:25 +0000",
                        "status": "failed",
                        "duration": "2.057",
                        "video": "https://api.browserstack.com/app-automate/espresso/builds/57cc68e05f76ca3c9c0d4600fd78ae064fa537bb/sessions/tests/c9215a31aace1d2b885f1c7a9f5d73bce55b4543406d4de4/video#t=0,5",
                        "id": "c9215a31aace1d2b885f1c7a9f5d73bce55b4543406d4de4",
                        "instrumentation_log": "https://api.browserstack.com/app-automate/espresso/builds/57cc68e05f76ca3c9c0d4600fd78ae064fa537bb/sessions/tests/c9215a31aace1d2b885f1c7a9f5d73bce55b4543406d4de4/instrumentationlogs"
                    },
                    {
                        "name": "ensureDivisionWorks",
                        "start_time": "2020-06-04 07:44:31 +0000",
                        "status": "failed",
                        "duration": "1.96",
                        "video": "https://api.browserstack.com/app-automate/espresso/builds/57cc68e05f76ca3c9c0d4600fd78ae064fa537bb/sessions/tests/c9215a31aace1d2b885f1c7a9f5d73bce55b4543e5295377/video#t=6,11",
                        "id": "c9215a31aace1d2b885f1c7a9f5d73bce55b4543e5295377",
                        "instrumentation_log": "https://api.browserstack.com/app-automate/espresso/builds/57cc68e05f76ca3c9c0d4600fd78ae064fa537bb/sessions/tests/c9215a31aace1d2b885f1c7a9f5d73bce55b4543e5295377/instrumentationlogs"
                    }
                ]
            },
            {
                "class": "EnsureInputTests",
                "testcases": [
                    {
                        "name": "ensureMultipleInputIsHandled",
                        "start_time": "2020-06-04 07:44:50 +0000",
                        "status": "failed",
                        "duration": "0.313",
                        "video": "https://api.browserstack.com/app-automate/espresso/builds/57cc68e05f76ca3c9c0d4600fd78ae064fa537bb/sessions/tests/c9219a12aace1d2b885f1c7a9f5d73bce55b454324e815c7/video#t=25,28",
                        "id": "c9219a12aace1d2b885f1c7a9f5d73bce55b454324e815c7",
                        "instrumentation_log": "https://api.browserstack.com/app-automate/espresso/builds/57cc68e05f76ca3c9c0d4600fd78ae064fa537bb/sessions/tests/c9219a12aace1d2b885f1c7a9f5d73bce55b454324e815c7/instrumentationlogs"
                    }
                ]
            }
        ]
    },
}
```

Fetch the details about the session execution including session status, duration and details about each test case execution in that session.


**REQUEST**

<span style="color:darkred">**DELETE**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/espresso/v2/builds/<build_id>/sessions/<session_id>`

**Query Parameter** <br>

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  id <br><sub><sup>required</sup></sub> | string | Build ID of the build to which the session belongs. <br> <b>Example</b> `57dd68e05f76ca3c9c0d4600fd78ae064fa537bb` |
|  session_id <br><sub><sup>required</sup></sub> | string | Session ID of the device execution. <br> <b>Example</b> `c9215a31aace1d2b885f1c7a9f5d73bce55b4543` |

<br>

**RESPONSE**

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  id  | string | Session ID. |
|  status | string | Status of the session. <br> <b>Values:</b> `running`/`failed`/`error`/`timedout`/`passed`/`queued`/`skipped` |
|  start_time | string | Time at which the session was started. <br> <b>Example</b> `7.0` |
|  duration | integer | Duration of the session |
|  testcases | object | Details about the count of test cases, their status and details about each test case execution in the given session  |


<aside class="notice">Note: In case the session corresponds to a shard execution, there will be an additional parameter in the response object named <b>shard</b> which will contain the details about the name of the shard and the strategy used.
</aside>



<br>
<br>


### Get JUnit report

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X DELETE "https://api-cloud.browserstack.com/app-automate/espresso/v2/builds/57dd68e05f76ca3c9c0d4600fd78ae064fa537bb/sessions/c9215a31aace1d2b885f1c7a9f5d73bce55b4543/report"
```

> Example Response

```xml
<?xml version="1.0"?>
<testsuites>
    <testsuite name="com.sample.browserstack.samplecalculator.EnsureInputTests" tests="2" failures="2" skipped="0" timedout="0" errors="0" time="4.419" timestamp="2020-06-04 07:44:14 +0000">
        <properties>
            <property session_id="c9215a31aace1d2b885f1c7a9f5d73bce55b4543"/>
            <property devicename="Google Pixel 3"/>
            <property os="Android"/>
            <property version="9"/>
        </properties>
        <testcase name="ensureMultipleInputIsHandled" classname="com.sample.browserstack.samplecalculator.EnsureInputTests" result="failed" test_id="be2460f7f5fd21f73673060d4046199e6a94d9e624e815c7" time="0.422" video_url="https://www.browserstack.com/s3-upload/bs-video-logs-aps/s3-ap-south-1/be2460f7f5fd21f73673060d4046199e6a94d9e6/video-be2460f7f5fd21f73673060d4046199e6a94d9e6.mp4#t=0,3">
            <failure>java.lang.RuntimeException: Unable to capture screenshot.
	        ... 32 more
            </failure>
        </testcase>
    </testsuite>
    <testsuite name="com.sample.browserstack.samplecalculator.EnsureOperationTests" tests="4" failures="4" skipped="0" timedout="0" errors="0" time="22.643" timestamp="2020-06-04 07:44:22 +0000">
        <properties>
            <property session_id="c9215a31aace1d2b885f1c7a9f5d73bce55b4543"/>
            <property devicename="Google Pixel 3"/>
            <property os="Android"/>
            <property version="9"/>
        </properties>
        <testcase name="ensureMultiplicationWorks" classname="com.sample.browserstack.samplecalculator.EnsureOperationTests" result="failed" test_id="be2460f7f5fd21f73673060d4046199e6a94d9e6406d4de4" time="2.366" video_url="https://www.browserstack.com/s3-upload/bs-video-logs-aps/s3-ap-south-1/be2460f7f5fd21f73673060d4046199e6a94d9e6/video-be2460f7f5fd21f73673060d4046199e6a94d9e6.mp4#t=8,13">
            <failure>java.lang.RuntimeException: Unable to capture screenshot.
	        ... 32 more
            </failure>
        </testcase>
    <testsuite name="com.sample.browserstack.samplecalculator.ExampleInstrumentedTest" tests="1" failures="0" skipped="0" timedout="0" errors="0" time="0.009" timestamp="2020-06-04 07:45:01 +0000">
        <properties>
            <property session_id="c9215a31aace1d2b885f1c7a9f5d73bce55b4543"/>
            <property devicename="Google Pixel 3"/>
            <property os="Android"/>
            <property version="9"/>
        </properties>
        <testcase name="useAppContext" classname="com.sample.browserstack.samplecalculator.ExampleInstrumentedTest" result="passed" test_id="be2460f7f5fd21f73673060d4046199e6a94d9e65e747bcf" time="0.009" video_url="https://www.browserstack.com/s3-upload/bs-video-logs-aps/s3-ap-south-1/be2460f7f5fd21f73673060d4046199e6a94d9e6/video-be2460f7f5fd21f73673060d4046199e6a94d9e6.mp4#t=47,50"/>
    </testsuite>
</testsuites>
```

Fetch the details about the session execution including session status, duration and details about each test case execution in that session.


**REQUEST**

<span style="color:darkgreen">**GET**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/espresso/v2/builds/<build_id>/sessions/<session_id>/report`

**Path Parameters** <br>

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  build_id <br><sub><sup>required</sup></sub> | string | Build ID of the build to which the session belongs. <br> <b>Example</b> `57dd68e05f76ca3c9c0d4600fd78ae064fa537bb` |
|  session_id <br><sub><sup>required</sup></sub> | string | Session ID of the device execution. <br> <b>Example</b> `c9215a31aace1d2b885f1c7a9f5d73bce55b4543` |

<br>

**RESPONSE** <br>
The JUnit report comprising the details of each test case execution in the session.


<aside class="notice">Note: In case the session corresponds to a shard execution, there will be an additional parameter in the response object named <b>shard</b> which will contain the details about the name of the shard and the strategy used.
</aside>



<br>
<br>

### Get coverage report

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X DELETE "https://api-cloud.browserstack.com/app-automate/espresso/v2/builds/57dd68e05f76ca3c9c0d4600fd78ae064fa537bb/sessions/c9215a31aace1d2b885f1c7a9f5d73bce55b4543/coverage"
```

> Example Response

```xml

```

Fetch the details about the session execution including session status, duration and details about each test case execution in that session.


**REQUEST**

<span style="color:darkgreen">**GET**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/espresso/v2/builds/<build_id>/sessions/<session_id>/report`

**Path Parameters** <br>

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  build_id <br><sub><sup>required</sup></sub> | string | Build ID of the build to which the session belongs. <br> <b>Example</b> `57dd68e05f76ca3c9c0d4600fd78ae064fa537bb` |
|  session_id <br><sub><sup>required</sup></sub> | string | Session ID of the device execution. <br> <b>Example</b> `c9215a31aace1d2b885f1c7a9f5d73bce55b4543` |

<br>

**RESPONSE** <br>
The JUnit report comprising the details of each test case execution in the session.


<aside class="notice">Note: In case the session corresponds to a shard execution, there will be an additional parameter in the response object named <b>shard</b> which will contain the details about the name of the shard and the strategy used.
</aside>



<br>
<br>





## Change log

<b>2020-01-01</b>

<b>MAJOR</b> : Support for multiple shard strategies in Espresso. You can now use shard feature in Execute API command.

<br>

<b>2020-02-02</b>

<b>MAJOR</b> : Support for multiple shard strategies in Espresso. You can now use shard feature in Execute API command.


