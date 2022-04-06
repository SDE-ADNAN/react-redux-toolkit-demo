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