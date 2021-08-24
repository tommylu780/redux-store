# useEffect
​
will run on each render of the app
​
```javascript
useEffect(() => {});
```
​
when the component is mounted
​
```javascript
useEffect(() => {}, []);
```
​
when the component is mounted and when the variable is updated
​
```javascript
useEffect(() => {}, [var])
```
​
will run on each render of the app
will run the returned function when the component is unmounted
​
```javascript
useEffect(() => {
  return () => {};
});
```
​
# useState
​
state represents the current state of the component
​
```javascript
const [state, setState] = useState("initialState");
```
​
to set state and cause a rerender, we need to use the setter function
​
```javascript
setState("newState");
```
​
to set the state from a previous value, we use the setter function with the function receiving a callback.
​
```javascript
setState((prevState) => prevState + "newStateV2");
```
​
# GraphQl
​
## Server
​
### Queries
​
when we want to fetch data without changing anything
​
### Mutations
​
when we want to mutate something
​
## client
​
- data - represents the payload from executing the query
- loading - indicates whether the query is loading
- error - was there an error
​
```javascript
const { data, loading, error } = useQuery(gql``);
```
​
- mutationFunc - is the function we call when we want to execute the mutation
- response - contains `data`, `loading` and `error` with other properties
​
```javascript
const [mutationFunc, response] = useMutation(gql``);
```
​
when we want to pass in parameters to the mutation, we pass them as an object in the variable `variables`.
​
```javascript
mutationFunc({ variables });
```
​
# JWT
​
JWT stands for json web token
It is an standard for passing data where we can set the expiry date and other features.
​
- [0] - this contains information about how the token was hashed and encrypted
- [1] - this is the payload that we encrypted to be used at a later date
- [2] - this is the verification signature
​
```javascript
const jwt =
  eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
    .eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ
    .SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c;
```
​
to create a jwt, we used `jsonwebtoken`
​
- payload - the data that you want to encrypt
- secret - a string that should not be shared that is used to later verify the token
​
```javascript
const jwt = jwt.sign(payload, secret);
```
​
to verify the token
​
```javascript
const decodedJWT = jwt.verify(payload, secret);
if (decodedJWt === null) {
  throw new Error("invalid token");
}
```
​
# useReducer
​
## Action
​
An action is a task that you want the reducer to perform when it is dispatched
​
## State
​
The state is the single source of truth for the reducer/application (if its a global context)
​
## Dispatch
​
Dispatch is how we execute an event and tell the reducer that we want the state to change
​
## Reducer
​
This is the brain behind how we manipulate the state to get the new state based on the action that was passed.
​
### Action
​
- an action is just a string that we create to depict that some work will be done and it will be triggered when the reducer receives this action type.
​
```javascript
const LOGIN = "LOGIN";
const LOGOUT = "LOGOUT";
```
​
### Dispatch
​
- when we dispatch an action, we are telling the reducer that we want to change the state.
- each action that we dispatch **MUST** contain a type.
​
```javascript
dispatch({ type: LOGIN, payload: userData });
```
​
### Reducer
​
- state - the state is an object that represents the current state of your application
- action - an action is an instruction that has to have a type and an optional payload. It tells the reducer how to manipulate the state.
​
each reducers **HAS** to have a default case where it returns just the state.
​
```javascript
function reducer(state, action) {
  switch (action.type) {
    case LOGIN: {
      return {
        ...state,
        user: action.payload,
      };
    }
    case LOGOUT: {
      return {
        ...state,
        user: null,
      };
    }
    default: {
      return state;
    }
  }
}
```
​
### useReducer
​
- reducer - the reducer function that you want this hook to use
- initialState - the initial state you want your reducer state to be
​
- state - the current state of your reducer
- dispatch - the dispatcher function used to execute actions
​
just like `useState` whenever the state changes in a reducer, it will cause a re-render.
​
```javascript
const [state, dispatch] = useReducer(reducer, initialState);
```