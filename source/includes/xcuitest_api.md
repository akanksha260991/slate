# XCUITest API

BrowserStack provides support for the XCUITest testing framework for iOS. You can run your XCUI tests written in both Swift and Objective C. 

In order to get started with XCUITest you need to make use of our XCUITest API to perform the following steps:
<br>
<br>
1. Upload your app <br>
2. Upload your test-suite <br>
3. Execute your build <br>

Once the build execution is completed, the XCUITest Builds and Sessions API endpoints can be used to view the execution details.

<aside class="notice">Note: Each device execution in XCUITest is treated as a session.
</aside> 


<!------------APPS APIS----------------->

## xcui:Apps

<p>In order to test your native and hybrid apps on BrowserStack, you need to upload your iOS apps and XCUI test-suite on BrowserStack using our REST API.</p>

###  xcui:Upload an app

> Example Request

```shell
# Upload app from local machine
curl -u "USERNAME:ACESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/upload" \
-F "file=@/path/to/test/file/app-debug.ipa" \
-F 'data={"custom_id": "SampleApp"}'

# Upload app using public URL
curl -u "USERNAME:ACESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/upload" \
-F 'data={"url": "https://www.browserstack.com/app-automate/sample-apps/ios/BrowserStack-SampleApp.ipa","custom_id":"SampleApp"}'
```

> Example Response

```json
{
   "app_url":"bs://e8ddcb5649a8280ca89075bfd8f151115bba6b3",
   "custom_id":"SampleApp",
   "shareable_id":"steve/SampleApp"
}
```

Upload your iOS app on BrowserStack. There are two ways to upload the apps:

1. Upload an app from local machine
2. Upload an app using a public URL


**REQUEST**

<span style="color:darkred">**POST**</span> &nbsp;&nbsp;&nbsp; `app-automate/xcuitest/v2/upload`

**Request Parameters** <br>

Upload an app from local machine

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  file <br><sub><sup>required</sup></sub> | string | The path to the app file in your local system. <br> <b>Example</b> `/Users/Desktop/Apps/app-debug.ipa` |
|  custom_id <br><sub><sup>optional</sup></sub> | string | Constant name for the uploaded app. You can upload multiple apps using the same custom id. <br> <b>Example</b>  `SampleApp` |


<br>
Upload an app using a public URL

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  url <br><sub><sup>required</sup></sub> | string | Remote public URL to the test-suite file. <br> <b>Example</b> `https://www.browserstack.com/app-automate/sample-apps/ios/CalculatorTest.ipa` |
|  custom_id <br><sub><sup>optional</sup></sub> | string | Specify a constant name for the test-suite. You can use the same custom ID for multiple versions of a test-suite you upload. <br> <b>Example</b>  `SampleTest` |

<br>

**RESPONSE**

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  app_url     | string | App url of the app uploaded on BrowserStack. <br> <b>Example</b> `bs://e8ddcb5649a8280ca89075bfd8f151115bba6b3` |
|  custom_id     | string | Unique name identifier for your app. <br> <b>Example</b> `SampleApp` |
|  shareable_id  | string | ID which can be used by other users of your team for accessing the app. <br> <b>Example</b>  `steve/SampleApp` |


<br>
<br>


###  xcui:Get app details

> Example Request

```shell
curl -u "USERNAME:ACESS_KEY" \
-X GET "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/apps/c8ddcb5649a8280ca800075bfd8f151115bba6b3" 
```

> Example Response

```json
{
    "app_name": "app-debug.ipa",
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

<span style="color:darkred">**POST**</span> &nbsp;&nbsp;&nbsp; `app-automate/xcuitest/v2/apps/<app_id>`

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  app_id <br><sub><sup>required</sup></sub> | string | Unique ID of the test-suite uploaded on BrowserStack. <br> <b>Example</b> `c8ddcb5649a8280ca800075bfd8f151115bba6b3` |

<br>

**RESPONSE**


| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  app_name     | string | Name of the .ipa file. <br> <b>Example</b> `app-debug.ipa` |
|  app_version     | string | The version of your app. <br> <b>Example</b> `1.2.0` |
|  app_url  | string | App url of the app uploaded on BrowserStack. <br> <b>Example</b>  `bs://c8ddcb5649a8280ca800075bfd8f151115bba6b3` |
|  app_id     | string | Unique ID of the app uploaded on BrowserStack. <br> <b>Example</b> `c8ddcb5649a8280ca800075bfd8f151115bba6b3` |
|  uploaded_at     | string | Timestamp value at which the app was uploaded on BrowserStack servers.. <br> <b>Example</b> `2020-05-05 14:52:54 UTC` |
|  custom_id     | string | Constant name for the uploaded app. You can upload multiple apps using the same custom id.. <br> <b>Example</b> `SampleApp` |
|  shareable_id  | string | ID which can be used by other users of your team to access the app. <br> <b>Example</b>  `steve/SampleApp` |


