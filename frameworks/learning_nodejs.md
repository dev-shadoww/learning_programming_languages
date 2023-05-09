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

### MVC Architecture

It is composed of `Application Logic`, `Business Logic` and `Presentation Logic`.

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

## Using MongoDB with Mongoose

### Connecting with express

```javascript
const mongoose = require("mongoose");

mongoose
  .connect("https://db.io", {
    useNewUrlParser: true,
    useCreateIndex: true,
    useFindAndModify: false,
  })
  .then((connection) => {
    console.log("DB Connected.");
  })
  .catch((error) => {
    console.log("DB Is Not Connected.");
  });
```

### Creating a model

`photoModel.js`

```javascript
const photoSchema = new mongoose.schema({
  user: {
    type: String,
    required: [true, "A Photo must have a user name."],
    unique: true,
    trim: true,
  },
  rating: {
    type: Number,
    default: 4.0,
  },
  images: [String],
  createdAt: {
    type: Date,
    default: Date.now(),
  },
});

const Photo = new mongoose.model("Photo", photoSchema);

module.exports = Photo;
```

### Creating Documents

```javascript
const testPhoto = Photo.save({
  user: "user",
  rating: 4.5,
});

testPhoto
  .then((doc) => {
    console.log(doc);
  })
  .catch((err) => {
    res.status(404).json({ status: "fail", message: err });
  });
```

Another way of creating Documents,

```js
exports.createPhotoDoc = async function (req, res) {
  try {
    const newPhoto = await Photo.create(req.body);

    res.status(200).json({
      data: {
        newPhoto,
      },
      status: "success",
    });
  } catch (err) {
    res.status(404).json({ status: "fail", message: err });
  }
};
```

### Reading Documents

```js
exports.getAllPhotos = async function (req, res) {
  try {
    const photos = await Photo.find();

    res.status(200).json({
      data: {
        photos,
      },
      status: "success",
    });
  } catch (err) {
    res.status(404).json({ status: "fail", message: err });
  }
};
```

```js
exports.getPhoto = async function (req, res) {
  try {
    const photo = await Photo.findById(req.params.id);

    if (!photo) {
      return next(new AppError("Couldn't find any photo.", 404));
    }

    res.status(200).json({
      data: {
        photo,
      },
      status: "success",
    });
  } catch (err) {
    res.status(404).json({ status: "fail", message: err });
  }
};
```

### Updating Documents

```js
exports.updatePhoto = async function (req, res) {
  try {
    const photo = await Photo.findByIdAndUpdate(req.params.id, req.body, {
      new: true,
      runValidators: true,
    });

    res.status(200).json({
      data: {
        photo,
      },
      status: "success",
    });
  } catch (err) {
    res.status(404).json({ status: "fail", message: err });
  }
};
```

### Deleting Documents

```js
exports.updatePhoto = async function (req, res) {
  try {
    await Photo.findByIdAndDelete(req.params.id);

    res.status(200).json({
      data: null,
      status: "success",
    });
  } catch (err) {
    res.status(404).json({ status: "fail", message: err });
  }
};
```

### Implementing Filtering

For filtering the values are passed in the `url`, `https://api/v1/photos?resolution=720p&price=10`, `req.query` contains all the key, value pairs passed in the `url`.

```javascript
exports.getAllPhotos = async function (req, res) {
  try {
    const queryObj = { ...req.query };
    const excludedFields = ["page", "limit", "sort", "fields"];
    excludeFields.forEach((el) => delete queryObj[el]);

    const photos = await Photo.find(queryObj);

    res.status(200).json({
      data: {
        photos,
      },
      status: "success",
    });
  } catch (err) {
    res.status(404).json({ status: "fail", message: err });
  }
};
```

`https://api/v1/photos?resolution[gte]=720p&price[lte]=10`, this link includes some advanced query attributes such as `gte`, `lte`, `gt`, `lt`.

