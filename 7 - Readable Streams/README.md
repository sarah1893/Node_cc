# Readable Streams

In the previous exercise, we practiced reading the contents of entire files into our JavaScript programs. In more realistic scenarios, data isn’t processed all at once but rather sequentially, piece by piece, in what is known as a *stream*. Streaming data is often preferable since you don’t need enough RAM to process all the data at once nor do you need to have all the data on hand to begin processing it.

One of the simplest uses of streams is reading and writing to files line-by-line. To read files line-by-line, we can use the`` .createInterface()`` method from the ``readline`` core module. ``.createInterface()`` returns an ``EventEmitter`` set up to emit ``'line'`` events:

```javascript
const readline = require('readline');
const fs = require('fs');

const myInterface = readline.createInterface({
  input: fs.createReadStream('text.txt')
});

myInterface.on('line', (fileLine) => {
  console.log(`The line read: ${fileLine}`);
});
```

Let’s walk through the above code:

- We require in the ``readline`` and ``fs`` core modules.
- We assign to ``myInterface`` the returned value from invoking ``readline.createInterface()`` with an object containing our designated ``input``.
- We set our ``input`` to ``fs.createReadStream('text.txt')`` which will create a stream from the **text.txt** file.
- Next we assign a listener callback to execute when ``line`` events are emitted. A ``'line'`` event will be emitted after each line from the file is read.
- Our listener callback will log to the console ``'The line read: [fileLine]'``, where ``[fileLine]`` is the line just read.
  
Let’s practice making a readable stream.

## Instructions

1. You’re going to create a program that reads each item off of a shopping list (located in **shoppingList.txt**) and prints it to the console. Let’s take it one step at a time.

Create a ``myInterface`` variable. Assign ``myInterface`` the value returned from invoking ``readline.createInterface()``.

You’ll want to invoke ``readline.createInterface()`` with an object with a key of ``input`` and a value of ``fs.createReadStream()``. Remember that ``fs.createReadStream()`` expects the file (as a string) from which it should read.

> **Hint**
```javascript
const myInterface = readline.createInterface({
  input: fs.createReadStream('shoppingList.txt')
});
```

2. Great work. Let’s create a listener callback function to use in the next step. Name this function ``printData``. ``printData()`` should expect to receive some ``data`` (we named our parameter data) and it should log that data to the console in the format: ``Item: [data]``, where ``[data]`` is the argument passed into the function.

**> Hint**
Here’s our ``printData()`` function looks:
```javascript
const printData = (data) => {
  console.log(`Item: ${data}`);
};
```

3. We’re nearly there! Remember that a ``'line'`` event will be emitted after each line from the file is read. Let’s assign our ``printData()`` function to execute whenever a ``'line'`` event is emitted by using myInterface‘s ``.on()`` method.

> Hint
```javascript
myInterface.on('line', printData);
```

4. Sweet! Let’s run the program in the terminal. Type **``node app.js``** in the terminal and press enter. If everything worked, each item from the shopping list should be printed to the terminal.