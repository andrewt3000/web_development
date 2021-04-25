## Mobx

[mobx-react](https://mobx-react.js.org/)  
[mobx chrome extension](https://chrome.google.com/webstore/detail/mobx-developer-tools/pfgnfdagidkfgccljigdamigbcnndkod?hl=en)  

Considering: [immer](https://immerjs.github.io/immer/docs/introduction) - work with immutable state in a more convenient way. Can be used to simplify redux or mobx reducers.    

The [gist of mobx](https://mobx.js.org/intro/overview.html) is:
1. Define state and make it [observable](https://mobx.js.org/refguide/observable.html).  
2. Create a view that responds to changes in the State. (by making it a mobx-react [observer](https://mobx-react.js.org/observe-how))  
3. Modify the State  (either through direct mutation or through an [action](https://mobx.js.org/refguide/action.html))  

Best practice: Currently using mobx-react inject when you need to access state variables via props (going forward [reconsider due to changes](https://mobx-react.js.org/recipes-inject)).  
Best practice: Have considered using the decorators, but not currently using them due to not being [stable supported language feature](https://mobx.js.org/best/decorators.html).  

