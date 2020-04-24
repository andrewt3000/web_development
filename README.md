# Web Development
These are notes on several web apps that I have built and maintain. It discusses the tools I am using and alternatives. It also gives example code and preferences among options within the libraries.   

The apps consists of a [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) / [react](https://reactjs.org/) /  [single page app (spa)](https://en.wikipedia.org/wiki/Single-page_application) and a [Node](https://nodejs.org) / [rest api](https://en.wikipedia.org/wiki/Representational_state_transfer) for the back end.   
The apps are targeted to desktop computers and not mobile, although in many cases the apps are [responsive](https://en.wikipedia.org/wiki/Responsive_web_design) and could be easily adapted to mobile.

Language Alternatives:  
[typescript](https://www.typescriptlang.org/) (a superset of javascript) has type checking support.  
[flow](https://flow.org/) - a javascript static type checker.  
 

### IDE, text editors
Preferred: [Visual Studio Code](https://code.visualstudio.com/), [vi](https://www.vim.org/)     
Alternative: [Atom](https://atom.io/), [emacs](https://www.gnu.org/software/emacs/)  


### Command Line
Many javascript libraries and tools use a [command line interface](https://en.wikipedia.org/wiki/Command-line_interface). [cli cheatsheet](cli.md)    
- MacOS [terminal](https://en.wikipedia.org/wiki/Terminal_(macOS)) 
- Windows [DOS](https://en.wikipedia.org/wiki/MS-DOS).  


### Source Control
Preferred: [git](https://git-scm.com/) - open source, distributed [version control](https://en.wikipedia.org/wiki/Version_control)     
[command reference](https://git-scm.com/docs)  
[git book](https://git-scm.com/book/en/v2)  

My source control current work flow is pushing to master, pushes to live production. Devs work on feature branches. When the feature is complete it is pushed to a dev branch, and they do a pull requests. Manager authorizes the push to master/live after testing.   

### Source control hosting
Preferred: [github](https://github.com/)  
Alternatives: [gitlab](https://about.gitlab.com/), [bitbucket](https://bitbucket.org/)  

### App Versioning  
Preferred: [semantic verisioning](https://semver.org/)   
I also plan to track an app version number in the package.json file and reflect that number to users to make sure they have the latest version. 

Keeping users on the latest version has been a challenge. Cache busting is built into the build process. However CRA defaults the app to be a [Service worker](https://developers.google.com/web/fundamentals/primers/service-workers/) which I believe is presenting problems. Currently users have to refresh the app, then close the browser to get the latest version.   

### Package manager
Preferred: [npm](https://www.npmjs.com/)   
Alternatives: [yarn](https://yarnpkg.com/)  

### Updating packages
I use ncu to keep javascript packages up to date on front and back end.  
```
#command show what needs to be updated
ncu 

#updates the package.json file. 
ncu -u 
```

# Front end web development

### React  
[Reactjs](https://reactjs.org/) ([docs](https://reactjs.org/docs/getting-started.html)) - A JavaScript library for building user interfaces.  
[create react app](https://github.com/facebook/create-react-app) - cli to generate new react app.  
CRA depends on react-scripts which should be [updated](https://create-react-app.dev/docs/updating-to-new-releases). We have not and do not plan to "eject"    

I generally prefer to use functional rather than class [components](https://reactjs.org/docs/components-and-props.html) and to use [state hooks](https://reactjs.org/docs/hooks-state.html) and [effect hooks](https://reactjs.org/docs/hooks-effect.html) rather than [state and lifecyle](https://reactjs.org/docs/state-and-lifecycle.html)     

Alternatives: [Angular](https://angularjs.org/), [Vue](https://vuejs.org/)  

### React componet libraries:  
Preferred:  
[antd](https://ant.design/docs/react/introduce) - Desktop oriented react ui components. It is used by several chinese companies including alibaba, tencent and Baidu.   
[styled components](https://www.styled-components.com/) - is a popular react library for styling custom components.  

Alternatives:  
- [react bootstrap](https://react-bootstrap.github.io/)  
- [material UI](https://material-ui.com/)  
- [blueprint](https://blueprintjs.com/)  
- [element](https://element.eleme.io)  
- [semantic ui](https://semantic-ui.com/)  

### State Management   
Preferred: [mobx](https://mobx.js.org/intro/overview.html) - simple, scalable, state management.  

Alternatives:  
- [redux](https://redux.js.org/) A Predictable State Container for JS Apps. Has immutable state. It has more boilerplate than mobx, [redux tradeoffs](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367).   
- [immer](https://immerjs.github.io/immer/docs/introduction) - work with immutable state in a more convenient way  

Use mobx inject when you need to access state variables(considered obsolete due to react context). Use observer to react to state variables.  
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

### Browser error logging
Using a browser error logging service such as [sentry](https://sentry.io/) helps alert to production problems.  

### Front end unit testing
Jest - test runner, assertion library, and mocking library.  
[snapshot testing](https://jestjs.io/docs/en/snapshot-testing) is a feature that I use.  
Jest expects tests to be in a folder named \_\_tests__ or to be named file_name.test.js  
```
#to run tests
npm test
```

#### Dom manipulation, and assertion libraries
- [Enzyme](https://enzymejs.github.io/enzyme/) is used for assert, manipulate, and traverse your React Components’ output. It mimicks jQuery api.  
- [react testing library](https://testing-library.com/docs/react-testing-library/intro) is an alternative to enzyme for dom manipulation and traversal. Written by Kent C. Dodds.    

### End to End Testing
- [cypress](https://www.cypress.io/)  
- [puppeteer](https://pptr.dev/) Headless Chrome Node.js API  

# Server Side
### Node  
An advantage of node for full stack developers is using the same language on front and back end.  

I prefer Express for routing. 
To get started use [Express application generator](https://expressjs.com/en/starter/generator.html)  
Guide: [Routing](https://expressjs.com/en/guide/routing.html) [Using Middleware](http://expressjs.com/en/guide/using-middleware.html)  Middleware, in the context of express, is code between receiving a request and producing a response.  
[4.X API](https://expressjs.com/en/api.html)  
Node contains objects: express, request, response and router.  
Commonly used: app.use(), router.route(), req.params, req.body    

Alternatives:  
Express is designed for server side rendering, not rest apis.  
[hapi](https://hapi.dev/) - node api that doesn't use middleware.  
[graphql](https://graphql.org/) - I chose not to use graphql because we have more full stack developers rather than a front end team and a backend team.     

Using serverless is an archticture that I am still considering and may move towards replacing express.  
[serverless](https://serverless.com/)   

### MS Sql Server
I use MS Sql Server on several projects that require a relational database.  
[tediousjs](https://github.com/tediousjs/node-mssql) MS Sql node driver.  
- [Sql Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15) - MS Windows client.  
- [SQLPro for MSSQL](https://www.macsqlclient.com/) mac client (room for improvement)  

### Mongo DB
I am using mongo db on some project due to large number of records stored.  
[Mongo node driver](https://mongodb.github.io/node-mongodb-native/contents.html)  
I am considering using [mongoose](https://mongoosejs.com/) for an ORM. One advantage is versioning system that helps resolve update conflicts.    
[Mongo Compass](https://www.mongodb.com/products/compass) - gui for mongo


## Authentication and Authorization
I prefer using [jwt](https://jwt.io/) over server side state management because it consumes less resources on the servers and it is easier to load balance accross multiple servers. 

JWT has 3 parts: header, payload, and signature. Payload contains session fields such as user name, user privileges, company_id etc. 

If the user login is successful it returns a jwt token to the client. The token is stored in localStorage and have a function to add the jtw token to all ajax requests in authorization header as Bearer {token}. The node api has [middleware](http://expressjs.com/en/guide/using-middleware.html) that filter routes. If authenticated, add info to request and call next middleware. Otherwise, api responds with 401. 

On the client side I wrap react router's Route object with logic to redirect if the user isn't logged in [Example](https://reacttraining.com/react-router/web/example/auth-workflow). I track if the user's login status in mobx. Client side authentication is for convenience, the pages without data are not secure assets.   

I considered using identity as a service providers because you don't have to store and protect sensitive information including user's passwords, and your jwt secret key.  
- [auth0](https://auth0.com/)
- [okta](https://www.okta.com/)  
- [Amazon cognito](https://aws.amazon.com/cognito/)   


# Dev Ops

### Current Deployment
Azure blob storage for images.  
Azure App Services to host the app. (node and front end)  
Database is hosted on [mongo db atlas](https://cloud.mongodb.com).  

In production, the front end is served through node. This avoids cors issues because everything is served from the same domain.  

In dev, "npm start" starts web on port 3000, and node on port 4001. There is a proxy in web package.json to port 4001 , which avoids cors issues in dev also. [See Create React app documentation](https://create-react-app.dev/docs/proxying-api-requests-in-development)   

### Under Consideration  
#### serverless architectures 
The upside to serverless is scalability. The downside is propreitary apis and lack of control of the environment. For instance, an issue I had with serverless was aws lambda was on an older version of node than what I was using.   

[Azure functions](azure_functions.md) - serverless functions use http triggers and binding to do routing.  

AWS [Cloud Formation](https://aws.amazon.com/cloudformation/) / API Gateway / lambda / Lambda authorizers.  

[vercel (formerly zeit) now](https://vercel.com/home) - Used previously.  cli (now), now.json config file, but routes default to file system layout.  
host static site and [serverless functions](https://zeit.co/docs/v2/serverless-functions/introduction/) (use now api for routing instead of express etc.).  
Integrates with github etc.    

#### Cloud agnostic Frameworks  
One solution to vendor lockin is to use another 3rd party.  
[serverless](https://serverless.com/) - cli (serverless) + yaml config file w/ routes (serverless.yml). supports aws, azure, google cloud etc.   

[Terraform](https://www.terraform.io/) - cli. teraform configuration language. infrastructure as code i.e. much larger in scope than serverless. Cloud agnostic (aws/azure/google etc.)     



