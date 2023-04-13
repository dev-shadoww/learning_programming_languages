# Learning NodeJS

## Introduction to NodeJS

`NodeJS` is a javascript runtime built on google's open source V8 javascript engine.

### Reading and Writing files

```javascript
const fs = require("fs");

const textInput = fs.readFileSync("./text_example.txt", "utf-8");

const textOutput = "Text from NodeJS";

fs.writeFileSync("./text_example.txt", textOutput);
```

### Synchrounous, Asynchrounus

`Synchrounous` is Blocking, but `Asynchrounous` is non-blocking.

Non-Blocking `Asynchrounous`,

```javascript
fs.readFile(`${__dirname}/text_example.txt`, "utf-8", (err, data) => {
  console.log(data);
});

console.log("Reading file....");
```

`__dirname` points to the directory that the script is executing from.

### Creating a simple web server

```javascript
const http = require("http");

// Server
const server = http.createServer((req, res) => {
  res.end("From server.");
});

server.listen(8080, "127.0.0.1", () => {
  console.log("Listening at PORT 8080.");
});
```

### Routing and Building Simple API

```javascript
const http = require("http");

// Server

// Read file only once
const data = fs.readFileSync(`${__dirname}/file_example.txt`, "utf-8");
const productData = JSON.parse(data);

const server = http.createServer((req, res) => {
  const pathName = req.url;

  if (pathName === "/home") res.end("This is the home page.");
  else if (pathName === "/product") {
    res.writeHead(200, { "content-type": "application/json" });

    res.end(productData);
  } else {
    res.writeHead(404, {
      "Content-type": "text/html",
    });

    res.end("<h1>Page not found.</h1>");
  }
});

server.listen(8080, "127.0.0.1", () => {
  console.log("Listening at PORT 8080.");
});
```

### Creating HTML Templates

To create HTML template, first change the data in HTML with special placeholder, this will be content that is going to change dynamically.

```html
<h1>{%NAME%}</h1>
```

Then in NodeJS loop over the data and replace all the placeholder with the data.

### Parsing Variables From URL

```javascript
const url = require("url");

const server = http.createServer((req, res) => {
  const { query, pathName } = url.parse(req.url, true);
});

server.listen(8080, "127.0.0.1", () => {
  console.log("Listening at PORT 8080.");
});
```

### Modules

```javascript
module.exports = (n) => n ** 2;
```

### Packages and npm

There are two types of packages, `Dependencies` and `Dev-dependencies`.

`Dependencies` are the packages with code which we include in our code.

```bash
npm install slugify
```

`Dev-dependencies` are the one for development, for example `webpack`, `parcel` etcetera.

```bash
npm install nodemon --save-dev
```

To install a package globally pass `-g` option.`1.18.11`, `1` Major version, `18` Minor version, `11` Patch.

- `^` - Accept patches in Minor releases,
- `~` - Only accept patch releases,
- `*` - include all versions

## Back-End Development

The `Client-Server Architecture` is where a `Client` makes a request, and the `Server` responds with a response.
