# Core Modules and Local Modules

*Modularity* is a software design technique where one program has distinct parts each providing a single piece of the overall functionality. These separate modules come together to build a cohesive whole. Modularity is essential for creating scalable programs which incorporate libraries and frameworks and separate the program’s concerns into manageable chunks. Essentially, a module is a collection of code located in a file. Instead of having an entire program located in a single file, code is organized into separate files and combined through requiring them where needed using the ``require()`` function.

To save developers from having to reinvent the wheel each time, Node has several modules included within the environment to efficiently perform common tasks. These are known as the core modules. The core modules are defined within Node.js’s source and are located in the lib/ folder. Core modules are required by passing a string with the name of the module into the ``require()`` function:

```javascript
// Require in the 'events' core module:
let events = require('events');
```

We can use the same ``require()`` function to require modules of our own creation. To handle these different tasks, the ``require()`` function includes some interesting logic “under the hood.” The ``require()`` function will first check to see if its argument is a core module, if not, it will move on to different attempts to locate it. Check out the [Node Modules documentation](https://nodejs.org/api/modules.html#modules_modules) to learn more about how ``require()`` works.

Let’s walk through the process of requiring a local module:

```javascript
// dog.js
module.exports = class Dog {

  constructor(name) {
    this.name = name;
  }

  praise() {
    return `Good dog, ${this.name}!`;
  }
};
```

Above, in the **dog.js** file, we assign the Dog class as the value of ``module.exports``. Each JavaScript file in the Node environment has a special JavaScript object called ``module.exports``. It holds everything in that file, or module, that’s available to be required into a different file.

```javascript
// app.js
let Dog = require('./dog.js');
const tadpole = new Dog('Tadpole');
console.log(tadpole.praise());
```

In our **app.js** file we assign the variable Dog to the ``module.exports`` object of our dog.js file by invoking the ``require()`` function. Unlike when we require core modules which are required in with the name of the module as a string, local modules are required by passing in the path to the module. The ``require()`` function has some other quirks, like assuming file extensions if none are provided; this means we could have written ``let Dog = require('./dog');`` in place of ``let Dog = require('./dog.js');`` in the code above, and the ``require()`` function would have still correctly located and required in **dog.js**.