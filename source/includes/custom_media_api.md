# Custom Media API

To test your app, you need to upload it on BrowserStack. 
<br>
1. Upload a media file <br>
2. View recent media files <br>
3. Delete a media file

## Upload a media-file

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" 
    -X POST "https://api-cloud.browserstack.com/app-automate/upload-media" 
    -F "file=@/path/to/media/file/mediaFile.jpg" 
    -F 'data={"custom_id": "SampleMedia"}'

```

> Example Response

```json
{
    "media_url": "media://b56494b5d005c7fa7da5511c182e59803aec24",
    "custom_id": "SampleMedia",
    "shareable_id": "steve/SampleMedia"
}
```


Upload a media-file on BrowserStack. You will get an `app_url` in response, which will be used in the test scripts inside the `app` params. 


**REQUEST**

<span style="color:darkred">**POST**</span> &nbsp;&nbsp;&nbsp; `/app-automate/upload-media`

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  file <br><sub><sup>required</sup></sub> | string | The path to your media file. <br> <b>Example</b> `/path/to/media/file/mediaFile.jpg` |
|  custom_id <br><sub><sup>optional</sup></sub> | string | The identifier for your app uploads. You can upload multiple apps using the same custom id. <br> <b>Example</b>  `SampleMedia` |


<aside class="notice"> You can upload multiple media-files using the same custom_id. It can be used instead of media_url inside the `uploadMedia` parameter in build execution API.</aside>

**REQUEST**

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  media_url     | string | media_url of app uploaded on BrowserStack. <br> <b>Example</b> `media://b56494b5d005c7fa7da5511c182e59803aec24` |
|  custom_id     | string | The unique name identifier set for your app. <br> <b>Example</b> `SampleMedia` |
|  shareable_id  | string | The id which can be used by other users of your team. <br> <b>Example</b>  `steve/SampleMedia` |


<br>
<br>


## List recent media-files

> Example Request

```shell
curl -u "USERNAME:ACESS_KEY" 
    -X GET "https://api-cloud.browserstack.com/app-automate/recent_media_files"
```

> Example Response

```json
[
    {
        "media_name": "mediafile.png",
        "media_url": "media://b56494b5d005c7fa7da5511c182e59803aec24",
        "media_id": "b56494b5d005c7fa7da5511c182e59803aec24",
        "uploaded_at": "2020-05-21 19:33:18 UTC",
        "custom_id": "SampleMedia",
        "shareable_id": "steve/MyMedia"
    },
    {
        "media_name": "Numbers.png",
        "media_url": "media://7y148c75bcb98a6a72b89d1dcae6a3db9a2",
        "media_id": "7y148c75bcb98a6a72b89d1dcae6a3db9a2",
        "uploaded_at": "2020-05-21 19:35:01 UTC",
        "custom_id": "MyMedia2",
        "shareable_id": "steve/MyMedia2"
    },
    {
        "media_name": "Testing.png",
        "media_url": "media://41r49b160228088f759dcc5f213a8431425de",
        "media_id": "41r49b160228088f759dcc5f213a8431425de",
        "uploaded_at": "2020-05-26 10:42:54 UTC"
    }
]
```


 Get the details about your recent 10 media file uploads on BrowserStack.


**REQUEST**

<span style="color:darkgreen">**GET**</span> &nbsp;&nbsp;&nbsp; `/app-automate/recent_media_files`


**RESPONSE**

array[[MediaData]


<br>
<br>


## Delete a media-file

> Example Request

```shell
curl -u "USERNAME:ACCESS_KEY" 
    -X DELETE "https://api-cloud.browserstack.com/app-automate/app/delete/<app_id>"
```

> Example Response

```json
{
    "success" : true
}
```


Delete an app uploaded on BrowserStack


**REQUEST**

<span style="color:darkred">**DELETE**</span> &nbsp;&nbsp;&nbsp; `/app-automate/app/delete/<app_id>`



<aside class="notice"> Apps are deleted automatically after 30 days of upload.</aside>

<br>
<br>

## Objects: MediaData

> Object

```json
{
    "media_name": "Mediafile.png",
    "media_url": "media://c32494b5d005f8c7fa7da5511c182e59803aec24",
    "media_id": "c32494b5d005f8c7fa7da5511c182e59803aec24",
    "uploaded_at": "2020-05-21 19:33:18 UTC",
    "custom_id": "MyMedia",
    "shareable_id": "steve/MyMedia"
}
```

| Name      | Type   | Description                         |
|-----------|--------|-------------------------------------|
|  media_name     | string | Name of the media file. <br> <b>Example</b> `Mediafile.png` |
|  media_url     | string | media_url of the media file uploaded on BrowserStack. <br> <b>Example</b> `media://b56494b5d005c7fa7da5511c182e59803aec24` |
|  media_id  | string | Hashed id(bs://..) of the media uploaded on BrowserStack. <br> <b>Example</b>  `b56494b5d005c7fa7da5511c182e59803aec24` |
|  uploaded_at     | string | ID of the app uploaded on BrowserStack. <br> <b>Example</b> `2020-05-21 19:33:18 UTC` |
|  custom_id     | string | Unique name identifier set for your app in the app upload API. <br> <b>Example</b> `MyMedia` |
|  shareable_id  | string | ID which can be used by other users of your team. <br> <b>Example</b>  `steve/MyMedia` |

<br>
<br>


