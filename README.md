FigChat API Documentation
=========================

The FigChat API is used to integrate your application with FigChat.  It has two major components:
- An [iframe embed system](docs/iframe.md) for adding the chat client to your application.
- A [REST API](docs/REST.md) for creating and managing chat rooms.

Support for the API is available at [support@fastfig.com](mailto:support@fastfig.com).
This API is meant for testing and demonstration purposes only and is subject to change.
Chat rooms created using this API are not meant for distribution.

Usage
-----
FigChat does not have any library requirements and is entirely self contained.
Chat creation, access, and embedding are all incredibly easy in our system.

to create a chatroom make a `GET` or `POST` request to https://www.fastfig.com/api/chat/new-room.php
As of now there are no required feilds for this request and you may leave it blank.
the api will return a json string containing the variables `name` and `error`.
If nothing went wrong on our end `error` will be false, and `name` will contain the string for your new chatroom.

####Sample Output:
```javascript
{
    name: "BkohKPkUJagToOtkSCEWuTVGzRpiVqAx",
    error: false
}
```

(Note: You are responsible for keeping track of the chatroom's name.)

To access this new chatroom directly through FastFig you can go to https://www.fastfig.com/chat/`name`
Or you can embed it using an `<iframe>`.

####Sample `<iframe>`:
```html
<iframe 
    src="https://www.fastfig.com/chat/hVUPLcIiBRyovQRzWwQzsiRWaWvRPKsX/?e=1" 
    frameborder="0" 
    allowfullscreen 
    mozallowfullscreen 
    webkitallowfullscreen>
</iframe>
```

The embed has some basic construction you may choose to follow.
* Query string: including the variable `e=1` at the end of the source URL will ensure the chatroom is styled for embedding.
* Frameborder="0": some basic css to ensure the iframe doesn't have a border around it.
* Fullscreen flags: FigChat allows for rich media such as youtube videos. To make sure they have permission to go fullscreen from within an iframe you can include the `allowfullscreen`, `mozallowfullscreen`, and `webkitallowfullscreen` flags in the iframe code.

Advice
------

Some things to design for:
* All FigChat API's will require a licence key for official use. Because of this calls to these APIs should be made from a backend server rather than from frontend javascript to ensure the security of a license key.
* FastFig will not keep track of specific chats. FastFig will maintain all chatrooms until they are deleted, but is not responsible for lost room names. Therefore it is your responsibility to keep track of the names of any chatrooms you create.



Examples
--------------
- [Basic Usage](http://htmlpreview.github.io/?https://github.com/FastFig/FigChat-API/blob/master/examples/basic.html) - [source](/examples/basic.html)
- [Popup in new window](http://htmlpreview.github.io/?https://github.com/FastFig/FigChat-API/blob/master/examples/popup.html) - [source](/examples/popup.html)
- [Load via JavaScript](http://htmlpreview.github.io/?https://github.com/FastFig/FigChat-API/blob/master/examples/javascript.html) - [source](/examples/javascript.html) - This is commonly used if you wish to use FigChat as an alternative to an existing chat client.
