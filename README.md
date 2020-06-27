# Web Development
These are notes for building web apps. I consult this document when starting a new app and maintaining existing apps. It list preferred tools/frameworks, and alternatives plus opinions about best practices and trade offs.   

What stack should I choose?  
Prefered: [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) / [react](https://reactjs.org/) /  [single page app (spa)](https://en.wikipedia.org/wiki/Single-page_application) and a [Node](https://nodejs.org) / [rest api](https://en.wikipedia.org/wiki/Representational_state_transfer) for the back end. I have used mongodb and sql server on most recent projects.    


Language Alternatives:  
[typescript](https://www.typescriptlang.org/) (a superset of javascript) has type checking support.  
[flow](https://flow.org/) - a javascript static type checker.  
 

### IDE, text editors
Preferred: [Visual Studio Code](https://code.visualstudio.com/), [vi](https://www.vim.org/)     
VS Code has support for [emmet](https://emmet.io/) in [jsx](https://stackoverflow.com/questions/56311467/configure-emmet-for-jsx-in-vscode) and [code snippets](https://code.visualstudio.com/docs/editor/userdefinedsnippets)    

Alternative: [Atom](https://atom.io/), [emacs](https://www.gnu.org/software/emacs/)  

### Coding standards
[prettier](https://prettier.io/) code formatter  
[eslint](https://eslint.org/) code linter   

### Security
[OWASP Top 10 Web Application Security Risks](https://owasp.org/www-project-top-ten/?gclid=CjwKCAjwkun1BRAIEiwA2mJRWbtTVQAVFpjgH-7mVohQ9xsPWonwgg_fRQdbR6tXf764TQmWuqke_hoCe_4QAvD_BwE)  

### Source Control
Preferred: [git](https://git-scm.com/) ([command ref](https://git-scm.com/docs)  ) - open source, distributed [version control](https://en.wikipedia.org/wiki/Version_control)     
[git book](https://git-scm.com/book/en/v2)  

Alternative: git obsoletes other open source vcs such as rcs, cvs, and subversion.  

### Source control hosting
Preferred: [github](https://github.com/)  
Alternatives: [gitlab](https://about.gitlab.com/), [bitbucket](https://bitbucket.org/)  

### Version control workflow
Version control work flow is a function of the size and organization of your team as well as the stage of your project. If you are working alone on a project that hasn't been deployed, I would probably just push to master.  

This is a reasonable work flow with multiple developers and an architects where the project is live.    
- Devs work on feature branches. 
- When the feature is complete devs merged and push to a dev branch, and they do a PR ([pull requests](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests)) 
- Architect/manager tests, inspects and approves the PR.   
- Pushing to master automatically deploys to production. 

This can get much more complicated, especially if you have testing team.  

### App Versioning  
Preferred: [semantic verisioning](https://semver.org/)   
I also plan to track an app version number in the package.json file and reflect that number to users to make sure they have the latest version. 

How do I keep users on the most recent version? Currently, on some apps, users have to refresh the app, then close the browser to get the latest version.   
Webpack Cache busting should help users get the latest version.  
CRA 2 defaults apps to not be [Service workers](https://developers.google.com/web/fundamentals/primers/service-workers/) which may be related to problems updating apps in the past. 

### Package manager
Preferred: [npm](https://www.npmjs.com/)  - npm is a cli package manager and task runner. npm hosts a public package repository.    
Alternatives: [yarn](https://yarnpkg.com/)  

### Updating packages
Best practice: Periodically (weekly) update javascript packages on front and back end. This is important for security reasons, but can challenging when libraries change and break your project. After upgrading run tests.    
```
#command show what needs to be updated
ncu 

#updates the package.json file. 
ncu -u 
```

# Front end web development

### React  
[Reactjs](https://reactjs.org/) ([src](https://github.com/facebook/react)) ([docs](https://reactjs.org/docs/getting-started.html)) - A JavaScript library for building user interfaces.  
[chrome extension](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)  
[create react app](https://create-react-app.dev/) ([src](https://github.com/facebook/create-react-app)) ([docs](https://create-react-app.dev/docs/getting-started)) - cli to generate new react app. CRA configures [webpack](https://webpack.js.org/), a js module bundler.   
CRA depends on react-scripts which should be [updated](https://create-react-app.dev/docs/updating-to-new-releases). We have not and do not plan to [eject](https://create-react-app.dev/docs/available-scripts#npm-run-eject)      

Preference: I generally prefer to use functional rather than class [components](https://reactjs.org/docs/components-and-props.html) and to use [state hooks](https://reactjs.org/docs/hooks-state.html) and [effect hooks](https://reactjs.org/docs/hooks-effect.html) rather than [state and lifecyle](https://reactjs.org/docs/state-and-lifecycle.html)     

Alternatives: [Angular](https://angularjs.org/), [Vue](https://vuejs.org/) ([vuex](https://vuex.vuejs.org/) [nuxt](https://nuxtjs.org/))   

### React component libraries:  
Most of my apps are targeted to desktop computers and not mobile, although they are mostly [responsive](https://en.wikipedia.org/wiki/Responsive_web_design).  

Preferred:  
[antd](https://ant.design/docs/react/introduce) - Desktop oriented react ui components. It is used by several chinese companies including alibaba, tencent and Baidu.   

Alternatives:  
- [react bootstrap](https://react-bootstrap.github.io/) - created by twitter.   
- [material UI](https://material-ui.com/) - created by google  
- [blueprint](https://blueprintjs.com/)  
- [element](https://element.eleme.io)  
- [semantic ui](https://semantic-ui.com/)  

### Custom styling
I typically use [standard](https://www.w3.org/Style/CSS/Overview.en.html)  [css](https://developer.mozilla.org/en-US/docs/Web/CSS). I prefer using [css grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout) for layout. Typically in a configuration such as [holy grail layout](https://alligator.io/css/css-grid-holy-grail-layout/). I prefer [flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox) for laying out sections.    
Alternatives:  
[styled components](https://www.styled-components.com/) - is a popular react library for styling custom components.  


### State Management   
Preferred: [mobx](https://mobx.js.org/intro/overview.html) - simple, scalable, state management.  
[mobx-react](https://mobx-react.js.org/)  
[mobx chrome extension](https://chrome.google.com/webstore/detail/mobx-developer-tools/pfgnfdagidkfgccljigdamigbcnndkod?hl=en)  

Alternatives:  
- [redux](https://redux.js.org/) is a predictable state container for JS Apps. Has immutable state. It has more boilerplate than mobx, [redux tradeoffs](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367). [See my redux cheat sheet](redux.md)

Considering: [immer](https://immerjs.github.io/immer/docs/introduction) - work with immutable state in a more convenient way. Can be used to simplify redux or mobx reducers.    

The [gist of mobx](https://mobx.js.org/intro/overview.html) is:
1. Define state and make it [observable](https://mobx.js.org/refguide/observable.html).  
2. Create a view that responds to changes in the State. (by making it a mobx-react [observer](https://mobx-react.js.org/observe-how))  
3. Modify the State  (either through direct mutation or through an [action](https://mobx.js.org/refguide/action.html))  

Best practice: Currently using mobx-react inject when you need to access state variables via props (going forward [reconsider due to changes](https://mobx-react.js.org/recipes-inject)).  
Best practice: Have considered using the decorators, but not currently using them due to not being [stable supported language feature](https://mobx.js.org/best/decorators.html).  

### React Router
[react router](https://reacttraining.com/react-router/web/guides/philosophy) is a declarative react routing framework.
React router supports [nested](https://reacttraining.com/react-router/web/example/nesting) routing.   
React router supports a DOM [history](https://reacttraining.com/react-router/web/api/history) which enables the browser back button even though it's used in single page applications.  

Use the history object to redirect to a route.  
```javascript
history.push('/myroute')
````
### Data fetching
[fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API#Concepts_and_usage) is a web api (natively supported in more recent browsers).  
best practice: If supporting older browsers use a [polyfill](https://developer.mozilla.org/en-US/docs/Glossary/Polyfill) such as [isomorphic-fetch](https://www.npmjs.com/package/isomorphic-fetch) or [fetch](https://github.com/github/fetch).  

alternative: [axios](https://github.com/axios/axios)  

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
[node](https://nodejs.org) - javascript runtime built on chrome v8 javascript engine. Node is frequently run as an [http server](https://nodejs.org/en/docs/guides/getting-started-guide/).     
[nvm node version manager](https://github.com/nvm-sh/nvm) - tool to switch versions of node.  

[Express](https://expressjs.com/) node library for routing http requests.  
[Express application generator](https://expressjs.com/en/starter/generator.html) - tool to generate node express   
Guide: [Routing](https://expressjs.com/en/guide/routing.html) [Using Middleware](http://expressjs.com/en/guide/using-middleware.html)  Middleware, in the context of express, is code between receiving a request and producing a response.  
[4.X API](https://expressjs.com/en/api.html)  
Node contains objects: express, request, response and router.  
Commonly used: app.use(), router.route(), req.params, req.body    

Alternatives server APIs:  
- [hapi](https://hapi.dev/) - node rest api that doesn't use middleware. Express was originally designed for server side rendering, not rest apis.    

- [graphql](https://graphql.org/) - is an alternative to rest apis. GraphQL is a specification for a typed query language similar to sql and runtime which incluces a client (eg. relay, apollo) and server. [Apollo](https://www.apollographql.com/) is a popular graphql implementation. [Relay](https://relay.dev/) is a popular graphql client.     
- [serverless](https://serverless.com/) is a framework that can route to serverless cloud functions such as AWS lambda. Serverless cloud functions can be implemented in a variety of languages.   
- [ruby on rails](https://rubyonrails.org/) - ror has support for [rest apis](https://guides.rubyonrails.org/api_app.html)   

# Databases
There are 2 classes of databases: relational (which typically use SQL) and NoSql which include Wide column stores, document stores, key-value stores, and graph databases.  

Best practice for relational databases: [database normalization](https://en.wikipedia.org/wiki/Database_normalization)  

### MS Sql Server
I use MS Sql Server on several projects are suited to relational databases.   
[tediousjs](https://github.com/tediousjs/node-mssql) MS Sql node driver.  
- [Sql Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15) - MS Windows client.  
- [SQLPro for MSSQL](https://www.macsqlclient.com/) mac client (room for improvement)  
- [Red Gate Sql Compare](https://www.red-gate.com/products/sql-development/sql-compare/) tool for migrating schema to production environments.   

### Mongo DB
I am using mongo db on some project due to large number of records stored.  
[Mongo node driver](https://mongodb.github.io/node-mongodb-native/contents.html)  
I am considering using [mongoose](https://mongoosejs.com/) for an ORM. One advantage is versioning system that helps resolve update conflicts.    
[Mongo Compass](https://www.mongodb.com/products/compass) - gui for mongo

# Application Logic

### Authentication and Authorization
For user authentication and authorization of the rest api I typically use a [jwt](https://jwt.io/) (JSON web token), an open standard ([RFC 7519](https://tools.ietf.org/html/rfc7519)).  

JWT has 3 parts: header, payload, and signature.  

Here is how I typicaly use jwt tokens to authenticate each rest api call. 
- If the user login is successful (user submits valid username and password) the server signs and returns a jwt token to the client. User authorization claims such as user id or group id are encrypted in the token payload.   
- On the client, store the token in sessionStorage or localStorage so the single page app data doesn't lose authtenticaion information on a user's browser refresh. sessionStorage is chosen when you want logins to persist over multiple browser sessions.  
- On the client side wrap react router's Route object with logic to redirect if the user isn't logged in [Example](https://reacttraining.com/react-router/web/example/auth-workflow). The user's login status, user name, etc. can be stored in a global store. Client side authentication is for convenience, the pages without data are typically not secure assets. Also if the store is empty check localStorage or sessionStorage to restore login infomation after a user refresh.      
- On the client, authenticated api calls are sent through a library function to add the jwt token to all ajax requests in the authorization header using Bearer {token} scheme. 
- The node api has [middleware](http://expressjs.com/en/guide/using-middleware.html) that filter routes to protected data calls. If the request doesn't has a valid authenticated token, the api responds with unauthorized (http error 401). If the token is valid the request for data is continued. User authorization data from the token payload can be trusted and used to authorize or filter database queries based on permission.  

Here is [documentation](https://github.com/auth0/node-jsonwebtoken) for signing and verifying jwt tokens in node using [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) library.   


Trade off: the jwt tokens have an expiration. The pro of longer expirations is convenience for users. The con is longer sessions are less secure.   

Best practice: When storing passwords in the database, [hash the passwords](https://auth0.com/blog/hashing-passwords-one-way-road-to-security/).  

Alternatives: 3rd party service    
Trade off: Most projects will benefit from outsourcing their security because the 3rd party can dedicate more resource to making sure the process is secure. For instance, if there is a vulnerability, presumably they would patch it very quickly.  
Pro: not storing and protecting sensitive information including user's passwords, and jwt secret key. 
Con: dependence on 3rd party and possible changes. (They can go down, go out of business, get bought out, change their pricing, change their api)     
- [auth0](https://auth0.com/)
- [okta](https://www.okta.com/)  
- [Amazon cognito](https://aws.amazon.com/cognito/)   

### Transactional email services
- Twilio [sendgrid](https://sendgrid.com/)
- [mailgun](https://www.mailgun.com/)  
- [mailchimp](https://mailchimp.com/help/about-transactional-email/) mandrill api    
- [Amazon AWS SES](https://aws.amazon.com/ses/)  

# Dev Ops

### Current Prefered Deployment
Azure blob storage for images.  
Azure blob storage for front end.  
Azure App Services to host the app.  
Database is hosted on [mongo db atlas](https://cloud.mongodb.com).  

Using azure pipelines to deploy when posting to master. (see azure-pipelines.yaml)   
Currently github app installed under: github: Settings -> Integrations -> Azure pipelines -> Configure.    

###### Previous project deployments
In production, on some old projects, the front end is served through node. This avoids cors issues because everything is served from the same domain.  

In the past, I have hosted node using [pm2](https://pm2.keymetrics.io/) and used [nginx](https://www.nginx.com/) for web server on linux amazon aws ec2 instances.  

### Serverless
The upside to serverless is scalability and paying only for what you use. The downside is propreitary apis and lack of control of the environment. For instance, I had an issue with aws lambda because it only supporting an older version of node.   

##### Azure 
[Azure functions](azure_functions.md) - serverless functions use http triggers and binding to do routing.  

##### AWS serverless stack
- API Gateway / [Lambda authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html)    
- Lambda functions

##### Vercel (formerly zeit)  
[vercel (formerly zeit) now](https://vercel.com/home) - Used previously.  cli (now), now.json config file, but routes default to file system layout.  
host static site and [serverless functions](https://zeit.co/docs/v2/serverless-functions/introduction/) (use now api for routing instead of express etc.).  
Integrates with github etc.    

#### Cloud agnostic Frameworks  
One solution to vendor lockin is to use another 3rd party.  
[serverless](https://serverless.com/) - cli (serverless) + yaml config file w/ routes (serverless.yml). supports aws, azure, google cloud etc.   

[Terraform](https://www.terraform.io/) - cli. teraform configuration language. infrastructure as code i.e. much larger in scope than serverless. Cloud agnostic (aws/azure/google etc.)     



