# NPM for React

| Term | Definition |
| ---- | ---------- |
| __Node.js__ | A JavaScript runtime environment built on Chrome's V8 JavaScript engine. It allows developers to run JavaScript code outside of a web browser, enabling server-side JavaScript development. |
| __npm__ | Node Package Manager for Node.js. It is a command-line tool that helps manage dependencies (third-party libraries) and facilitates the installation, sharing, and versioning of JavaScript packages. |
| __package.json__ | A file used in Node.js projects to store metadata and configuration information about the project. It includes details such as the project name, version, dependencies, scripts, and more. |
| __Modules__ | Reusable pieces of code that can be organized into separate files. Each file is treated as a module and has its own scope for variables and functions. Modules allow for better code organization and encapsulation. |
| __Import & Export__ | JavaScript syntax used to share code between modules. The export statement is used to export variables, functions, or objects from a module, making them accessible to other modules. The import statement is used to import and use exported code from other modules. |
| __JSON__ | JavaScript Object Notation is a lightweight data format that is easy for humans to read and write and easy for machines to parse and generate. It is often used to transmit data between a server and a web application as a text format. |
| __Scripts__ | In the context of package.json, a script is a command or set of commands that can be executed via the command line using npm. Scripts are defined in the "scripts" section of the package.json file and can be used for tasks such as running tests, building the application, or performing other custom operations. |

## Creating a Node.js project

- What does `mkdir` stand for? It stands for make directory(folder)
- What does `cd` stand for? It stands for change directory(folder)

```bash
mkdir my-node-project
cd my-node-project
npm init(Intialize)
```

## Exporting a Variable

- What does the `default` keyword do? If we want to export a single value or to have a fallback value for your module, you could use a default export.

```js
export default message;
```

## Importing a Module

- The import name `importedMessage` doesn't match the export name `message` from above. Is that ok? yes, its ok because its only one component being exported, it still the smae vaule from the file.
- Does this renaming on import change the name of the export? No, it still stays the same in the home file and can be reused else where.

```js
import importedMessage from "./messages.js";
```

## Exporting & Importing Multiple Variables

- These import and export names do match, why is that? because there are multiple named varibles being transfered between components.
- Could we change them to not match? No

```js
// messages.js
export { message, anotherMessage };
import { message, anotherMessage } from "./messages.js";
```

## Renaming Imported Modules

- What are some benefits of renaming imported variables? We can solve naming conflicts in the file that we are importing to.
- What are some good conventions to follow when naming variables? Make sure the name is descriptive and unique names. They give context to what you are using them for and they avoid keywords. Avoid accessive abbreviations.

```js
import {message as hello, anotherMessage} from "./messages.js";
```

## Exporting a Function

- What's the purpose of exporting a function? To use the functionality in another component(file)
- How come we don't include the parameters in our export? becuase this would call the function and we aren't trying too do that

```js
const customMessage = (message, name) => {
  return `${message} ${name}`;
};

module.exports = { message, anotherMessage, customMessage };
```

## Importing a Function

- How do we know that `customMessage` is a function? we could go to the export file and look, we can console.log it
- Why are we passing "Nice to see you," and "Ava" to the `customMessage` function? because the function expects two parameters and needs them to be called correctly.

```js
import {
  message as hello,
  anotherMessage as goodbye,
  customMessage,
} from "./messages.js";

console.log(customMessage("Nice to see you,", "Ava"));
```

## Exporting JSON

- Why isn't there an export statement anywhere? because it exports data by default. thats its whole purpose.

```json
[
  {
    "id": "0001",
    "type": "donut",
    "name": "Cake"
  },
  {
    "id": "0002",
    "type": "donut",
    "name": "Raised"
  },
  {
    "id": "0003",
    "type": "donut",
    "name": "Old Fashioned"
  }
]
```

## Importing JSON

- What's different about importing JSON compared to other imports? We need to assert the type as json if we are using vanilla js
- Do we need to `assert` the data type for JSON in the latest version of React? No because react has webpack and webpack use json loader that deals with that.

```js
import donuts from "./donuts.json" assert { type: "json" };
```

## Create a Custom Script in `package.json`

- What benefits can you see from creating your own scripts? Error handling, increase productivity, customize tasks, etc. 

```json
// package.json
{
  "name": "my-node-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "my-script": "echo 'I just ran my own script!'"
  },
  "author": "",
  "license": "ISC"
}
```

```bash
npm run my-script
```
