# REDUX

Stores all your data in a single store much like how Smaug hoarded all his gold inside a single mountain dump but that's beside the point.

#### Why Redux?

- Avoids _propdrilling_ : You don't have to pass states down an endless hierarchy of components but access all the states from a single place
- Well set up redux configs apparently gives you more control over your app
- You like to cause yourself pain

### Redux terminologies

- REDUX : Complex State Management tool. Helps create a CDS(central data store)
- REDUCERS : Manages state and returns newly updated state
- ACTIONS : Parameters of REDUCERS. 2 types:
  - Unique identifier
  - Payload which also returns data
- DISPATCH : Used to send actions to update the data
