## STEPS FOR USING REACT_REDUX_TOOLKIT

# 1.) install the redux/toolkit package by running this command:
    (((( npm install @reduxjs/toolkit  ))))


# 2.) install the react-redux package by running this command:
 <!-- can run only this command for installing redux toolkit and also react-redux at once -->
    (((( npm install @reduxjs/toolkit react-redux ))))


# 3.) Create a Redux Store​
Create a file named src/app/store.js. Import the configureStore API from Redux Toolkit. We'll start by creating an empty Redux store, and exporting it:

import { configureStore } from '@reduxjs/toolkit'

export const store = configureStore({
  reducer: {},
})

# 4.) Provide the Redux Store to react
Once the store is created , we can make it available to our react components by putting a React-Redux <Provider> around our 
application in src/index.js. Import the Redux store we just created, put a <Provider> around your <App> , and pass the store as a prop:
==================
index.js
====================
import React from 'react'
import ReactDOM from 'react-dom'
import './index.css'
import App from './App'
import { store } from './app/store'
import { Provider } from 'react-redux'

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)

# 5.) Create a redux State slice 

Add a new file named src/features/counter/counterSlice.js
In that file , import the createSlice Api from redux Toolkit

Creating  a slice requires a string name to identify the slice, an initial state value, and one or more reducer functions to define how the state can be updated. Once a slice is created, we can export the generated redux action creators and the reducer Function for the whole slice.

Redux require that we write all state update immutably, by making copies of data and updating the copies. However, Redux Toolkit's createSlice and createReducer APIs use Immer inside to allow us to write "mutating" update logic that becomes correct immutuable updates ..

# code Example..
features/counter/counterSlice.js
import { createSlice } from '@reduxjs/toolkit'

const initialState = {
  value: 0,
}

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      // Redux Toolkit allows us to write "mutating" logic in reducers. It
      // doesn't actually mutate the state because it uses the Immer library,
      // which detects changes to a "draft state" and produces a brand new
      // immutable state based off those changes
      state.value += 1
    },
    decrement: (state) => {
      state.value -= 1
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload
    },
  },
})

// Action creators are generated for each case reducer function
export const { increment, decrement, incrementByAmount } = counterSlice.actions

export default counterSlice.reducer

# 6.) Add Slice Reducers to the Store​
Next, we need to import the reducer function from the counter slice and add it to our store. By defining a field inside the reducer parameter, we tell the store to use this slice reducer function to handle all updates to that state.

app/store.js
import { configureStore } from '@reduxjs/toolkit'
import counterReducer from '../features/counter/counterSlice'

export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
})