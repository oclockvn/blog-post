# Redux

1. Install redux, we'll want to install react redux binding as well

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
        data: "" // <- will become component props
    }
}

export default connect(mapStateToProps, null)(App) // <- connect
```

[React-redux api](https://github.com/reduxjs/react-redux/blob/master/docs/api.md#provider-store)

> [mapStateToProps(state, [ownProps]): stateProps] (Function): If this argument is specified, the new component will subscribe to Redux store updates. This means that any time the store is updated, mapStateToProps will be called. The results of mapStateToProps must be a plain object, which will be merged into the component’s props. If you don't want to subscribe to store updates, pass null or undefined in place of mapStateToProps.
>
> If your mapStateToProps function is declared as taking two parameters, it will be called with the store state as the first parameter and the props passed to the connected component as the second parameter, and will also be re-invoked whenever the connected component receives new props as determined by shallow equality comparisons. (The second parameter is normally referred to as ownProps by convention.)

After connected, we'll get updated state in component props

```js
// src/app.js

class App extends Component {
    render() {
        console.log(this.props); // <- latest data
        // ...
    }
}

// ...

export default connect(mapStateToProps, null)(App)
```

6. Passing actions

After connect and map state tp props, we can get all updated `state` via component `props`. So now, if we wanted to get all actions, pass the 2nd arguments in connect function

```js
// src/app.js
import * as actions from "./actions/"

class App extends Component {
    // now we can use action via props
    console.log(this.props.updateAction) // -> { type: "UPDATE", payload: "ABC" }

    render() { }
}

// ...

export default connect(mapStateToProps, actions)(App)
```

From snippet above, we imported all funtions from actions

```js
import * as actions from "./actions/"
```

what if we have like 100 actions, but wanted to import just 1 or 2. In this case, we may want to use name import like this

```js
import { updateAction, deleteAction } from "./actions/"
```

so that we don't have `actions` and `props.action_name` anymore. What will we do?

[React-redux api](https://github.com/reduxjs/react-redux/blob/master/docs/api.md#provider-store)

> [mapDispatchToProps(dispatch, [ownProps]): dispatchProps] (Object or Function): If an object is passed, each function inside it is assumed to be a Redux action creator. An object with the same function names, but with every action creator wrapped into a dispatch call so they may be invoked directly, will be merged into the component’s props.
>
> If a function is passed, it will be given dispatch as the first parameter. It’s up to you to return an object that somehow uses dispatch to bind action creators in your own way. (Tip: you may use the bindActionCreators() helper from Redux.)
>
> If your mapDispatchToProps function is declared as taking two parameters, it will be called with dispatch as the first parameter and the props passed to the connected component as the second parameter, and will be re-invoked whenever the connected component receives new props. (The second parameter is normally referred to as ownProps by convention.)
> 
> If you do not supply your own mapDispatchToProps function or object full of action creators, the default mapDispatchToProps implementation just injects dispatch into your component’s props.

Now, we use `mapDispatchToProps`

```js
// src/app.js
import { updateAction, deleteAction } from "./actions/"

class App extends Component {
    // ...
}

const mapDispatchToProps = (dispatch) => {
    return {                        // <- return an object with
        updateActionAction: () => { // <- a new function
            dispatch(updateAction)  // <- this function will dispatch action we imported from our actions
        },
        // <- many other actions
    }
}

export default connect(mapStateToProps, mapDispatchToProps)(App)
```

Then we can use new action from `props`

```js
// src/app.js

class App extends Component {
    this.props.updateActionAction() // <- use new action   
}

const mapDispatchToProps = (dispatch) => {
    return {
        updateActionAction: () => {},
    }
}

export default connect(mapStateToProps, mapDispatchToProps)(App)
```

Ok, so now all seem good. But here we face off new issue: what if we have a lot of actions, then our mapDispatchToProps's object will like a ...I don't know, mixed a lot of things! Yeah, pain in the ass.

So how to deal with this, redux ship with a handly method called [bindActionCreators](https://redux.js.org/api/bindactioncreators)

```js
// src/app.js
import { bindActionCreators } from "redux"
import { updateAction, deleteAction } from "./actions/";

class App extends Component {
    this.props.updateActionAction() // <- use new action   
}

const mapDispatchToProps = (dispatch) => {
    return bindActionCreators({
        updateAction, 
        deleteAction
    }, dispatch);
}

export default connect(mapStateToProps, mapDispatchToProps)(App)
```
