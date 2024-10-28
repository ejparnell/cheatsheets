# Node Cheatsheet

## Basic Commands

| Command                       | Description                                                            |
|-------------------------------|------------------------------------------------------------------------|
| `node -v`                     | Check the installed version of Node.js                                 |
| `npm -v`                      | Check the installed version of npm                                     |
| `node`                        | Open the Node.js REPL                                                  |
| `node <filename.js>`          | Run a JavaScript file with Node.js                                     |
| `npm init`                    | Initialize a new Node.js project                                       |
| `npm install <package>`       | Install a package locally                                              |
| `npm install -g <package>`    | Install a package globally                                             |
| `npm install --save <package>`| Install a package and save it to the `dependencies` in `package.json`  |
| `npm install --save-dev <package>` | Install a package and save it to the `devDependencies` in `package.json` |
| `npm start`                   | Start a Node.js application                                            |
| `npm test`                    | Run tests for a Node.js application                                    |
| `npm run <script>`            | Run a custom script defined in `package.json`                          |
| `npm list`                    | List installed packages                                                |
| `npm list -g`                 | List globally installed packages                                       |
| `npm update <package>`        | Update a package                                                       |
| `npm uninstall <package>`     | Uninstall a package                                                    |
| `npm uninstall -g <package>`  | Uninstall a global package                                             |


## CommonJS Modules

```js
// Exporting a module
module.exports = {
  key: 'value',
  func: function() {
    // Function logic here
  }
}

// Importing a module
const myModule = require('./my-module')
console.log(myModule.key) // Output: value
myModule.func() // Output: Function logic here
```

> Note: CommonJS modules are the standard for Node.js modules. There are other module systems like ES modules (ESM) that are supported in newer versions of Node.js but are not covered here.

## File System

```js
const fs = require('fs')

// Reading a file
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err
  console.log(data)
})

// Writing to a file
fs.writeFile('file.txt', 'Hello, Node.js!', (err) => {
  if (err) throw err
  console.log('File written.')
})
```

## Basic Express.js Setup w/o Router

```bash
npm install express
```

```js
const express = require('express')
const app = express()
const PORT = 3000

app.get('/', (req, res) => {
  res.send('Hello, Express!')
})

app.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}`)
})
```

## Basic Express.js Setup with Router

```bash
npm install express
```

```js
// Server file - app.js/server.js/index.js
const express = require('express')
const app = express()
const PORT = 3000

const router = require('./router')

app.use('/', router)

app.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}`)
})

// Router file - router.js
const express = require('express')
const router = express.Router()

router.get('/', (req, res) => {
  res.send('Hello, Router!')
})

module.exports = router
```

## MongoDB with Mongoose

```bash
npm install mongoose dotenv
```

```js
// Can be defined in the main server file or in a seperate database file
const dotenv = require('dotenv')
dotenv.config()
const mongoose = require('mongoose')

mongoose.connect(process.env.MONGODB_URI)

mongoose.connection.on('connected', () => {
  console.log(`Connected to MongoDB ${mongoose.connection.name}.`)
})

// Define a schema and model
const mongoose = require('mongoose')
const Schema = mongoose.Schema

const userSchema = new Schema({
  name: String,
  email: String
})

const User = mongoose.model('User', userSchema)

// Create a new user
const newUser = new User({
  name: 'Jane Doe',
  email: 'janeDoe@mail.com'
})

await newUser.save()
```

## Asynchronous JavaScript (Promises & Async/Await)

### Promises

```js
function asyncFunction() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Async Function')
    }, 2000)
  })
}

asyncFunction()
  .then((data) => {
    console.log(data) // Output: Async Function
  })
  .catch((error) => {
    console.error(error)
  })
```

### Async/Await

```js
function asyncFunction() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Async Function')
    }, 2000)
  })
}

async function fetchData() {
  try {
    const data = await asyncFunction()
    console.log(data) // Output: Async Function
  } catch (error) {
    console.error(error)
  }
}
```

## Environment Variables

```bash
npm install dotenv
```

```bash
# .env file
PORT=3000
MONGODB_URI=mongodb://localhost:27017/mydatabase
```

```js
const dotenv = require('dotenv')
dotenv.config()

const PORT = process.env.PORT
const MONGODB_URI = process.env.MONGODB_URI

console.log(`Server running at http://localhost:${PORT}`)
console.log(`Connected to MongoDB at ${MONGODB_URI}`)
```