<br>
<br>

###  xcui:List recent apps

> Example Request

```shell
curl -u "USERNAME:ACESS_KEY" \
-X GET "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/apps"
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
     "app_name": "app-debug.ipa",
    "app_version": "1.2.0",
    "app_url": "bs://c8ddcb5649a8280ca800075bfd8f151115bba6b3",
    "app_id": "c8ddcb5649a8280ca800075bfd8f151115bba6b3",
    "uploaded_at": "2020-05-05 14:52:54 UTC",
    "custom_id": "SampleApp",
    "shareable_id": "steve/SampleApp"
  }
]
```

 Fetch a list of your recently uploaded apps and its details such as `app_url`, `custom ID`, `shareable ID` and upload timestamp for each app.

<br>

**REQUEST**

<span style="color:darkgreen">**GET**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/xcuitest/v2/apps`

<br>

**RESPONSE**

The response is an array of the app details object.

<br>
<br>
<br>

###  xcui:Delete an app

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X DELETE "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/apps/<app_id>"
```

> Example Response

```json
{
    "success": {
        "message": "App was deleted."
    }
} 
```


We automatically delete your uploaded apps after 30 days from the day of upload. However, you can also use our REST API to explicitly delete an app before this 30 day time period. The app can be deleted using the `app_id`.

<br>

**REQUEST**

<span style="color:darkred">**DELETE**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/xcuitest/v2/apps/<app_id>`

**Path Parameter** <br>

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  app_id     | string | App ID of the app uploaded on BrowserStack. <br> <b>Example</b> `f7c874f21852ba57957a3fdc33f47514288c4ba4` |

<br>

**RESPONSE**

There will a **success** or **error** object depending on the success/failure of the app delete request.

<br>
<br>




<!------------TEST-SUITE APIS----------------->

##  xcui:Test suites
In order to test your iOS apps using XCUITest framework, you need to upload your iOS app and the XCUI test-suite on BrowserStack. Using the XCUI Test-Suite API endpoints, you can perform the following:

1. View the recent test-suite uploads <br>
2. View the test-suite info <br>
3. Delete any test-suite <br>


###  xcui:Upload a test-suite

> Example Request

```shell
# Upload test-suite from local machine
curl -u "USERNAME:ACCESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/XCUI/v2/test-suite" \
-F "file=@/path/to/test/file/app-debug-androidTest.ipa" \
-F 'data={"custom_id": "SampleTest"}'


# Upload test-suite using a public URL
curl -u "USERNAME:ACESS_KEY"  \
-X POST "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/test-suite" \
-F 'data={"url": "https://www.browserstack.com/app-automate/sample-apps/ios/CalculatorTest.ipa","custom_id":"SampleTest"}'

```

> Example Response

```json
{
    "test_url":"bs://f7c874f21852ba57957a3fdc33f47514288c4ba4",
    "custom_id":"SampleTest",
    "shareable_id":"steve/SampleTest"
}
```

Upload your XCUI test-suite on BrowserStack. There are two ways to upload the test-suite:
<br>
<br>
1. Upload a test-suite from local machine <br>
2. Upload a test-suite using a public URL <br>

<br>

**REQUEST**

<span style="color:darkred">**POST**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/xcuitest/v2/test-suite`
<br>

**Request Parameters** <br>
Upload a test-suite from local machine

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  file <br><sub><sup>required</sup></sub> | string | Path to your test-suite. <br> <b>Example</b> `/Users/Desktop/Appium/app-debug.ipa` |
|  custom_id <br><sub><sup>optional</sup></sub> | string | Specify a constant name for the test-suite. You can upload multiple test-suites using the same custom ID. <br> <b>Example</b>  `SampleTest` |

<br>
Upload a test-suite using a public URL

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  url <br><sub><sup>required</sup></sub> | string | Remote public URL to the test-suite file. <br> <b>Example</b> `https://www.browserstack.com/app-automate/sample-apps/ios/CalculatorTest.ipa` |
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

