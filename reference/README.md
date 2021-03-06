# Integrating redux into react

1. Install the `redux` and `react-redux` libraries
2. Import `createStore`, `Provider` and `connect`
3. Create a reducer
4. Create a store
5. Place the provider component
6. Connect your components

# Installation

Install the redux and react-redux libraries
`npm install redux`
`npm install react-redux`

Here are the most important values to be imported from the libraries:

```javascript
import { connect, Provider } from "react-redux";
import { createStore } from "redux";
```

# Reducer

- You can only have one reducer in your whole project
- It is simply a two parameter function defined by the programmer
- The first argument is the state
- The second argument is the action
- It returns a new state

### Example

```javascript
let reducer = function(state, action) {
  if (action.type === "addTodo") {
    return { todos: state.todos.concat(action.content) };
  }
  return state; // Needed because react-redux calls your reducer with an @@init action
};
```

# `createStore`

- This function is supplied by the redux library. It needs to be imported
- Only call this function once in your whole project
- It takes 3 arguments
- First argument: reducer (see above)
- Second argument: initial state
- Third argument (needed for redux devtools): `window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()`

### Example

```javascript
const store = createStore(
  function(state, action) {
    return { ...state, numActions: state.numActions + 1 };
  }, // reducer
  { todos: [] }, // initial state
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
);
```

# `Provider`

- Component supplied by the react-redux library. It needs to be imported.
- Only used once in your whole project
- Must be an ancestor of all your connected components
- Takes one attribute called `store`, the value of that attribute is the store
- The easiest place to put it is as the top level component in the index.js file
### Example

```JSX
      ReactDOM.render(<Provider store={store}>
        <App/>
      </Provider>, document.getElementById("root"))

```

# `connect`

- This function is supplied by the react-redux library. It needs to be imported.
- `connect` can take 0, 1 or 2 arguments
- The first argument is a function, typically referred to by a mapStateToProps variable
- mapStateToProps takes 1 parameter. That parameter represents the state
- The return value of mapStateToProps is an object. Each property of that object will become a prop in a component
- `connect` is a function that returns a function.

### Example

```javascript
let mapStateToProps = function(state) {
  return { actionProp: state.numActions };
}
let ConnectedDisplayTodos = connect(mapStateToProps)(SomeComponent);
```

# `dispatch`

- Any connected component has access to this.props.dispatch
- Dispatch takes one argument
- The argument represents an action
- The reducer is then called with that action and the current state

### Example

```javascript
this.props.dispatch({
  type: "deletItem",
  itemNumber: 5
});
```
