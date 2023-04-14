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

## NodeJS Basics

`NodeJS` relies on `V8` and `libuv`.

### `Event loop`

`Start -> Expired Timer Callbacks -> I/O Polling and Callbacks -> SetImmediate Callbacks -> Close Callbacks`,

```javascript
const fs = require("fs");

setTimeOut(() => console.log("It's timer 1."), 0);
setImmediate(() => console.log("Immediate call 1."));

fs.readFile("./example.txt", () => {
  console.log("I/O Completed.");
  setTimeOut(() => console.log("It's timer 2."), 0);
  setImmediate(() => console.log("Immediate call 2."));
});

console.log("This is from top-level code");
```

### Events

```javascript
const eventEmitter = require("events");

const emitter_example = new eventEmitter();

emitter_example.on("example_signal", (value) => {
  console.log(`The example_signal received, and value is ${value}.`);
});

emitter_example.emit("example_signal", 10);
```

### Streams

Used to process data piece by piece, without completing the whole read or write operation.

- `Readable` (We can consume data, examples are `fs`, `http`, Important events `data`, `end`, Functions are `pipe()`, `end()`)
- `Writable` (We can write data, examples are `fs`, `http`, Important events `drain`, `finish`, Functions are `write()`, `end()`)
- `Duplex` (We can both consume and write data, examples are `net` web socket, Important events `drain`, `finish`, Functions are `write()`, `end()`)
- `Transform` (Used to transform stream, examples are `zlib`)

```javascript
const readStream = fs.createReadStream("./example.txt");
readStream.on("data", (chunk) => {
  res.write(chunk);
});

readStream.on("end", () => res.end());

readStream.on("error", (err) => console.log(err));

// OR

const readStreamPipe = fs.createReadStream("./example.txt");

readStreamPipe.pipe(res);
```

## Building API

### Express

`Express` is a minimal `node.js` framework, higher level of abstraction.

```javascript
const express = require("express");

const app = express();

app.get("/", (req, res) => {
  res.status(200).send("Hello From The Server !");
});

app.get("/sendJSON", (req, res) => {
  res.status(200).json({
    message: "Success",
  });
});

const port = 3000;

app.listen(port, () => {
  console.log(`Listening at port ${port}.`);
});
```

### REST Architecture

- Separate API into logical resources
- Expose structured, resource-based URL's
- Use HTTP methods
- Send data as JSON
- Be stateless

The project is a photo selling web application,

`server.js`

```javascript
const app = require("./app");

const port = 3000;

app.listen(port, () => {
  console.log(`Listening at port ${port}.`);
});
```

`app.js`

```javascript
const express = require("express");
const morgan = require("morgan");

const photoRoute = require("./photoRoute");

const app = express();

app.use(morgan("dev"));

/* Important middleware to parse request object */
app.use(express.json());

/* Serve static files */
app.use(express.static(`${__dirname}/public`));

app.use("/api/v1/tours", photoRoute);

module.exports = app;
```

`photoRoute.js`

```javascript
const express = require("express");

const router = express.Router();

const photoController = require("./photoController");

router.route("/").get(photoController.getPhotos);

router.route("/:id").get(photoController.getPhoto);

module.exports = router;
```

`photoController.js`

```javascript
exports.getPhotos = (req, res, next) => {
  return "All Photos";
};
```

`param middleware`,

```javascript
router.param("id", (req, res, next, val) => console.log("Value is ", value));
```

### Environment Variables

For setting up `Environment Variables`, create a `config.env` file.

```bash
NODE_ENV="development" nodemon server.js
```

```javascript
const dotenv = require("dotenv");

dotenv.config({ path: "./config.env" });
```