###  xcui:Get test-suite details

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/test-suite/<test_suite_id>" 
```

> Example Response

```json
{
    "test_suite_name": "app-debug-androidTest.ipa",
    "test_suite_url": "bs://f7c874f21852ba57957a3fdc33f47514288c4ba4",
    "test_suite_id": "f7c874f21852ba57957a3fdc33f47514288c4ba4",
    "uploaded_at": 1591254892,
    "custom_id": null,
    "framework": "xcuitest"
}
```

View the details about any test-suite uploaded on BrowserStack. You need to pass the `test_suite_id` to fetch the details of any test-suite file.

<br>

**REQUEST**

<span style="color:darkred">**POST**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/xcuitest/v2/test-suite/<test_suite_id>`
<br>

**Path Parameter** <br>

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  test_suite_id <br><sub><sup>required</sup></sub> | string | Unique ID of the test-suite uploaded on BrowserStack. <br> <b>Example</b> `f7c874f21852ba57957a3fdc33f47514288c4ba4` |

<br>

**RESPONSE**

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  test_suite_name     | string | Name of the test-suite file. <br> <b>Example</b> `app-debug-androidTest.ipa` |
|  test_suite_url     | string |  Test url obtained after successful upload of test-suite on BrowserStack. <br> <b>Example</b> `bs://f7c874f21852ba57957a3fdc33f47514288c4ba4` |
|  test_suite_id  | string | Unique ID of the test-suite uploaded on BrowserStack. <br> <b>Example</b>  `f7c874f21852ba57957a3fdc33f47514288c4ba4` |
|  uploaded_at     | timestamp | Timestamp value at which the app was uploaded on BrowserStack servers. <br> <b>Example</b> `1591254892`|
|  custom_id     | string | Constant name for the test-suite. <br> <b>Example</b> `SampleTest` |
|  framework     | string | Name of the framework. <br> <b>Value</b> `xcuitest` |

<br>
<br>
<br>



###  xcui:List recent test-suites

> Example Request

```shell
curl -u "USERNAME:ACESS_KEY" \
-X GET "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/test-suites"
```

> Example Response

```json
[
  {
    "test_suite_name": "app-debug-androidTest.ipa",
    "test_suite_url": "bs://f7c874f21852ba57957a3fdc33f47514288c4ba4",
    "test_suite_id": "f7c874f21852ba57957a3fdc33f47514288c4ba4",
    "uploaded_at": 1590083493,
    "custom_id": "SampleTest",
    "framework": "xcuitest"
  },
  {
    "test_suite_name": "app-debugTest.ipa",
    "test_suite_url": "bs://d819081c97b4a61f6250b441cbe3efaea4c99210",
    "test_suite_id": "d819081c97b4a61f6250b441cbe3efaea4c99210",
    "uploaded_at": 1589900729,
    "custom_id": "ShardTest",
    "framework": "xcuitest"
  }
]
```


 Fetch a list of your recently uploaded test-suites and its details such as test_url, custom ID, shareable ID and upload timestamp for each test-suite.

<br>

**REQUEST**

<span style="color:darkgreen">**GET**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/xcuitest/v2/test-suites`

<br>

**RESPONSE**

The response is an array of the test-suite details object.


<br>
<br>
<br>


###  xcui:Delete a test-suite

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X DELETE "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/test-suites/<test_suite_id>"
```

> Example Response

```json
{
    "success": {
        "message": "Test-suite was deleted."
    }
} 
```


We automatically delete your uploaded test-suites after 30 days from the day of upload. However, you can also use our REST API to explicitly delete a test-suite before this 30 day time period. The test-suite can be deleted using the test-suite's `test_url`.

<br>

**REQUEST**

<span style="color:darkred">**DELETE**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/xcuitest/v2/test-suites/<test_suite_url>`

**Path Parameter** <br>

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  test_suite_id     | string | Test suite ID of the test-suite uploaded on BrowserStack. <br> <b>Example</b> `f7c874f21852ba57957a3fdc33f47514288c4ba4` |

<br>

**RESPONSE**

There will a **success** or **error** object depending on the success/failure of the test-suite delete request.

<br>
<br>





<!------------BUILD APIS----------------->

##  xcui:Builds
<p>An XCUI build represents your test-suite execution on Browserstack. Once you upload your iOS app and XCUI test-suite, you can use the Build REST API endpoints, to perform the following actions:</p>
<p>
1. Execute the build <br>
2. Get details about your build executions <br>
3. Delete an XCUITest build 
</p>

###  xcui:Execute a build

> Example Request

```shell
curl -X POST "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/build" \
-d '{"devices": ["iPhone 11 Pro-13"], "app": "bs://3b79f7f0390dbe5f3550b544514bddcaa8197abe", "testSuite": "bs://832ge0b1c3d8bacef95ad71c09c65ad2a0008499", "project": "XCUISampleBuild" }' \
-H "Content-Type: application/json" \
-u "akankshaverma1:HxWsPGucWDxLU1qHYzxn"
```

> Example Response

```json
{
    "message": "Success",
    "build_id": "235ab4338cec13ae6b8f7a6977344556ac00bccd6"
}

