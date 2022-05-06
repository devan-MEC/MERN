# Routing

Consider the following code

```
app.get("/api/goals",(req,res)=>{
    res.send('get goals!');

app.post("/api/goals",(req,res)=>{
    res.send('set goals!');

app.put("/api/goals/:id",(req,res)=>{
    res.send(`updated goal with id: ${req.params.id}`);

app.post("/api/goals/:id",(req,res)=>{
    res.send(`deleted goal with id: ${req.params.id}`);
})
```

As not to clutter up `server.js`, it is divided into 3 parts:

- server.js

```

app.use("/api/goals", require("goalRoutes"));
```

- goalRoutes.js

```
const express = require("express");
const router = express.Router();

const {
  getGoals,
  setGoals,
  updateGoal,
  deleteGoal,
} = require("goalController");

router.get("/", getGoals);
router.post("/", setGoals);
router.put("/:id", updateGoal);
router.delete("/:id", deleteGoal);
```

- Further simplified using:

```
const express = require("express");
const router = express.Router();

const express = require("express");
const router = express.Router();
const {
  getGoals,
  setGoals,
  updateGoal,
  deleteGoal,
} = require("goalController");

router.route("/").get(getGoals).post(setGoals);
router.route("/:id").put(updateGoal).delete(deleteGoal);
```

- goalController.js

```
const getGoals = asyncHandler(async (req, res) => {
  res.send('get Goals!');
});

const setGoals = asyncHandler(async (req, res) => {
  res.send('get Goals!');
});

const updateGoal = asyncHandler(async (req, res) => {
  res.send(`updated goal with id: ${req.params.id}`);
});

const deleteGoal = asyncHandler(async (req, res) => {
  res.send(`deleted goal with id: ${req.params.id}`);
});

module.exports={getGoals};
```

Therefore, we have a file to specifically edit _where_ each route directs to(`goalRoutes.js`) and another file to specifically control _what_ is being done after a route is chosen(`goalController.js`)  
It is recommended to further divid up these files into folders of their own for further modularity
