FigChat REST API
================

The FigChat REST API is used to create chat rooms, get chat room content, send messages to chat windows. All of the endpoints return JSON.


New Room
--------

https://www.fastfig.com/api/chat/new-room.php
`GET` or `POST`

The new-room endpoint is used to create chat rooms. 

### Query String Arguments: 
None

### Sample Output:

```javascript
{
    name: "BkohKPkUJagToOtkSCEWuTVGzRpiVqAx",
    error: false
}
```

Get Room
--------

https://www.fastfig.com/api/chat/get-room.php
`GET` or `POST`

The get-room endpoint is used to get the current content of a chat room.

### Query String Arguments:
- `room` *required* - The id of the room.

### Sample Output:

```javascript
{
    "error": false,
    "messages": [
        {
            "id": "446",
            "room": "hVUPLcIiBRyovQRzWwQzsiRWaWvRPKsX",
            "user": "YXQGKeSlEmfjmnbitNBMhiJVAKtboiXmgNTRRLcvYhFkvHtPvVCCelxEWRGlZDyg",
            "msg": {
                "caret": false,
                "type": "SeaGlass-Document",
                "content": [
                    {
                        "caret": {
                            "isStart": false,
                            "isEnd": true,
                            "isTop": true,
                            "isBottom": true
                        },
                        "type": "SeaGlass-IO-Html",
                        "content": "Hello there developer!<\/p>"
                    }
                ],
                "meta": {
                    "edited": 1395439134
                }
            },
            "time": "2014-03-21 21:58:54Z-5"
        }
    ]
}
```

### Example:

https://www.fastfig.com/api/chat/get-room.php?room=hVUPLcIiBRyovQRzWwQzsiRWaWvRPKsX



Poll
----

https://www.fastfig.com/api/chat/poll.php

Poll is a [Long Poll](http://en.wikipedia.org/wiki/Push_technology#Long_polling) API that allows your application to receive a push notification when a message comes in to a chat room.  While traditional REST endpoints return a result immediately, Long Poll APIs wait until either a new message is available or the request times out (30s or so).  Typically, if the request times out another one is sent immediately to wait for a new message.


### Query String Arguments:
- `room` *required* - The id of the room.
- `latestId` - The id of the last message received. This is used to prevent any messages from being missed between polls.


### Sample Output:

```javascript
{
    "error": false,
    "messages": [
        {
            "id": "446",
            "room": "hVUPLcIiBRyovQRzWwQzsiRWaWvRPKsX",
            "user": "YXQGKeSlEmfjmnbitNBMhiJVAKtboiXmgNTRRLcvYhFkvHtPvVCCelxEWRGlZDyg",
            "msg": {
                "caret": false,
                "type": "SeaGlass-Document",
                "content": [
                    {
                        "caret": {
                            "isStart": false,
                            "isEnd": true,
                            "isTop": true,
                            "isBottom": true
                        },
                        "type": "SeaGlass-IO-Html",
                        "content": "Hello there developer!<\/p>"
                    }
                ],
                "meta": {
                    "edited": 1395439134
                }
            },
            "time": "2014-03-21 21:58:54Z-5"
        }
    ]
}
```


### Usage Example

JavaScript with jQuery:

```javascript
var latestId = false;

(function poll() {
    $.ajax({
        url:        "https://www.fastfig.com/api/chat/poll.php",
        dataType:   "json",
        type:       "POST",
        data: {
            room:       roomId,
            latestId:   latestId
        },
        success: function(data) {
            console.log(data.messages);
            latestId = data.messages[data.messages.length - 1].id;
        },
        complete: poll,
        timeout: 30000
    });
})();
```