```javascript
exports.getAllPhotos = async function (req, res) {
  try {
    const queryObj = { ...req.query };
    const excludedFields = ["page", "limit", "sort", "fields"];
    excludeFields.forEach((el) => delete queryObj[el]);

    let queryStr = JSON.stringify(queryObj);
    queryStr = queryStr.replace(
      /\b(gte)|(lt)|(lte)|(gt)\b/g,
      (match) => `$${match}`
    );

    const photos = await Photo.find(JSON.parse(queryStr));

    res.status(200).json({
      data: {
        photos,
      },
      status: "success",
    });
  } catch (err) {
    res.status(404).json({ status: "fail", message: err });
  }
};
```

### Implementing Sorting

`https://api/v1/photos?sort=price,rating`,

```javascript
exports.getAllPhotos = async function (req, res) {
  try {
    const queryObj = { ...req.query };
    const excludedFields = ["page", "limit", "sort", "fields"];
    excludeFields.forEach((el) => delete queryObj[el]);

    let queryStr = JSON.stringify(queryObj);
    queryStr = queryStr.replace(
      /\b(gte)|(lt)|(lte)|(gt)\b/g,
      (match) => `$${match}`
    );

    let query = Photo.find(JSON.parse(queryStr));

    if (req.query.sort) {
      const sortQuery = req.query.sort.split(",").join(" ");
      query = query.sort(sortQuery);
    }

    const photos = await query;

    res.status(200).json({
      data: {
        photos,
      },
      status: "success",
    });
  } catch (err) {
    res.status(404).json({ status: "fail", message: err });
  }
};
```

### Implementing Field Limiting

`https://api/v1/photos?field=price,rating`,

```javascript
exports.getAllPhotos = async function (req, res) {
  try {
    const queryObj = { ...req.query };
    const excludedFields = ["page", "limit", "sort", "fields"];
    excludeFields.forEach((el) => delete queryObj[el]);

    let queryStr = JSON.stringify(queryObj);
    queryStr = queryStr.replace(
      /\b(gte)|(lt)|(lte)|(gt)\b/g,
      (match) => `$${match}`
    );

    let query = Photo.find(JSON.parse(queryStr));

    if (req.query.fields) {
      const fieldsQuery = req.query.fields.split(",").join(" ");
      query = query.select(fieldsQuery);
    } else {
      query = query.select("-__v");
    }

    const photos = await query;

    res.status(200).json({
      data: {
        photos,
      },
      status: "success",
    });
  } catch (err) {
    res.status(404).json({ status: "fail", message: err });
  }
};
```

### Implementing Pagination

`https://api/v1/photos?page=2&limit=10`,

```javascript
exports.getAllPhotos = async function (req, res) {
  try {
    const queryObj = { ...req.query };
    const excludedFields = ["page", "limit", "sort", "fields"];
    excludeFields.forEach((el) => delete queryObj[el]);

    let queryStr = JSON.stringify(queryObj);
    queryStr = queryStr.replace(
      /\b(gte)|(lt)|(lte)|(gt)\b/g,
      (match) => `$${match}`
    );

    let query = Photo.find(JSON.parse(queryStr));

    const page = req.query.page * 1 || 1;
    const limit = req.query.limit * 1 || 100;
    const skip = (page - 1) * limit;

    query = query.skip(skip).limit(limit);

    if (req.query.page) {
      const numberOfPhotos = await Photo.countDocuments();
      if (skip >= numberOfPhotos) throw new Error("Page doesn't exist.");
    }

    const photos = await query;

    res.status(200).json({
      data: {
        photos,
      },
      status: "success",
    });
  } catch (err) {
    res.status(404).json({ status: "fail", message: err });
  }
};
```

### Aggregation Pipeline Matching and Grouping

