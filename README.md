# Web Development
These are notes on several web apps that I have built and maintain. It discusses libraries choosen and why. It also gives example code and preferences among options within the libraries.   

The apps consists of a [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) / react /  [single page app (spa)](https://en.wikipedia.org/wiki/Single-page_application) and a Node / [rest api](https://en.wikipedia.org/wiki/Representational_state_transfer) for the back end.   
This app is targeted to desktop computers and not mobile.

I typically use IDE [Visual Studio Code](https://code.visualstudio.com/)  

I use ncu to keep javascript packages up to date.  
```
#command show what needs to be updated
ncu 

#updates the package.json file. 
ncu -u 
```

Alternatives: I have considered typescript and [flow](https://flow.org/)  

### Source Control
Source code is versioned in [git](https://git-scm.com/).  
[git reference](https://git-scm.com/docs)  
[git book](https://git-scm.com/book/en/v2)  
I am planning to do continuous integration. Pushing to master will publish.  
I also plan to track an app version number in the package.json file and reflect that number to users to make sure they have the latest version. 

Keeping users on the latest version has been a challenge. cache busting is built into the build process. However CRA defaults the app to be a [Service worker](https://developers.google.com/web/fundamentals/primers/service-workers/) which I believe is presenting problems. Currently users have to refresh the app, then close the browser to get the latest version.   

### React  
[Reactjs](https://reactjs.org/docs/getting-started.html)    
[create react app](https://github.com/facebook/create-react-app) - Used to create original react app. On this project we are using npm (rather than yarn or npx). CRA depends on react-scripts which should be updated. We have not and do not plan to "eject"    

I prefer to use functional rather than class [components](https://reactjs.org/docs/components-and-props.html). I also prefer to use [state hooks](https://reactjs.org/docs/hooks-state.html) and [effect hooks](https://reactjs.org/docs/hooks-effect.html) rather than [state and lifecyle](https://reactjs.org/docs/state-and-lifecycle.html)     

### React componet libraries:  
[antd](https://ant.design/docs/react/introduce) - desktop oriented react ui components. used by alibaba.   
[styled components](https://www.styled-components.com/) - is popular react library for styling custom components. It should be used for any custom components.   

Alternatives:  
These are alternative libraries that were considered and should be reconsidered if we need a component that is not available. 
[react bootstrap](https://react-bootstrap.github.io/)  
[material UI](https://material-ui.com/)  

### State Management   
[mobx](https://mobx.js.org/intro/overview.html) - state managment. This was chosen over [redux](https://redux.js.org/) becuase it has less boilerplate.    

Use inject when you need to access state variables. Use observer to react to state variables.  
We are not using the decorators.  

```javascript
import { inject, observer } from "mobx-react"
props.appState.cameraID
export default inject("appState")(observer(CameraSelect))
```

### React Router
[react router](https://reacttraining.com/react-router/web/guides/philosophy)  App uses BrowserRouter which uses history api.

There is a page that routes urls to react components. Use the Link object to link to urls.   
```javascript
import { BrowserRouter as Router, Route, Link } from "react-router-dom";
<Route path="/image" exact component={Image} />
<Link to="/camera">Cameras</Link>

//to read route parameters
props.match.params.myParam
```

Use the history object to redirect to a route. This comes from createBrowserHistory.  
```javascript
history.push('/myroute')
````

### Socket io
[socket.io](https://socket.io) is prefered for real time notifications to browser.  

### Browser error logging
Using a browser error logging service such as [sentry](https://sentry.io/) helps alert to production problems.  

### front end testing
Jest (bundled with create react app) is test runner, assertion library, and mocking library.  
Enzyme is used for assert, manipulate, and traverse your React Components’ output.  

## Authentication and Authorization
I prefer using [jwt](https://jwt.io/) over server side state management because it consumes resources on the servers and it is easier to load balance accross multiple servers. 

JWT has 3 parts: header, payload, and signature. Payload contains session fields such as user name, user privileges, company_id etc. 

If the user login is successful it returns a jwt token to the client. The token is stored in localStorage and have a function to add the jtw token to all ajax requests in authorization header as Bearer {token}. The node api has [middleware](http://expressjs.com/en/guide/using-middleware.html) that filter routes. If authenticated, add info to request and call next middleware. Otherwise, api responds with 401. 

On the client side I wrap react router's Route object with logic to redirect if the user isn't logged in [Example](https://reacttraining.com/react-router/web/example/auth-workflow). I track if the user's login status in mobx. Client side authentication is for convenience, the pages without data are not secure assets.   

I considered using identity as a service providers such as [auth0](https://auth0.com/), and [Amazon cognito](https://aws.amazon.com/cognito/) because you don't have to store and protect sensitive information including user's passwords, and your jwt secret key.  


### Node  
I chose node because I am a full stack developer and prefer to work in javascript.  

I prefer Express for routing.  
Guide: [Routing](https://expressjs.com/en/guide/routing.html) [Using Middleware](http://expressjs.com/en/guide/using-middleware.html)  
[4.X API](https://expressjs.com/en/api.html)  
Node contains objects: express, request, response and router.  
Commonly used: app.use(), router.route(), req.params, req.body    

Alternatives:  
[graphql](https://graphql.org/) - I chose not to use graphql because we have more full stack developers rather than a front end team and a backend team.     

Using serverless is an archticture that I am still considering and may move towards replacing express.  
[serverless](https://serverless.com/)   

### Mongo DB
I am using mongo db due to large number of records stored.  
[Mongo node driver](https://mongodb.github.io/node-mongodb-native/contents.html)  
I am considering using [mongoose](https://mongoosejs.com/) for an ORM. One advantage is versioning system that helps resolve update conflicts.    
[Mongo Compass](https://www.mongodb.com/products/compass) - gui for mongo

### Deployment
I am using Azure blob storage for images. I am considering Azure App Services to host the node app. I am considering using App services or blob storage for hosting the front end.  

A serverless option to consider is to use azure functions.

Database is hosted on mongo db.  
