# MongoDB

In MongoDB, each table is called a _Collection_

## Connecting to MongoDB Atlas Cluster

- Before establishing connection, make sure you have your ip whitelisted in the network access and you've got the credentials of a user to request access in MongoDB  
  MONGO_URI is what is defined inside `.env` and it stores the connection url. (P.S Remember to replace the connection url with the correct password and correct collection name)

##### db.js

```
const mongoose = require("mongoose");

const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGO_URI);

    console.log(`MongoDB connected: ${conn.connection.host}`.cyan.underline);
  } catch (error) {
    console.log(error);
    process.exit(1);
  }
};

module.exports = connectDB;
```

To finally establish connection, you can import `db.js` inside `server.js` like so:

##### server.js

```
const connectDB = require("db");

connectDB();
```

## Schema (Models)

- A _Collection_ is a group of documents in MongoDB(equivalent of tables in MySql)
- Each Collection can have a variety of documents
- Here's how you define a schema for a document having a single attribute called 'text'

##### goalModel.js

```
const mongoose = require("mongoose");

const goalSchema = mongoose.Schema(
  {
    text: {
      type: String,
      required: [true, "Please add a text value"],
    },
  },
  {
    timestamps: true,
  }
);

module.exports = mongoose.model("Goal", goalSchema);
```

The second parameter is simply to enable timestamps which will automatically add a createdAt and updatedAt attribute to the documents

## Using the schema

The created schema can be imported inside other files after which you can call certain mongoose methods that let you access your collection

```
const Goal = require("goalModel");

const getGoals = asyncHandler(async (req, res) => {
  const goals = await Goal.find();
  res.status(200).json(goals);
});

const setGoals = asyncHandler(async (req, res) => {
  if (!req.body.text) {
    res.status(400);
    throw new Error("Please add a text fieldaasdas");
  } else {
    const goal = await Goal.create({ text: req.body.text });
    console.log(req.body);
    res.status(200).json(goal);
  }
});

```
