# Errors

> Error Example(404/422)

```shell
# The error response object for `DELETE` endpoints.
{
    "error": {
        "message": "App not found"
    }
}

# The error response object for `GET` endpoints.
{
    "message": "Session not found"
}
```

The BrowserStack App Automate APIs use the following error codes:

Error Code | Meaning
---------- | -------
401 | Unauthorized -- Your credentials are invalid.
404 | Not Found -- The requested resource could not be found.
422 | Unprocessable Entity -- Unable to process the request.
500 | Internal Server Error -- We had a problem with our server. Try again later.






