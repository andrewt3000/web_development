## Redux cheatsheet

Redux is a predictable state container for JS apps.  

[The 3 principles of Redux](https://redux.js.org/introduction/three-principles) 

1. Single source of truth
The global state of your application is stored in an object tree within a single store.  
2. State is read-only  
The only way to change the state is to emit an action, an object describing what happened.  
3. Changes are made with pure functions  
To specify how the state tree is transformed by actions, you write pure reducers.



Redux is  commonly used with [Redux toolkit](https://redux-toolkit.js.org/) and [React-Redux](https://react-redux.js.org/) bindings.  
Redux typically use involves [thunks](https://github.com/reduxjs/redux-thunk#redux-thunk) or [sagas](https://redux-saga.js.org/) for [middleware](https://redux.js.org/advanced/middleware) for asynchronous calls such as fetching data.  

[redux cra template](https://github.com/reduxjs/cra-template-redux) 
```
npx create-react-app project_name --template redux  
```

[redux chrome extension](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en)  
