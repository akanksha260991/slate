---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for the BrowserStack Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors
  - espresso_api
  - xcuitest_api
  - custom_media_api

search: true
---

# Overview

<p>Welcome to BrowserStack App Automate API. You can use this API Reference to access all our API endpoints for automated testing of your apps on BrowserStack. The API's allows you integrate BrowserStack to your continuous integration environment. </p>

<p>The App Automate APIs have been grouped as:</p>

| API       | Description                         |
|-----------|--------|-------------------------------------|
|  <b>Espresso API</b> | Provides a simple and flexible way to upload Android apps, upload Espresso test-suites and start build executions. Post the build execution, the Espresso build and sessions APIs can be used to view the execution details. |
|  <b>XCUITest API</b>  | Provides a simple and flexible way to upload iOS apps, upload XCUI test-suites and start build executions. Post the build execution, the XCUI build and sessions APIs can be used to view the execution details. |
|  <b>Appium API</b>  | Allows you to upload your Android/iOS apps for Appium testing on BrowserStack. Post the session execution, the Appium build and sessions APIs can be used to view the execution details. |
|  <b>Custom Media API</b>  | API to upload media files you want to use in your tests running on the BrowserStack servers. |



<p>The APIs are organized around REST. All request and response bodies, including errors, are encoded in JSON.</p>

Our API endpoint is `https://api-cloud.browserstack.com`


# Authentication

> Authorization:

```shell
curl -u "USERNAME:ACESS_KEY"
```



<p>All requests must be made to our endpoint via HTTP. Authentication to the API needs to happen via HTTP Basic Auth. </p>

You can authenticate to our BrowserStack **App Automate** APIs by providing: <br>

| API       | Description                         |
|-----------|--------|-------------------------------------|
|  <b>USERNAME</b> | The username for your account on BrowserStack. |
|  <b>ACCESS-KEY</b>  | The access-key for your account on BrowserStack. |

You can access your credentials from [Account Settings](https://www.browserstack.com/accounts/settings) page. The credentials can also be accessed from the [App Automate dashboard](https://app-automate.browserstack.com/dashboard), when the user is signed in as shown:

![Authenticate]('images/authenticate.png')




<!---
# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete


-->
