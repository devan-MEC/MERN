# Routing

```
app.get("/api/goals",(req,res)=>{
    res.send('get goals!');
})
```

There might be a GET,POST,PUT and DELETE request all to the same route
and it might get too cluttered if everything is put inside the server.js  
Therefore, it is compartmentalized into 3

- server.js

```
app.use("/api/goals", require("./routes/goalRoutes"));
```

- routes/goalRoutes.js

```
const {
  getGoals,
  setGoals,
  updateGoal,
  deleteGoal,
} = require("../controllers/goalController");

router.get("/", getGoals);
router.post("/", setGoals);
router.put("/:id", updateGoal);
router.delete("/:id", deleteGoal);
```

- Further simplified using:

```
const {
  getGoals,
  setGoals,
  updateGoal,
  deleteGoal,
} = require("../controllers/goalController");

router.route("/").get(getGoals).post(setGoals);
router.route("/:id").put(updateGoal).delete(deleteGoal);
```

- controllers/goalController.js (similarly the other functions. Just one is shown here)

```
const getGoals = asyncHandler(async (req, res) => {
  res.send('get Goals!');
});

module.exports={getGoals};
```
