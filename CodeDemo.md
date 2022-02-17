# Code Demo

## Setting Up the Project

1- Initialize a new Node.js project.

```bash
npm init
```

You have to fill the requested information to your requirements, or you can use the default settings by adding the -y flag to the same command:

```bash
npm init -y
```

A project will be created with a package.json file.

```bash
{
  "name": "demo",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.2"
  }
}
```

2- Install Express.

```bash
npm install –save express
```

A new file called package-lock.json is created, alongside a node_modules directory. The file will keep track of your dependencies.

<br>

## Creating Endpoints

1- Create a file called app.js

2- Import the Express framework within it:

```bash
const express = require("express");
```

3- Instantiate the Express app:

```bash
const app = express();
```

4- Set the port:

```bash
const port = process.env.PORT || 3000;
```

5- Create GET endpoint that returns the message “Hello World” and rendered in the browser and displayed on the console:

```bash
app.get("/", (req, res) => {
  res.send("Hello World!");
});
```

6- Call app.listen()

```bash
app.listen(port, () =>
  console.log(`Demo app listening on port ${port}!`)
);
```

7- Run the application and check it on it browser:

```bash
node app.js
```

8- Install Nodemon

```bash
npm i –g nodemon
```

After that you can use the command nodeman to run your app:

```bash
nodemon app.js
```

9- Create GET endpoint that returns list of objects:

```bash
let cakes = [
    {id: 1, "flavor":"Vanilla"},
    {id: 2, "flavor":"Chocolate"},
    {id: 3, "flavor":"Red Velvet"}
]

app.get("/api/cakes", (req, res) => {
  res.send(cakes);
});
```

10- Create GET endpoint that returns certain object:

```bash
app.get("/api/cakes/:id", (req, res) => {
    const cake = cakes.find((cake) => cake.id === parseInt(req.params.id));

    if (!course) res.status(404).send("Cake with given ID is not found");
    res.send(cake);
});
```

11- Create POST request to add new cake object:

```bash
app.post("api/cakes", (req, res) => {
  const cake = {
    id: cakes.length + 1,
    flavor: req.body.flavor,
  };
  cakes.push(cake);
  res.send(cake);
});
```

In order to use the posted request data, parse JSON object using:

```bash
app.use(express.json());
```

12- Add input validation in previous post method:

```bash
  if(!req.body.flavor || req.body.flavor.length < 3) return res.status(400).send("Name is required & should be minimum 3 characters")
```

13- Install joi node package for better input validation:

```bash
npm i joi
```

15- Import joi:

```bash
const Joi = require("joi");
```

14- Replace the previous input validation line:

```bash
const schema = Joi.object({
    flavor: Joi.string().min(3).required(),
});

const result = schema.validate(req.body);

if (result.error)
    return res.status(400).send(result.error.details[0].message);

```
