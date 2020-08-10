# Filesystem

All of the data on a computer is organized and accessed through a *filesystem*. When running JavaScript code on a browser, it’s important for a script to have only limited access to a user’s filesystem. This technique of isolating some applications from others is known as *sandboxing*. Sandboxing protects users from malicious programs and invasions of privacy.

In the back-end, however, less restricted interaction with the filesystem is essential. The Node ``fs`` core module is an API for interacting with the **f**ile **s**ystem. It was modeled after the [POSIX](https://en.wikipedia.org/wiki/POSIX) standard for interacting with the filesystem.

Each method available through the ``fs`` module has a synchronous version and an asynchronous version. One method available on the ``fs`` core module is the ``.readFile()`` method which **reads** data from a provided **file**:

```javascript
const fs = require('fs');

let readDataCallback = (err, data) => {
  if (err) {
    console.log(`Something went wrong: ${err}`);
  } else {
    console.log(`Provided file contained: ${data}`);
  }
};

fs.readFile('./file.txt', 'utf-8', readDataCallback);
```

Let’s walk through the example above:

- We required in the ``fs`` core module.
- We define an error-first callback function which expects an error to be passed as the first argument and data as the second. If the error is present, the function will print ``Something went wrong: ${err}``, otherwise, it will print ``Provided file contained: ${data}``.
- We invoked the ``.readFile()`` method with three arguments:
  1. The first argument is a string that contains a path to the file **file.txt**.
  2. The second argument is a string specifying the file’s [character encoding](https://en.wikipedia.org/wiki/Character_encoding) (usually ‘utf-8’ for text files).
  3. The third argument is the callback function to be invoked when the asynchronous task of reading from the file system is complete. Node will pass the contents of **file.txt** into the provided callback as its second argument.


## Instructions

1. We’ve created a devious treasure hunt for you! Your task is to use ``fs.readFile()`` to figure out the secret word and assign that value to the ``secretWord`` variable in **app.js**. Here’s your first clue, found scratched into walls of an abandoned castle: **fileOne.txt**.

There are many ways to complete this treasure hunt! You could write one program in **app.js** to solve the puzzle or you can run **app.js** to gain new insight and then change the program based on what you’ve figured out.

If you want some direction, but aren’t quite ready to check out the hint: we suggest you use the ``fs.readFile()`` method to print the contents of **fileOne.txt**.

> Hint
We created the following error-first callback function to start:
```javascript
let readDataCallback = (err, data) => {
  if (err) {
    console.log(`Something went wrong: ${err}`);
  } else {
    console.log(`Provided file contained: ${data}`);
  }
}; 
```
Next we ran:
```javascript
fs.readFile('./fileOne.txt', 'utf-8', readDataCallback);
```
This gave us the clue that the next file was called **anotherFile.txt**, so we ran:
```javascript
fs.readFile('./anotherFile.txt', 'utf-8', readDataCallback);
```
That gave us the clue that the next file was called **finalFile.txt**, so we ran:
```javascript
fs.readFile('./finalFile.txt', 'utf-8', readDataCallback);
```
That gave us the secret word!