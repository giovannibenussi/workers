# Your First Worker
## HTML Worker

Let's start this guide with a working example that returns some html:

```js
const html = `<!DOCTYPE html>
<body>
  <h1>Hello World</h1>
  <p>This is the content of my html</p>
</body>`

async function handleRequest(request) {
  return new Response(html, {
    headers: {
      "content-type": "text/html;charset=UTF-8",
    },
  })
}

addEventListener("fetch", event => {
  return event.respondWith(handleRequest(event.request))
})
```

This worker return an html document and you can test it [here](https://cloudflareworkers.com/?_gl=1*1usvnfh*_ga*MjEyOTExMjY2Mi4xNjMzNjAzNDMw*_gid*NTg3MzkzNjkuMTY0MDAyMDYyNA..#31ea5078600b33c95fb48c1bbb6c0457:about:blank).

Let's see what's going on piece by piece.

```js
const html = `<!DOCTYPE html>
<body>
  <h1>Hello World</h1>
  <p>This is the content of my html</p>
</body>`
```

The html variable is instantiated with a [template
literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) that returns a string.

```js
async function handleRequest(request) {
  return new Response(html, {
    headers: {
      "content-type": "text/html;charset=UTF-8",
    },
  })
}
```

`handleRequest` is an [asynchronous function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) that returns an html response with the content of the `html` variable declared previously.

Lastly, we declare an event listener to the `fetch` event and respond with a
call to our `handleRequest` function. This is common to most of the examples
we'll see.

```js
addEventListener("fetch", event => {
  return event.respondWith(handleRequest(event.request))
})
```

## JSON Worker

Now that we have a basic idea of a worker's structure, let's create a worker
that responds with some JSON. To do this, we only need to update the `handleRequest`
function so it returns some JSON and keep that `addEventListener` call without
changes.

```js
async function handleRequest(request) {
  const data = {
    hello: "world"
  }

  const json = JSON.stringify(data, null, 2)

  return new Response(json, {
    headers: {
      "content-type": "application/json;charset=UTF-8"
    }
  })
}

addEventListener("fetch", event => {
  return event.respondWith(handleRequest(event.request))
})
```

You can test this on the Workers Playground [here](https://cloudflareworkers.com/#b7be497a14d576fd64f8c4548ee5028a:https://tutorial.cloudflareworkers.com).
