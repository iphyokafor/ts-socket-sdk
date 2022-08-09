# ts-socket-sdk
A NodeJs and Browser SDK that allow end-users to send and receive messages through a WebSocket connection.


#### Requirements:

  - [ ] Codebase written in [TypeScript](https://www.typescriptlang.org/) and export types for TypeScript consumers
  - [ ] Provide the Node.js SDK that saves all the sent/received messages to a file (with a very _basic_ format)
  - [ ] Provide the Browser SDK that renders all the sent/received messages in a raw _unstyled_ list
  - [ ] Provide tests for the above behaviours.

##### API Examples:

> Node.js

Feel free to create the `log.txt` file to collect all the messages at whatever path you prefer or let the end-user 
to configure it:

```ts
// with sdk defined above

// inbound messages should be automatically added a log.txt file with the format `RECV:<message-content>`
sdk.on('message', (message) => { // TS infers the type of `message`
  console.log(
    'Received', 
    message.id, // Random id of your preference
    message.content, // String or JSON object
    message.sentAt, // Message sent at
  )
})

// `send()` should append a line to a `log.txt` file with the format `SEND:<message-content>`
sdk.send({
  foo: 'bar'
})

sdk.disconnect()
```

> Browser.js

Feel free to append/create the list (`<ul>`) at the `body` of the page or allow the end-user to configure it:

```ts
// with sdk defined above

/**
 * inbound messages should be automatically appended to a list 
 * in the body with the format `RECV:<message-content>`
 */
sdk.on('message', (message) => { // TS infers the type of `message`
  console.log(
    'Received', 
    message.id, // Random id of your preference
    message.content, // String or JSON object
    message.sentAt, // Message sent at
  )
})

// 
/**
 * `send()` should append an item to the list in the body 
 * with the format `SEND:<message-content>`
 */
sdk.send({
  foo: 'bar'
})

sdk.disconnect()
```

##### Installation

* To install packages, run

`npm install`

* To build the NodeJs SDK, run

`npm run build`

* To start the server, run

`npm run dev`

* To build the browser SDK, run

`npm run build-prod`

        This command generates a `dist/browser` folder where the browser sdk is complied to, in `bundle.js` file. The `bundle.js` is what will be linked to the html file on the browser. See example in "Testing the SDKs below 👇"

##### Testing the SDKS

Carry out a simple test by creating a demo project with a basic html file linked with a javascript file, like so:

> index.html
```js

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Browser SDK Test</title>
</head>
<body>
</body>

<script src="index.js"></script> 
</html>
```

> index.js

```js

// copy the content of bundle.js file and replace here in index.js

```