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

## Make it Modular"
- To create a module, you'd simply create a new `mymodule.js` file with your functions inside it.
- To have the function exported by default, you'd assign `module.exports = <your_functions_code>`.
- To include the new function, you'd import the local file using `require('./mymodule.js')` since it's in the current directory.
- Don't forget to check for errors: `if( err ) return callback( err )`.
- The node way is to return `null, data` in the callback: `callback( null, data)`.
- This is to signify that no errors were detected.
- Don't forget to move dependencies into the module.

## HTTP Client"

## Research:

## Reference:
- [Callbacks]( https://github.com/maxogden/art-of-node#callbacks )