```javascript
exports.getStats = async (req, res) => {
  try {
    const stats = await Photo.aggregate([
      {
        $match: {
          ratings: { $gte: 4.5 },
        },
      },
      {
        $group: {
          _id: null,
          averageRating: { $avg: "$ratings" },
          averagePrice: { $avg: "$price" },
        },
      },
      {
        $sort: {
          averageRating: 1,
        },
      },
    ]);

    res.status(200).json({
      data: {
        stats,
      },
      status: "success",
    });
  } catch (err) {
    res.status(404).json({ status: "fail", message: err });
  }
};
```

### Aggregation Pipeline Unwinding and Projecting

```javascript
exports.getPlan = async (req, res) => {
  try {
    const stats = await Photo.aggregate([
      {
        $unwind: pricesPlans,
      },
      {
        $addField: { month: "$id" },
      },
      {
        $project: {
          _id: 0,
        },
      },
    ]);

    res.status(200).json({
      data: {
        stats,
      },
      status: "success",
    });
  } catch (err) {
    res.status(404).json({ status: "fail", message: err });
  }
};
```

### Virtual Properties

These are the properties defined on the schema which will not be persisted.

```javascript
const photoSchema = new mongoose.model({
  toJSON: { virtuals: true },
  toObject: { virtuals: true },
});

photoSchema.virtual("users").get(function () {
  return this.users;
});
```

### Document MiddleWare

`pre` hook is called before saving the document, and `post` hook is called after saving the document (that is before .save() and .create()).

```javascript
tourSchema.pre("save", function (next) {
  this.slug = slugify(this.name, { lower: true });
  next();
});

tourSchema.post("save", function (doc, next) {
  console.log(doc);
  next();
});
```

### Query MiddleWare

`pre` hook is called before a query is executed, and `post` hook is called after a query is executed (that is before .save() and .create()).

```javascript
tourSchema.pre("find", function (next) {
  next();
});

tourSchema.post("find", function (doc, next) {
  console.log(doc);
  next();
});
```

### Aggregation MiddleWare

`pre` hook is called before the aggregation, and `post` hook is called after the aggregation.

```javascript
tourSchema.pre("aggregate", function (next) {
  this.slug = slugify(this.name, { lower: true });
  next();
});

tourSchema.post("aggregate", function (doc, next) {
  console.log(doc);
  next();
});
```

### Validation

`Validator` does not works on `update`, it points to current document during creation.

```javascript
const photoSchema = new mongoose.model({
  photo: {
    type: String,
    maxlength: [20, "Must have less than or equal to 20 characters."],
    minlength: [20, "Must have more than or equal to 20 characters."],
    max: [1, "Must be above 1."],
    min: [5, "Must be below 5."],
    enum: {
      values: ["dark", "light"],
      message: "Only Dark and Light.",
    },
    rating: {
      type: Number,
      max: [1, "Must be above 1."],
      min: [5, "Must be below 5."],
      validate: {
        validator: function (val) {
          console.log("Validation");
        },
        message: "This is a custom validator. (VALUE)",
      },
    },
  },
});
```

## Error handling with express

If a route which is not handle by any other routes then this route will be activated.

```javascript
app.all(*, (req, res, next) => {
  const err = new Error(`Can't find ${req.url} on this server`)
  err.statusCode = 500;
  err.status = 'fail';
  next(err);
})
```

There are two types of errors, `Operational Errors` and `Programming Errors`,

```javascript
class AppError extends error {
  constructor(message, statusCode) {
    super(message);

    this.statusCode = statusCode;
    this.status = `${statusCode}`.startsWith("4") ? "fail" : "error";
    this.isOperational = true;

    Error.captureStackTrace(this, this.constructor);
  }
}
```

```javascript
const handleCastErrorDB = (err) => {
  const message = `Invalid ${err.path} : ${err.value}`;
  return new AppError(message, 400);
};

