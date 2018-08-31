# Redux

1. Install redux, we'll wanted to install react redux binding as well

```
npm i redux react-redux --save
```

2. Adding provider to entry

```js
// index.js
import { Provider } from 'react-redux'

ReactDOM.render(
    <Provider> <!-- add provider -->
        <App />
    </Provider>
, document.getElementById('root'))
```

3. Just Provider is not enough, you'll need more than that

to connect react with redux, do following

```js
// index.js
import { Provider } from 'react-redux'
import { createStore, applyMiddleware } from 'redux' // <- (1) import redux

const createStoreWithMiddleware = applyMiddleware()(createStore) // <- (2) store with middleware

ReactDOM.render(
    <Provider store={createStoreWithMiddleware()}> <!-- adding store -->
        <App />
    </Provider>
, ...)
```

4. Next, you need to add a reducer

As a convention, create a directory inside `src/`

```
--src/
    |--reducer/
         |--index.js
         |--reducer.js
```

setup a root reducer

```js
// src/reducer/index.js
import { combineReducers } from 'redux'
import reducer from './reducer'

const rootReducer = combineReducers({
    reducer,
    // anotherReducer,
    // ...
})

export default rootReducer
```

then, use this rootReducer in entry point

```js
// index.js
//...
import reducers from './reducers'

ReactDOM.render(
    <Provider store={createStoreWithMiddleware(reducer)}> <!-- passing reducer here -->
        <App />
    </Provider>
, ...)
```

> Why combineReducers/roorReducers?
> 
> It's important to note that you'll only have a single store in a Redux application. When you want to split your data handling logic, you'll use reducer composition aka combineReducers instead of many stores.

Here is a reducer

> Reducers specify how the application's state changes in response to actions sent to the store. Remember that actions only describe what happened, but don't describe how the application's state changes.

```js
// src/reducer/reducer.js

export default function(state, action) {
    // transform the state but not direct modify (mutate) it
    switch (action.type) {
        case "A":
            // return new state
            return state + "A";
            // or we can merge previous state
            // return { ...state, new_data }
        break;
        // another cases...
        default:
            return state;
    }
}
```

Related to Reducer, there is a definition called [Action](https://redux.js.org/basics/actions)

> Actions are payloads of information that send data from your application to your store. They are the only source of information for the store. You send them to the store using store.dispatch().

Basically, actions are just plain javascript object that describe how data changes.

```
--src/
    |--actions/
         |--index.js
         |--action.js
```

```js
// src/actions/action.js

export const updateAction = {
    type: "UPDATE",
    payload: "ABC"
}

export const deleteAction = {
    type: "DELETE",
    payload: 1
}

export const deleteAction2 = {
    type: "DELETE",
    payload: 2
}

// or even a function (called action creator)
export function getList() {
    return {
        type: "LIST",
        payload: [
            // data
        ]
    }
}
```

### Why action? why action creator?

```js
// action to delete product which id = 1
deleteProduct1 = {
    type: "DELETE",
    payload: 1
}

// and then, action to delete product 2
deleteProduct2 = {
    type: "DELETE",
    payload: 2
}

// and again, product 3, 4, ..., 1000

// why so that complicated, why dont we just...reuse an action as a function
function deleteProduct = id => {
    type: "DELETE",
    payload: 1
}

// that's called action creator, simple right?
```

5. Connect react with redux

Here we have a simple component

```js
// src/app.js
import React, { Component } from 'react'

class App extends Component {
    render() {
        return (
            <div>My App</div>
        )
    }
}

export default App
```

First, connect

```js
// src/app.js
import { connect } from 'react-redux' // <- import

class App extends Component {
    render() {
        // return (...)
    }
}

const mapStateToProps = (state) => { // map state to props
    return {
        data: ""
    }
}

export default connect(null, null)(App) // <- connect
```