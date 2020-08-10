# Accessing the Process Object

In computer science, a *process* is the instance of a computer program that is being executed. You can open Task Manager if you’re on a Windows machine or Activity Monitor from a Mac to see information about the various processes running on your computer right now. Node has a global `process` object with useful methods and information about the current process.

The ``process.env`` property is an object which stores and controls information about the environment in which the process is currently running. For example, the ``process.env`` object contains a ``PWD`` property which holds a string with the directory in which the current process is located. It can be useful to have some ``if/else`` logic in a program depending on the current environment— a web application in a development phase might perform different tasks than when it’s live to users. We could store this information on the process.env. One convention is to add a property to ``process.env`` with the key ``NODE_ENV`` and a value of either ``production`` or ``development``.

```javascript
if (process.env.NODE_ENV === 'development'){
  console.log('Testing! Testing! Does everything work?');
}
```

The ``process.memoryUsage()`` returns information on the CPU demands of the current process. It returns a property that looks similar to this:

```javascript
{ rss: 26247168,
  heapTotal: 5767168,
  heapUsed: 3573032,
  external: 8772 }
```

*Heap* can mean different things in different contexts: a heap can refer to [a specific data structure](https://en.wikipedia.org/wiki/Heap_(data_structure)), but it can also refer to the a block of [computer memory](https://en.wikipedia.org/wiki/Memory_management). ``process.memoryUsage().heapUsed`` will return a number representing how many bytes of memory the current process is using.

The ``process.argv`` property holds an array of command line values provided when the current process was initiated. The first element in the array is the absolute path to Node, which ran the process. The second element in the array is the path to the file that’s running. The following elements will be any command line arguments provided when the process was initiated. Command line arguments are separated from one another with spaces.

    
    node myProgram.js testing 
    several features
```javascript
    console.log(process.argv[3]); // Prints 'several'
```

We’ve only covered a few of the properties of the ``process`` object, so make sure to check out the [documentation on the process object](https://nodejs.org/api/process.html) to learn more about it and explore some of its other methods and properties.

Let’s get some practice using the ``process`` object!