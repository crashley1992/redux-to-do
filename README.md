# redux-to-do
Using Redux for a basic todo app
Notes are from Redux documentation: https://redux.js.org/basics/reducers


Actions
- Are Payload of infomation that send data from your application to your store.
- they are the only source of information for the store.
- you send them to the store using store.dispatch()

redux-thunk middleware - allows simple asynchronous use of dispatch

Enhancers
- you can only pass one enhancer into createStore
- to use multple enhancers you must first compose them into a single larger enhancer

REDUCERS
- reducers specify how the application's state changes in response to actions sent to the store. 
- remember that actions only desbribe what happened, but dont desbribe how the application's state changes.
- keep the data seperate from the UI state 
- reducer is a pure function that takes the previous state and an action, and returns the next state.

Never do this inside a reducer
- Mutate its arguments;
- Perform side effects like API calls and routing transitions;
- Call non-pure functions, e.g. Date.now() or Math.random().

- We don't mutate the state. We create a copy with Object.assign(). Object.assign(state, { visibilityFilter: action.filter }) is also wrong: it will mutate the first argument. 

- You must supply an empty object as the first parameter. You can also enable the object spread operator proposal to write { ...state, ...newState } instead.

- We return the previous state in the default case. It's important to return the previous state for any unknown action.

- todoApp gives todos just a slice of the state to manage, and todos knows how to update just that slice. This is called reducer composition, and it's the fundamental pattern of building Redux apps.

- All combineReducers() does is generate a function that calls your reducers with the slices of state selected according to their keys, and combines their results into a single object again. 

- combineReducers() does not create a new object if all of the reducers provided to it do not change state.

STORE
 - the store is the object that brings them together. 
 It has the following responsibilities:
 - holds the application state
 - allows access tot he state via getState()
 - allows state to be updated via dispatch(action);
 - Registers listeners via subscribe(listener);
Handles unregistering of listeners via the function returned by subscribe(listener).

It's important to note that you'll only have a single store in a Redux application. When you want to split your data handling logic, you'll use reducer composition instead of many stores.

Data Flow
- Redux architecture revolves around a strict unidirectional data flow.
- This means that all data in an application follows the same lifecycle pattern