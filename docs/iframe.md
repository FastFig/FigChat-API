FigChat iframe embed
====================

FigChat can be integrated with other web applications through an `iframe` system with HTML markup:

```html
<iframe 
    src="https://www.fastfig.com/chat/hVUPLcIiBRyovQRzWwQzsiRWaWvRPKsX/?e=1" 
    frameborder="0" 
    allowfullscreen 
    mozallowfullscreen 
    webkitallowfullscreen>
</iframe>
```

Which results in:

<iframe src="https://www.fastfig.com/chat/hVUPLcIiBRyovQRzWwQzsiRWaWvRPKsX/?e=1" frameborder="0" width="400" height="400"></iframe>


`src` Attribute
---------------

The most important attribute of the `iframe` tag is the `src` attribute which receives a URL of form:

```
https://www.fastfig.com/chat/[ chat room name ]/?e=1
```

The chat room name is typically returned from the [New Room REST API](REST.md) or may be the name of a public chat room listed on the [FigChat website](https://www.fastfig.com/chat/).

The query string parameter `?e=1` is very important as it denotes that the chat room should be formatted for embedding.  Without it, a chat embed will appear exactly as it does [here](https://www.fastfig.com/chat/hVUPLcIiBRyovQRzWwQzsiRWaWvRPKsX).


Other Parts of the `iframe` Embed
---------------------------------

- `frameborder="0"` prevents the iframe from having an ugly default border surrounding it.
- `allowfullscreen mozallowfullscreen webkitallowfullscreen` allows rich media such as videos sent within FigChat to go full-screen when a user opts to.  Remove these if you wish for videos within FigChat to not have the capability to go full-screen.
