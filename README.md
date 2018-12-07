# Redux/Context Scheduling Example

This is a small project to demonstrate the UI lifecycle of a React/Redux structure. For contrast, an alternative React Context solution has been provided.

## Redux

### Reasons to use Redux

Lean towards using Redux rather than Context when:

1. You need to do more than just avoid prop-drilling. Context was made to avoid the hassle of passing props down from one Component to another, so if that's your only use case, Context is a simpler option; however, if your needs extend beyond this, you likely need Redux.
2. Having your components be Pure Components is something you plan to do broadly. Pure components only rerender when one of their props has changed. Redux makes connected components Pure by default.
3. You need to debug complex state. The Redux DevTools extension is very impressive and can save you some headaches when strange bugs rear their heads. There are tools like [LogRocket](https://logrocket.com/) that even let you use the Redux devtools in production.
4. You need to use middleware. Redux supports adding new middleware that runs logic on every action running through the system. You can do things like spawn multiple actions with a trigger action, cancel actions altogether when they match your criteria, or spawn async actions.

### Redux Setup Process

1. Install react-redux using NPM/Yarn.
2. Import the Redux Provider component.
3. Wrap your app component in the \<Provider> component
4. Create a configureStore() function in a separate file and import into your App component file.
5. Inside your configureStore file, import {createStore, applyMiddleware, compose} from the 'redux' package, and thunk from 'redux-thunk'.
6. At your project root, create a 'reducers' folder and an index.js file.
7. Inside reducers/index.js, import {combineReducers} from 'redux'.
8. Create your first reducer file inside the reducers folder.
9. Create an 'actions' folder at the root of your application and a file named 'actiontypes.js'. This file holds a simple Javascript object with string constants that name your action types. Add some types and move back to the reducer you created.
10. Import your actiontypes object in your reducer.
11. Create a default export function in your reducer that takes two parameters, the state and an action object.
12. Create a switch statement inside your function that contains a case statement for each type of action you want this reducer to handle. 
13. To maintain immutability, each action type should return a new *copy* of the *full* Redux state. You can do this easily with an Object.assign() call that takes an empty object as its first parameter, the state as the second, and your state changes as the third.
14. The "default:" case should return the existing state.
15. Back in your 'reducers/index.js' file, import your reducer and export a default that is the result of a combineReducers() call, passing it an object containing all your imported reducers.
16. Return to the configureStore() file. Import your reducers/index.js file.
17. Create a const called initialStore and give it some initial values, matching the structure your reducer is expecting.
18. Fill your configureStore function with an initial parameter called initialState and set its default value to the initialStore variable you created.
19. Inside your function, return the result of createStore(), passing your reducers, initialState, and the result of a compose() applying the thunk middleware.
20. Return to the application \<Provider> component file, and add the "store" prop, passing it the result of a call to configureStore().
21. Lastly, in your 'actions' folder, create an action creator file that returns an object in the Standard Flux Action format, including a 'type', 'payload', and an optional 'meta' section. The 'type' should be a constant from your actiontypes.js file, and the 'payload' an object containing the information your reducer will need in order to create the next Redux state object.

### Redux Connect to Component

Now Redux is set up and running, but there are no React components connected to the store. Follow the below steps to create the first connected component.

1. Import {bindActionCreators} from 'redux', {connect} from 'react-redux', and the action creator file pertinent to your new component.




## Create-React-App Boilerplate:

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br>
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br>
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br>
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br>
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br>
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (Webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
