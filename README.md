# stream-render - render templates asynchronous
## Introduction
With `stream-render` you can insert information into files before you send them to the user.
The advantage of `stream-render` is that it processes your file line by line so it uses few memory and the processed lines can be send to the user immediately.
## Installation
`npm install stream-render`
## Templates
The easiest way is to create a directory called `views` in your projects folder.
Then you can create Templates in this directory.
There is no special file extension that you have to use. You can use `.html`, `.txt` and others.
## Example - Template
This is a file called `<pathToYourProject>/views/example.txt`
```
@// use ` and ` to seperate your js code from other contents.
Hello `username´,
Welcome to our site! three times hurray!

@// if you put an @ in the beginning of a line the whole line gets interpreted as js
@ for(let i = 0; i < 3; i++) {
Hurray
@ }

```
Note: You must add an empty line at the end of your file.
## Example - The Result
The file you get from your server after rendering it would look like that:
```
Hello Hans,
Welcomt to our site! three times hurray!

Hurray
Hurray
Hurray

```
## Example - Using stream-render with http-server
```
const http = require('http');
const render = require('stream-render');

const server = http.createServer((req, res) => {
  
  // our template needs some information
  const data = {
    username: 'Hans'
  };
  
  // render our example template
  render(res, 'example.txt', data);
});

server.listen(3000, function () {
  console.log(`Server running on port`, port);
});
```
## Example - Using stream-render with express
```
const app = require('express')();
const render = require('stream-render');

app.get('/example', function (req, res) {
  
  // our template needs some information
  const data = {
    username: 'Hans'
  };
  
  // render our example template
  render(res, 'example.txt', data);
});

app.listen(3000, function () {
  console.log('App listening on port 3000!');
});
```
