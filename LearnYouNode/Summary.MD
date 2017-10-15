# Learn You Node

## Hello World"
- If you get a `process-nextick-args` error, then run:
  1. `nvm install 6.5.0`
  2. `nvm use 6.5.0`
  3. `npm install -g npm`
  4. `npm install -g learnyounode`
- To run the program use `node <program_name>.js`.
- Write output to the console using `console.log( "text" )`.
- Don't forget that javascript needs `;` at the end of lines.

## Baby Steps"
- Node saves command line arguments via `process.argv`.
- This object is an array.
- The format of the array is always:
  1. Node
  2. path_to_js_file
  3. etc, elements.
- You can coerce input to Integers using:
  1. `+process.argv[]`
  2. `Number( process.argv[])`

## My First I/O"
- An import or include looks like `var fs = require('fs')`.
- All synchronous calls end with `Sync`.
- To read a file, use `fs.readFileSync(<path_to_file>)`.
- This will return a *Buffer* object.
- You can convert a *Buffer* object to a string using `.toString()`.
- You can split a string in javascript using `str.split("<delim>")`.
- Don't forget to keep in mind what the returned data will look like to avoid off by one errors.


## My First Async I/O"

## Filtered LS"

## Make it Modular"

## HTTP Client"
