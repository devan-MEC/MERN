# MERN CRUD

whip whoop

## Folder Structure

- Create a folder called `backend` inside the root folder
- install the dependencies mentioned beneath while in the root folder( i.e the package.json resides in the root folder )

## Setting up package.json

While in the root folder

```
npm init
```

Enter whatever description you need and enter server.js as entry point( as that is what we'll be using ).
Just use the default settings for everything else

## Dependencies for backend

- nodemon - Dev dependency to automatically restart server everytime changes are made
- express - something which makes everything work in the backend I guess
- mongoose - something to interact easily with mongoDB
- dotenv - something to store variables so that the code looks very cool and posh
- colors - just to display fancy ass colored messages in the terminal

```
npm i express dotenv mongoose colors
npm i -D nodemon
```

## Set up nodemon

Head over to the newly created `package.json` in the root folder
and under 'scripts', add these lines so the whole thing looks like this

```
 "scripts": {
    "start": "node backend/server.js",
    "server": "nodemon backend/server.js"
  },
```

You can start the server later using the command( P.S don't do this yet, you don't even have a `server.js` file yet )

```
npm run server
```

## Set up dotenv

create a file called `.env` in the root folder and add in these two lines for now

```
NODE_ENV=development
PORT=5000
```

- NODE_ENV is just for our reference, i.e telling the system that it's in production
- PORT is set to whichever port we want our server to run on.  
  PORT = 5000 would mean that our server runs on `http://localhost:5000` once we start it

## Set up the server

- Create a file called `server.js` inside the `backend` folder
- add these lines to import the dependencies we'll need for now

```
const express = require("express");
const app = express();
const dotenv = require("dotenv").config();
const port = process.env.PORT || 5000;
```

The first two lines are to import express and get an instance of express in 'app'  
The third lines imports and configures dotenv  
The fourth line takes the value from `PORT` stored inside `.env` and if for some reason if it fails, assigns it to 5000 directly ( which is why the || 5000 )

## server.js

Inside `server.js`, add the following lines of code

```
app.get("/helloworld",(req,res)=>{
    res.send('Yooohoooo');
})
```

This basically translates into 'If someone sends a GET request targeted at `http://localhost:5000/helloworld`, send them a response of "Yooohoooo" '  
Now to finally make the server listen to such requests on the specified port, include these lines of code in `server.js`

```
app.listen(port, () => {
  console.log(`Server started on port ${port}`);
});
```

Asks the server to listen to port (which has the value 5000 stored in our case)  
The second argument is a function which we want to run once it starts listening to said port. Here, we are just console logging a message to the terminal the server is running on.  
The final `server.js` file should look something like This

```
const express = require("express");
const app = express();
const dotenv = require("dotenv").config();
const port = process.env.PORT || 5000;

app.get("/helloworld",(req,res)=>{
    res.send('Yooohoooo');
})

app.listen(port, () => {
  console.log(`Server started on port ${port}`);
});

```

To run the server(inside root folder)

```
npm run server
```

## Check set-up

To see if everything is working properly, send a GET request to `http://localhost:5000/helloworld`  
Postman is what I use. The extension called Thunder-client inside vscode is an alternative I know.
If everything is working as expected you should get a response of 'Yooohoooo' to your sent request!