```


<p>The Build API allows you to start the XCUI test execution on BrowserStack. As part of the API request, you must specify the app you want to test, the test-suite that contains your XCUI test cases and device(s) list. </p>

You can also specify optional parameters like `debugscreenshots` for enabling the screenshots capture, `only-testing` to test only some selected classes or tests etc.


**REQUEST**

<span style="color:darkred">**POST**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/xcuitest/v2/build`

**Request Parameters** <br>

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  app <br><sub><sup>required</sup></sub> | string | App url of app uploaded on BrowserStack. <br> <b>Example</b> `bs://3b79f7f0390dbe5f3550b544514bddcaa8197abe` |
|  testSuite <br><sub><sup>required</sup></sub> | string | Test url of test uploaded on BrowserStack. <br> <b>Example</b>  `bs://832ge0b1c3d8bacef95ad71c09c65ad2a0008499` |
|  devices <br><sub><sup>required</sup></sub> | string | Array of devices on which you want the test-suite execution. <br> <b>Example</b>  `["Samsung Galaxy S8-7.0","Google Pixel 3-9.0"]` |
|  project <br><sub><sup>optional</sup></sub> | string | Name of the project. It can be used as a constant to list multiple build executions under same project name. <br> <b>Example</b>  `XCUI_Test` |
|  debugscreenshots <br><sub><sup>optional</sup></sub>  | boolean | Enable saving of screenshots automatically captured by XCode. Screenshots can be rendered by accessing the rawlogs using the XCUITest sessions API. Values: `true`/`false` |
|  skip-testing <br><sub><sup>optional</sup></sub>  | boolean | Specify the classes or tests to be skipped in the build. <br> <b>Example</b> : `["SampleXCUITests/testLogin","SampleXCUITests/testSignUp"]` |
|  only-testing <br><sub><sup>optional</sup></sub>  | array | Specify the classes or tests to be executed in the build. <br> <b>Example</b> : `["SampleXCUITests/testAlert"]` |
|  callbackURL <br><sub><sup>optional</sup></sub>  | string | Specify a callback url where we can send a confirmation once your individual test execution is completed. |
|  projectNotifyURL <br><sub><sup>optional</sup></sub>  | string | Notify url for projects where we can send a confirmation once execution of all the builds under the project are completed. |
|  video <br><sub><sup>optional</sup></sub>  | boolean | Enable/Disable the video of the test run. <br> <b>Default</b> : `true` |
|  deviceLogs <br><sub><sup>optional</sup></sub>  | boolean | Enable the device logs. <br> <b>Default</b> : `false` |
|  networkLogs <br><sub><sup>optional</sup></sub>  | boolean | Enable the network logs. <br> <b>Default</b> : `false` |
|  local <br><sub><sup>optional</sup></sub>  | boolean | Required if you are testing against internal/local servers. <br> <b>Default</b> : `false` |
|  localIdentifier <br><sub><sup>optional</sup></sub>  | string | If you are using same account to test multiple applications, you can setup named connection using the localIdentifier option. <br> <b>Example</b> : `Test123` |
|  networkProfile <br><sub><sup>optional</sup></sub>  | string |  Simulate different network conditions from the [list of existing](https://www.browserstack.com/app-automate/network-simulation) network profiles. <br> <b>Example</b> : `2g-gprs-good` |
|  customNetwork <br><sub><sup>optional</sup></sub>  | string |  Simulate the custom network conditions. <br> <b>Format</b> : `download speed (kbps), upload speed (kbps), latency (ms), packet loss (%)` |
|  geoLocation <br><sub><sup>optional</sup></sub>  | string | Test how your app behaves in specific countries. View the [list of supported countries](https://www.browserstack.com/ip-geolocation).<br> <b>Example</b> : `CN` for China |
|  gpsLocation <br><sub><sup>optional</sup></sub>  | string |  Simulate the location of the device to a particular GPS location. Acceptable range for latitude is -90 to +90 and for longitude is -180 to +180. <br> <b>Example</b> : `40.730610,-73.935242` |
|  locale <br><sub><sup>optional</sup></sub>  | string | Change the locale to test the localized version of your app. <br> <b>Example</b> : `fr` |
|  language <br><sub><sup>optional</sup></sub>  | string | Set the language of the app under test. <br> <b>Example</b> : `fr` |
|  deviceOrientation <br><sub><sup>optional</sup></sub>  | string | Set the language of the app under test. <br> <b>Default</b> : `potrait` |
|  idleTimeout <br><sub><sup>optional</sup></sub>  | integer | Specify the maximum time limit for which your tests can remain idle. Accepted values are between 60 sec to 900 sec. <br> <b>Example</b> : `80` |
|  uploadMedia <br><sub><sup>optional</sup></sub>  | array | Allows you to upload images or videos that are required during the test executions. <br> <b>Example</b> : `["media://49a8jg6280ca89075bfd8f15280ca89075bfd8f15", "media://9b7gd5s30ca89075bfd8f15280ca89075bfd8"]` |
|  otherApps <br><sub><sup>optional</sup></sub>  | array | Allows you to use uploaded apps that are required alongwith the main app during the test executions. <br> <b>Example</b> :  `["bs://49a8jg6280ca89075bfd8f15280ca89075bfd8f15", "bs://9b7gd5s30ca89075bfd8f15280ca89075bfd8"]` |

<br>

**RESPONSE** <br>
Once the build is successfully started, an object containing the `build_id` will be returned. 



<br>
<br>

###  xcui:Get build summary

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" 
  -X GET "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/builds/235ab4338cec13ae6b8f7a6977344556ac00bccd6"
```

> Example Response

```json
{
    "id": "235ab4338cec13ae6b8f7a6977344556ac00bccd6",
    "framework": "xcuitest",
    "duration": 30,
    "status": "passed",
    "input_capabilities": {
        "devices": [
            "iPhone X-11.0",
            "iPhone 8-11.0"
        ],
        "project": "XCUISampleBuild",
        "debugscreenshots": "true",
        "app": "bs://3b79f7f0390dbe5f3550b544514bddcaa8197abe",
        "testSuite": "bs://832ge0b1c3d8bacef95ad71c09c65ad2a0008499",
        "only-testing": [
            "SampleXCUITests/testAlert"
        ]
    },
    "start_time": "2020-06-08 14:30:41 UTC",
    "app_details": {
        "url": "bs://3b79f7f0390dbe5f3550b544514bddcaa8197abe",
        "bundle_id": "com.browserstack.Sample-iOS",
        "version": "1.0",
        "name": "app-debug.ipa"
    },
    "test_suite_details": {
        "url": "bs://832ge0b1c3d8bacef95ad71c09c65ad2a0008499",
        "bundle_id": "com.apple.test.SampleXCUITests-Runner",
        "version": "1.0",
        "name": "BrowserStack-SampleXCUITest.zip"
    },
    "devices": [
        {
            "device": "iPhone X",
            "os": "ios",
            "os_version": "11.0",
            "sharding": false,
            "sessions": [
                {
                    "id": "90a161aef48b475eeacc0f384e8909089a4a1282",
                    "status": "passed",
                    "start_time": "2020-06-08 14:30:58 +0000",
                    "duration": 12,
                    "testcases": {
                        "count": 1,
                        "status": {
                            "passed": 1,
                            "failed": 0,
                            "skipped": 0,
                            "timedout": 0,
                            "error": 0,
                            "running": 0,
                            "queued": 0
                        }
                    }
                }
            ]
        },
        {
            "device": "iPhone 8",
            "os": "ios",
            "os_version": "11.0",
            "sharding": false,
            "sessions": [
                {
                    "id": "t5809b1ed88dde3526b5d50160e583c68760e425",
                    "status": "passed",
                    "start_time": "2020-06-08 14:30:55 +0000",
                    "duration": 12,
                    "testcases": {
                        "count": 1,
                        "status": {
                            "passed": 1,
                            "failed": 0,
                            "skipped": 0,
                            "timedout": 0,
                            "error": 0,
                            "running": 0,
                            "queued": 0
                        }
                    }
                }
            ]
        }
    ]
}
```
Get the details about your XCUI build executions.


**REQUEST**

<span style="color:darkgreen">**GET**</span> &nbsp;&nbsp;&nbsp;&nbsp; `app-automate/xcuitest/v2/builds/{build_id}`

**Path Parameter** <br>

Name | Type | Description
--------- | ------- | -----------
build_id <br><sub><sup>required</sup></sub> | string |The unique ID of your XCUITest build execution. <br> <b>Example</b> `235ab4338cec13ae6b8f7a6977344556ac00bccd6` |

<br>
<br>

**RESPONSE**

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  id     | string | ID of the build. <br> <b>Example</b> `235ab4338cec13ae6b8f7a6977344556ac00bccd6` |
|  framework | string | Name of the framework. <br> <b>Value</b> `xcuitest` |
|  duration | string | Duration of the build in ms. <br> <b>Example</b> `83` |
|  status  | array[string] | The overall status of the build. <br> <b>Values</b> `passed`/`failed`/`error`/`running`/`timedout`/`queued`/`skipped` |
|  input_capabilities  | object | Details of all the input parameters provided by the user inside build execution API.|
|  start_time | string | Time at which test execution was started. <br> <b>Example</b> `2020-06-04 07:43:49 UTC` |
|  app_details     | object | Details about the app uploaded on BrowserStack. |
|  test_suite_details | object | Details about the test-suite uploaded on BrowserStack. |
|  devices | array[object] | Details about each device execution in the build. |

<br>
<br>


###  xcui:List recent builds

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/builds"


# List builds using the project filter
curl -u "USERNAME:ACCESS_KEY" \
-X POST "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/builds?project=XCUISampleBuild"
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

<span style="color:darkgreen">**GET**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/xcuitest/v2/builds`

**Query Parameter** <br>

For getting the list of builds using the project filter:

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  project <br><sub><sup>required</sup></sub> | string | Name of the project. <br> <b>Example</b> `XCUISampleBuild` |

<aside class="notice"> To know more about how to split your test-suite using shards, refer to our documentation - /docs/xcuitest/shards </aside>


**RESPONSE**

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  builds | array[object] | List of builds containing build ID and their timestamp. |

<br>
<br>

###  xcui:Delete a build

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X DELETE "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/builds/235ab4338cec13ae6b8f7a6977344556ac00bccd6"
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

<span style="color:darkred">**DELETE**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/xcuitest/v2/builds/<build_id>`

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

##  xcui:Sessions
<p> Each execution of test-suite on individual device(s) is treated as a session on Browserstack. You can use the Session REST API endpoints to get the session details. </p>

###  xcui:Get session details

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" \
-X DELETE "https://api-cloud.browserstack.com/app-automate/xcuitest/v2/builds/235ab4338cec13ae6b8f7a6977344556ac00bccd6/sessions/90a161aef48b475eeacc0f384e8909089a4a1282"
```

> Example Response

```json
{
    "id": "90a161aef48b475eeacc0f384e8909089a4a1282",
    "status": "passed",
    "start_time": "2020-06-08 14:30:58 +0000",
    "duration": 12,
    "testcases": {
        "count": 1,
        "status": {
            "passed": 1,
            "failed": 0,
            "skipped": 0,
            "timedout": 0,
            "error": 0,
            "running": 0,
            "queued": 0
        },
        "data": [
            {
                "class": "SampleXCUITests",
                "testcases": [
                    {
                        "name": "testAlert",
                        "start_time": "2020-06-08 14:31:00 +0000",
                        "status": "passed",
                        "duration": 9.563,
                        "video": "https://api.browserstack.com/app-automate/xcuitest/builds/235ab4338cec13ae6b8f7a6977344556ac00bccd6/sessions/tests/76a161aef48b475eeacc0f384e8909089a4a1282b76c8202/video#t=0,0",
                        "id": "76a161aef48b475eeacc0f384e8909089a4a1282b76c8202",
                        "instrumentation_log": "https://api.browserstack.com/app-automate/xcuitest/builds/235ab4338cec13ae6b8f7a6977344556ac00bccd6/sessions/tests/76a161aef48b475eeacc0f384e8909089a4a1282b76c8202/instrumentationlogs"
                    }
                ]
            }
        ]
    }
}
```

Fetch the details about the session execution including session status, duration and details about each test case execution in that session.


**REQUEST**

<span style="color:darkred">**DELETE**</span> &nbsp;&nbsp;&nbsp;&nbsp; `/app-automate/xcuitest/v2/builds/<build_id>/sessions/<session_id>`

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




<br>
<br>

## xcui:Change log

<b>2020-01-01</b>

<b>MAJOR</b> : The deprecation of the v1 API endpoints.

<br>

<b>2020-02-02</b>

<b>MAJOR</b> : New parameter added `idleTimeout`


