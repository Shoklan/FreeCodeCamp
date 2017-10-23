# Learn You Node

## Hello World
- If you get a `process-nextick-args` error, then run:
  1. `nvm install 6.5.0`
  2. `nvm use 6.5.0`
  3. `npm install -g npm`
  4. `npm install -g learnyounode`
- To run the program use `node <program_name>.js`.
- Write output to the console using `console.log( "text" )`.
- Don't forget that javascript needs `;` at the end of lines.

## Baby Steps
- Node saves command line arguments via `process.argv`.
- This object is an array.
- The format of the array is always:
  1. Node
  2. path_to_js_file
  3. etc, elements.
- You can coerce input to Integers using:
  1. `+process.argv[]`
  2. `Number( process.argv[])`

## My First I/O
- An import or include looks like `var fs = require('fs')`.
- All synchronous calls end with `Sync`.
- To read a file, use `fs.readFileSync(<path_to_file>)`.
- This will return a *Buffer* object.
- You can convert a *Buffer* object to a string using `.toString()`.
- You can split a string in javascript using `str.split("<delim>")`.
- Don't forget to keep in mind what the returned data will look like to avoid off by one errors.

## My First Async I/O
- The Asynchronous version of a function simply removes the `Sync` from the function.
- Ex: `fs.readFileSync()` is now `fs.readFile()`.
- The syntax for callbacks looks like `function callback (err, data){}`.
- It is very important to understand the Async versions since this is the *node way*.
- See Reference below for link to reminder.
- High level path:
  1. Define a function passing the callback to display/write.
  2. Define the callback to display/write the data.
  3. Call (1) passing it (2).

## Filtered LS
- You can read files from a directory using `fs.readdir(<path>, <callback>)`.
- You can use the `path` module to assist in processing filenames and directories.
- `const path = require('path')`.
- You can extract the extension of a file using `path.extname()`.
- Note that this will return the `.`; such as `.html`.
- Placing `callback()` inside of a for loop will not interrupt nor end the loop.
- Node has a For Each function called `<list>.forEach( )` that you can put a function inside.

## Make it Modular
- To create a module, you'd simply create a new `mymodule.js` file with your functions inside it.
- To have the function exported by default, you'd assign `module.exports = <your_functions_code>`.
- To include the new function, you'd import the local file using `require('./mymodule.js')` since it's in the current directory.
- Don't forget to check for errors: `if( err ) return callback( err )`.
- The node way is to return `null, data` in the callback: `callback( null, data)`.
- This is to signify that no errors were detected.
- Don't forget to move dependencies into the module.

## HTTP Client
- Making http calls is done using the http module.
- To make a simple GET request, you use `http.get()`.
- The returned object is of type **response**.
- This is a node *Stream* object.
- These objects emit events that can be picked up on.
-  The most common event types are:
  1. data
  2. error
  3. end
- Accepting events comes in the format `response.on( "event_type", function( data ){} )`.
- The response object has a method called `setEncoding()` and will output strings when passed "utf8".
- When setting the encoding, you want to apply it to the response object **BEFORE** attempting to interact with it.
- Official Solution:
```
var http = require('http')

    http.get(process.argv[2], function (response) {
      response.setEncoding('utf8')
      response.on('data', console.log)
      response.on('error', console.error)
    }).on('error', console.error)
```
- Mine is more verbose and does not pass console.log directly.

## HTTP Collect
- You can install a node package using `npm install <package_name>`.
- There are two pre-built packages for dealing with stream data:
  1. `bl` Buffer List.
  2. `concat-stream`
- You can use `response.pipe()` which will collect all the data before invoking the callback.
- Printing the output will require you to append `.toString()` to the buffer object.
```
var http = require('http')
var bl = require('bl')

http.get(process.argv[2], function (response) {
  response.pipe(bl(function (err, data) {
    if (err) {
      return console.error(err)
    }
    data = data.toString()
    console.log(data.length)
    console.log(data)
  }))
})
```

## Juggling Async
- Managing the asynchronous calls is the important difficulty about node.
- Remember that asynchronous calls do not return input so you need to have the callback process the data.
- Each entry in the list must be a function for `async.series([], callback()).`
- You can use `setTimeout( function(), <n>)` where n is milliseconds to delay for input.
- Official Solution:
```
var http = require('http')
    var bl = require('bl')
    var results = []
    var count = 0

    function printResults () {
      for (var i = 0; i < 3; i++) {
        console.log(results[i])
      }
    }

    function httpGet (index) {
      http.get(process.argv[2 + index], function (response) {
        response.pipe(bl(function (err, data) {
          if (err) {
            return console.error(err)
          }

          results[index] = data.toString()
          count++

          if (count === 3) {
            printResults()
          }
        }))
      })
    }

    for (var i = 0; i < 3; i++) {
      httpGet(i)
    }
```

## Time Server

## HTTP File Server

## HTTP Uppercase

## HTTP JSON API Server


## Research:

## Reference:
- [Callbacks]( https://github.com/maxogden/art-of-node#callbacks )
- [bl Package](https://www.npmjs.com/package/bl)
- [async Package](https://www.npmjs.com/package/async)
