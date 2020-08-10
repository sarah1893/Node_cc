# Event-Driven Architecture

Node is often described as having event-driven architecture. Let’s explore what that means.

In traditional imperative programming, we give the computer a series of instructions to execute in a pre-defined order. In contrast, when we write web applications, we often need to write logic to handle situations without knowing exactly when they’ll occur. For example, when programming a website, we might provide functionality for a click event without knowing when a user will trigger it. When Node was created, it applied this same concept of event-driven principles to the back-end environment.

Node provides an ``EventEmitter`` class which we can access by requiring in the ``events`` core module:

```
// Require in the 'events' core module
let events = require('events');

// Create an instance of the EventEmitter class
let myEmitter = new events.EventEmitter();
```

Each event emitter instance has an ``.on()`` method which assigns a *listener* callback function to a named event. The ``.on()`` method takes as its first argument the name of the event as a string and, as its second argument, the listener callback function.

Each event emitter instance also has an ``.emit()`` method which announces a named event has occurred. The ``.emit()`` method takes as its first argument the name of the event as a string and, as its second argument, the data that should be passed into the listener callback function.

```
let newUserListener = (data) => {
  console.log(`We have a new user: ${data}.`);
};

// Assign the newUserListener function as the listener callback for 'new user' events
myEmitter.on('new user', newUserListener)

// Emit a 'new user' event
myEmitter.emit('new user', 'Lily Pad') //newUserListener will be invoked with 'Lily Pad'
```

Let’s create an event emitter!


# Asynchronous JavaScript with Node.js

In server-side development, we often perform time-consuming tasks such as reading files or querying a database. Instead of halting the execution of our code to await these operations or using multiple threads like other back end environments, Node was designed to use an event loop like the one used in browser-based JavaScript execution. The [event-loop](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/) enables asynchronous actions to be handled in a [non-blocking](https://nodejs.org/en/docs/guides/blocking-vs-non-blocking/) way.

Node provides a number of APIs for performing asynchronous tasks which expect callback functions to be passed in as arguments. Under the hood, these APIs trigger the subscription to and emitting of events to signal the completion of the operation. When the operation completes, the callback function is added to a queue, or line, of tasks waiting for their turn to be executed. When the current stack, or list, or synchronous tasks finish executing, the operations on the queue will be performed.

This means if synchronous tasks never end, operations waiting in the event-queue would never have the chance to run. Take a look at the following example code using the asynchronous Node ``setTimeout()`` API which asynchronously executes a provided callback function after a given delay:

```javascript
let keepGoing = true;

let callback = () => {
  keepGoing = false;
};

setTimeout(callback, 1000); // Run callback after 1000ms

while(keepGoing === true) {
  console.log(`This is the song that never ends. Yes, it just goes on and on my friends. Some people started singing it, not knowing what it was, and they'll continue singing it forever just because...`)
};
```

This while-loop will continue forever! Even though the callback changing the `keepGoing` variable to ``false`` is added to the event queue after 1 second, it will never have a chance to run— the synchronous code from the loop will always fill the stack! If we wanted to avoid the infinite loop, we could replace the while-loop with an asynchronous function— for example, the Node ``setInterval()`` API.

Note: The modern way of handling asynchronous tasks is through JavaScript `Promises` (developers also favor the newer ``async...await`` syntax). If you’re not familiar with these topics, check out our lessons on them. Newer versions of Node (v8.0.0 and later) provide a collection of the traditional Node asynchronous APIs formatted for promises instead of callbacks. This can be found on ``util.promisify``. Many contemporary 3rd party libraries also favor promise-based patterns over traditional callbacks.