const handleDuplicateFieldsDB = (err) => {
  const value = err.errmsg.match(/(["'])(\\?.)*?\1/)[0];
  const message = `Duplicate field value : ${value}`;
  return new AppError(message, 400);
};

const handleValidationErrorDB = (err) => {
  const errors = Object.values(err.errors).map((el) => el.message);
  const message = `Invalid input data. ${error.join(". ")}`;
  return new AppError(message, 400);
};

const handleJsonWebTokenError = (err) => {
  const message = `Invalid Token`;
  return new AppError(message, 400);
};

const handleTokenExpiredError = (err) => {
  const message = `Please Login once again.`;
  return new AppError(message, 400);
};
```

```javascript
const sendErrorDev = (err, res) => {
  res.status(err.statusCode).json({
    status: err.status,
    error: err,
    message: err.message,
    stack: err.stack,
  });
};

const sendErrorProduction = (err, res) => {
  if (err.isOperational) {
    res.status(err.statusCode).json({
      status: err.status,
      message: err.message,
    });
  } else {
    console.error("Error : Programming error.", err);

    res.status(500).json({
      status: "error",
      message: "Something went wrong.",
    });
  }
};
```

```javascript
app.use((err, req, res, next) => {
  err.statusCode = err.statusCode || 500;
  err.status = err.status || "error";

  if (process.env.NODE_ENV == "development") {
    sendErrorDev(err, res);
  } else if (process.env.NODE_ENV == "production") {
    let error = { ...error };
    if (err.name === "CastError") error = handleCastErrorDB(error);
    if (err.code === 11000) error = handleDuplicateFieldsDB(error);
    if (err.name == "ValidationError") error = handleValidationErrorDB(error);
    if (err.name == "JsonWebTokenError") error = handleJsonWebTokenError(error);
    if (err.name == "TokenExpiredError") error = handleTokenExpiredError(error);

    sendErrorProduction(error, res);
  }
});
```

### Catching error in Async functions

```javascript
const catchAsync = (fn) => {
  return (req, res, next) => {
    fn(req, res, next).catch((err) => next(err));
  };
};
```

### Errors outside Express

```javascript
process.on("unhandledRejection", (err) => {
  console.log(err.name, err.message);
  server.close(() => {
    process.exit(1);
  });
});

process.on("uncaughtException", (err) => {
  console.log(err.name, err.message);
  server.close(() => {
    process.exit(1);
  });
});
```

## Authentication

Only works on `.save()` and `.create()`.

```javascript
const user = new mongoose.schema({
  name: String,
  password: {
    type: String,
  },
  passwordConfirm: {
    type: String,
    validate: {
      validator: function (el) {
        return el === this.password;
      },
      message: "Passwords doesn't match",
    },
  },
});
```

### Creating user

```javascript
exports.signUp = catchAsync(async (req, res, next) => {
  const newUser = await User.create(req.body);

  res.status(200).json({
    status: "success",
    data: {
      user: newUser,
    },
  });
});
```

### Working with passwords

To work with passwords install `bcryptjs` module.

```javascript
const bcrypt = require("bcrypt");

userSchema.pre("save", async function (next) {
  if (!this.isModified("password")) return next();

  this.password = await bcrypt.hash(this.password, 12);

  this.passwordConfirm = undefined;
  next();
});
```

### JSON Web Tokens

There is `Client` and `Server`, first `client` makes a request with `password` and `email`, then if it is correct then the server creates and sends a unique `JWT Token` to that particular user (which is stored in a cookie or local storage), Now the `client` sends this `JWT Token` and if it's valid then the server allows the services to that `client`.

It should work on `HTTPS` and not on `HTTP`, the `JWT Token` is composed of `header`, `Payload` and `Verified Signature`, the `header` and `Payload` are combined to create a `Verified Signature` then it sent to the `server`, next `server` creates a `Test Signature` and compares both the signatures.

Install `jsonwebtoken` module.

```javascript
const signedToken = (id) =>
  jwt.sign({ id }, process.env.JWT_SECRET, {
    expiresIn: process.env.EXPIRES_IN,
  });
```

### Logging user in

```javascript
userSchema("save", function (next) {
  if (!this.isModified("password") || this.isNew) return next();

  this.passwordChangedAt = Date.now() - 1000;
  next();
});
```

This is known as `instance method` and available to all the documents.

```javascript
userSchema.methods.correctPassword = async function (
  candidatePassword,
  userPassword
) {
  return await bcrypt.compare(candidatePassword, userPassword);
};
```

```javascript
userSchema.methods.changedPasswordAfter = async function (JWTTimeStamp) {
  if (this.passwordChangedAt) {
    return JWTTimeStamp < parseInt(this.passwordChangeAt.getTime() / 1000, 10);
  }
  return false;
};
```

```javascript
userSchema.methods.createPasswordResetToken = function () {
  const resetToken = crypto.randomBytes(32).toString("hex");

  this.passwordResetToken = crypto
    .createHash("sha256")
    .update(resetToken)
    .digest("hex");

  this.passwordResetTokenExpiresIn = Date.now() + 10 * 60 * 1000;

  return resetToken;
};
```

```javascript
exports.login = catchAsync(async (req, res, next) => {
  const { email, password } = req.body;

  if (!email || !password) {
    return next(new AppError("Please provide email or password.", 400));
  }

  const user = await user.findOne({ email }).select("password");

  if (user) {
    const correct = await user.correctPassword(password, user.password);
  }

  if (!user || !correct) {
    return next(new AppError("Incorrect Email or Password.", 401));
  }

  const token = signedToken(user._id);

  res.status(200).json({
    status: "success",
    data: {
      user: newUser,
    },
  });
});
```

### Protecting Routes

Send token using `HTTP headers`, it is `req.headers`.

`authorization Bearer Value`,

```javascript
const { promisify } = require("util");

exports.protect = catchAsync(async (req, res, next) => {
  let token;

  if (
    req.header.authorization &&
    req.header.authorization.startsWith("Bearer")
  ) {
    token = req.header.authorization.split(" ")[1];
  }

  if (!token) {
    return next(new AppError("Not logged in,", 401));
  }

  const decoded = await promisify(jwt.verify)(token, process.env.JWT_SECRET);

  const freshUser = await User.findById(decoded.id);

  if (!freshUser) {
    return next(new AppError("User doesn't exist,", 401));
  }

  if (await freshUser.changedPasswordAfter(decoded.iat)) {
    return next(new AppError("Password changed.", 401));
  }

  req.user = freshUser;
  next();
});
```

### Postman setup

```javascript
pm.environment.set("jwt", pm.response.json().token);
```

Then set the Authorization to `Bearer Token`, and token to `{{jwt}}`.

### User Roles

```javascript
exports.restrictTo = (...roles) => {
  return (req, res, next) => {
    if (!roles.include(req.user.role)) {
      return next(
        new AppError("You Don't have permission to perform this action.", 403)
      );
    }

    next();
  };
};
```

### Working with nodemailer

```javascript
const nodemailer = require("nodemailer");

const sendEmail = (options) => {
  const transporter = nodemailer.createTransporter({
    host: process.env.EMAIL_HOST,
    port: process.env.EMAIL_PORT,
    auth: {
      user: process.env.EMAIL_USER,
      pass: process.env.EMAIL_PASSWORD,
    },
  });

  const mailOptions = {
    from: "user <hello@user.io>",
    to: options.mail,
    subject: options.subject,
    text: options.message,
  };

  await transport.sendMail(mailOptions);
};
```

### Reset Password

`forgotPassword` is a `POST` method and `resetPassword` is a `PATCH` method.

```javascript
exports.forgotPassword = catchAsync(async (req, res, next) => {
  const user = await user.findOne({ email: req.body.email });

  if (!email) {
    return next(new AppError("Please provide email or password.", 404));
  }

  const resetToken = user.createPasswordResetToken();
  await user.save({
    validateBeforeSave: false,
  });

  const resetUrl = `${req.protocol}://${req.get(
    "host"
  )}/api/v1/users/resetPassword/${resetToken}`;

  const message = `Use this url : ${resetUrl}`;

  try {
    await sendEmail({
      email: user.email,
      subject: "Password reset link expires in 10 minutes",
      message,
    });

    res.status(200).json({
      status: "success",
      message: "Token sent to email.",
    });
  } catch (err) {
    user.passwordResetToken = undefined;
    user.passwordResetExpires = undefined;
    await user.save({
      validateBeforeSave: false,
    });

    return next(new AppError("Error", 500));
  }
});
```

```javascript
exports.resetPassword = catchAsync(async (req, res, next) => {
  const hashedToken = await crypto
    .createHash("sha256")
    .update(req.params.token)
    .digest("hex");

  const user = await User.findOne({
    passwordResetToken: hashedToken,
    passwordResetExpires: { $gt: Date.now() },
  });

  if (!user) {
    return next(new AppError("Token is invalid.", 400));
  }

  user.password = req.body.password;
  user.passwordConfirm = req.body.passwordConfirm;
  user.passwordResetToken = undefined;
  user.passwordResetExpires = undefined;
  await user.save();

  const token = signedToken(user._id);

  res.status(200).json({
    status: "success",
    token,
  });
});
```

### Updating Password

```javascript
exports.updatePassword = catchAsync(async (req, res, next) => {
  const user = await User.findById(req.user.id).select("+password");

  if (!user) {
    return next(new AppError("User not found.", 400));
  }

  if (user) {
    const correct = await user.correctPassword(
      req.body.passwordCurrent,
      user.password
    );
  }

  if (!user || !correct) {
    return next(new AppError("Incorrect Email or Password.", 401));
  }

  user.password = req.body.password;
  user.passwordConfirm = req.body.passwordConfirm;
  await user.save();

  const token = signedToken(user._id);

  res.status(200).json({
    status: "success",
    token,
  });
});
```

### Updating UserData

```javascript
const filterObj = (obj, ...allowedFields) => {
  Object.keys(obj).forEach((el) => {
    if (allowedFields.includes(el)) {
      newObj[el] = obj[el];
    }
  });

  return newObj;
};

exports.updateMe = catchAsync(async (req, res, next) => {
  if (req.body.password || req.body.passwordConfirm) {
    return next(new AppError("This route is not for password update.", 400));
  }

  const filteredBody = filterObj(req.body, "name", "email");
  const updateUser = await User.findByIdAndUpdate(req.user.id, filteredBody, {
    new: true,
    runValidators: true,
  });

  res.send(200).json({
    status: "success",
    data: updatedUser,
  });
});
```

### Deleting User

```javascript
userSchema.pre(/^find/, function (next) {
  this.find({ active: { $ne: false } });
  next();
});
```

```javascript
exports.deleteMe = catchAsync((req, res, next) => {
  await user.findByIdUpdate({active : false});

  res.status(204).json({
    status: 'success',
    data: null
  })
});
```

### Sending JWT via cookie

```javascript
const createSendToken = (user, statusCode, res) => {
  const token = signedToken(user._id);

  res.cookie("jwt", token, {
    expires: new Date(
      Date.now() + process.env.JWT_EXPIRES_IN * 24 * 60 * 60 * 1000
    ),
    secure: true,
    httpOnly: true,
  });

  user.password = undefined;

  res.status(statusCode).json({
    status: "success",
    data: {
      user,
    },
  });
};
```

### Some Security Practices

Install these modules `express-rate-limiter`, `helmet`, `express-mongo-sanitize`, `xss-clean`, `hpp`.

```javascript
const limiter = rateLimiter({
  max: 100,
  windowMs: 60 * 60 * 1000,
  message: "Too many requests, try again later.",
});

app.use("/api", limiter);
```

```javascript
app.use(helmet());

app.use(express.json({ limit: "10kb" }));

app.use(mongoSanitize());

app.use(xss());

app.use(hpp());
```
