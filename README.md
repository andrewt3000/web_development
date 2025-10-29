# Software Development
This document contains opinions about tools and methods of building web apps.   

[Dev tools](#dev-tools)  
[Front End](#front-end)  
[Server Side](#server-side)  
[Database](#databases)  
[Dev Ops](#dev-ops)  
[Project management](#project-management)  

# Dev Tools 
Web architectures has gone through 3 phases: 
- 90s/2000s - Server side rendering
- 2010s - [single page app (spa)](https://en.wikipedia.org/wiki/Single-page_application) and a [rest api](https://en.wikipedia.org/wiki/Representational_state_transfer) for the back end. 
- 2020s - Hybrid (client and SSR (server side rendering)) frameworks that use [hydration](https://en.wikipedia.org/wiki/Hydration_(web_development)).   

I prefer using [javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)/[typescript](https://www.typescriptlang.org/) on the front end because it's native to the browser (this may be changing due to [web assembly](https://developer.mozilla.org/en-US/docs/WebAssembly)). In the past I have used [Node](https://nodejs.org) on the backend because as full stack dev I prefer to work in the same lanuage as it increases javascript fluency. However I have more recenlty used frameworks such as 
- [next.js](https://nextjs.org/) - Next js is good for ssr and runs well on vercel, but vercel can be expensive.  
- [react router](https://reactrouter.com/)  formerly [remix](https://remix.run/) - react router 7 replaces remix.
- [tan stack](https://tanstack.com/) - Tanstack is a client side framework that includes client-side data fetching, routing, and caching.  
- [expo](https://expo.dev/) - for mobile apps    

Another consideration for choosing a backend is integration with the database. It's important that the database api is well supported, stays up to date and has good support for database features and types. Well supported ORMs are another key feature. Here are some well supported backend languages and database combinations:
- nodejs / mongodb  
- ruby on rails / postgres  
- .net / sql server  
- java / oracle, ibm db2  

### AI 
Prefered AI setups:
I typically use [Cursor](https://cursor.com/) or [Claude Code](https://www.claude.com/product/claude-code) cli.  


### IDE
Preferred: [Visual Studio Code](https://code.visualstudio.com/)      
VS Code has support for productivity features such as [emmet](https://emmet.io/) and [code snippets](https://code.visualstudio.com/docs/editor/userdefinedsnippets)    

- Configure emmet to work in [jsx](https://stackoverflow.com/questions/56311467/configure-emmet-for-jsx-in-vscode). (Code > Preferences > Settings: Emmet: Include Languages -> javascript / javascriptreact ). 
- Create custom code snippets (Code > Preferences > Configure User Snippets / Javascript)

``` json
	"Print to JSON console": {
		"prefix": "logj",
		"body": [
			"console.log(JSON.stringify($1));",
			"$2"
		],
		"description": "Log json output to console"
	},
```

Learn useful VS Code shortcuts. [Mac](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf) / [Windows](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)  

Alternative: [vi](https://www.vim.org/)  

### Coding standards
[eslint](https://eslint.org/) code linter   
[prettier](https://prettier.io/) code formatter. 
- Install VS Code [eslint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint).  
- Install VS code Prettier extension and make prettier the [default formatter](https://github.com/prettier/prettier-vscode#default-formatter). 
- Install husky [pre-commit hook](https://github.com/azz/pretty-quick#pre-commit-hook) to format code before commit. It's important all code is formatted the same, otherwise it makes diffs and merging conflicts difficult to understand.  

variables are in camelCase.  

### Source Control
Preferred: [git](https://git-scm.com/) ([command ref](https://git-scm.com/docs)  ) - open source, distributed [version control](https://en.wikipedia.org/wiki/Version_control)     

Alternative: [Mercurial](https://www.mercurial-scm.org/). 

git obsoletes many other open source vcs I have previously used such as rcs, cvs, and subversion.   

### Source control hosting
Preferred: [github](https://github.com/)  
Alternatives: [gitlab](https://about.gitlab.com/), [bitbucket](https://bitbucket.org/)  

If you're hosting at AWS you might want to consider [Code Commit](https://docs.aws.amazon.com/codecommit/latest/userguide/welcome.html) due to integration features.  

### Version control workflow
Version control work flow is a function of the size and organization of your team as well as the stage of your project.  

As an example, this is a reasonable work flow with multiple developers and an architects where the project is live.    
- Devs work on feature branches. 
- When the feature is complete, devs do a PR ([pull requests](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests)) to merge their branch to a test branch.  
- Architect approves the PR, inspects and tests the code.   
- Architect merges the test branch to main/master branch which automatically deploys to production.  

### App Versioning  
Preferred: [semantic verisioning](https://semver.org/)   
I also plan to track an app version number in the package.json file and reflect that number to users to make sure they have the latest version. 

### Package manager
Preferred: [npm](https://www.npmjs.com/)  - npm is a cli package manager and task runner. npm hosts a public package repository.    
Alternatives: [yarn](https://yarnpkg.com/)  

### Updating packages
Best practice: Periodically (weekly?) update javascript packages on front and back end. This is important for security reasons, but can challenging when libraries change and break your project. After upgrading run tests.    
```
# install ncu
npm install -g npm-check-updates  

#command show what needs to be updated
ncu 

#updates the package.json file. 
ncu -u 
```



# Front End

### React  
[Reactjs](https://reactjs.org/) ([docs]([https://reactjs.org/docs/getting-started.html](https://react.dev/learn))) - A JavaScript/typescript library for building user interfaces.  
[chrome extension](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)  

[Vite](https://vitejs.dev/) is a simple option to create react apps. ([create react app](https://create-react-app.dev/) no longer maintained).  However I would typically use a framework to start a project.    

Preference: I generally prefer to use functional rather than class [components](https://reactjs.org/docs/components-and-props.html) and to use [state hooks](https://reactjs.org/docs/hooks-state.html) and [effect hooks](https://reactjs.org/docs/hooks-effect.html) rather than [state and lifecyle](https://reactjs.org/docs/state-and-lifecycle.html) I also would consider using hooks in place of [higher order components](https://reactjs.org/docs/higher-order-components.html) and [render props](https://reactjs.org/docs/render-props.html). It's recommended to not use [unneccesary effects](https://react.dev/learn/you-might-not-need-an-effect) and consider server side rendering for event handling.  

Alternatives: [Angular](https://angularjs.org/), [Vue](https://vuejs.org/) ([vuex](https://vuex.vuejs.org/) [nuxt](https://nuxtjs.org/))   
I prefer react because of it's [one-way binding](https://reactjs.org/docs/thinking-in-react.html) rather than two-way binding which is supported in angular and vue. I also prefer using javascript inline rather than directives for control such as ngFor, ngIf (angular) or v-for, v-if (vue). Using javascript inline increase javascript fluency.     

### Custom styling
By default, I try to make apps [responsive](https://en.wikipedia.org/wiki/Responsive_web_design).  

Preferred:
[tailwind css](https://tailwindcss.com/) - [utility first](https://tailwindcss.com/docs/utility-first/) css framework. 

In the past, I would use [standard](https://www.w3.org/Style/CSS/Overview.en.html)  [css](https://developer.mozilla.org/en-US/docs/Web/CSS). I prefer using an atomic css style. I prefer using [css grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout) for layout such as [holy grail layout](https://alligator.io/css/css-grid-holy-grail-layout/). I prefer [flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox) for laying out items in rows or columns. I often use media queries to make responsive styles. I typically avoid css preprocessors such as sass and less. I rarely use float, [clear](https://www.w3schools.com/howto/howto_css_clearfix.asp), etc. anymore.   

Using [Shad cn](https://ui.shadcn.com/) component library to start a project is my current default.  It's a modern, simple design with themes, and light/dark mode feature.  

Alternatives:  
- [material UI](https://material-ui.com/)  - Looks like Google.  
- [antd](https://ant.design/docs/react/introduce) - Desktop oriented react ui components. 
	- Pro: Antd has a desktop oriented Table component that has scrolling features, based on [rc-table](https://github.com/react-component/table)  
	- Con: I don't like the typography (probably due to Chinese influence and their different character set). There is not as much emphasis on responsive design as other packages.  
- [react bootstrap](https://react-bootstrap.github.io/) - originally [bootstrap](https://getbootstrap.com/) was created by twitter.   
- [chakra](https://chakra-ui.com/)  
- [blueprint](https://blueprintjs.com/)  
- [element](https://element.eleme.io)  
- [semantic ui](https://semantic-ui.com/)  

### State Management   
I typically use a state store for non-trivial projects. One reason is to avoid excessive [lifting of state](https://reactjs.org/docs/lifting-state-up.html) and prop drilling. Another reason to use a state store is middleware can simplify some tasks such as logging or [undo](https://redux.js.org/recipes/implementing-undo-history) functinality.  
State stores typically have reducers that accept an action and the state and return the new state. Change to the state store is initiated by dispatching an action.    
Preferred: [mobx](https://mobx.js.org/) - simple, scalable, state management.  

Alternatives:  
- [react Context](https://reactjs.org/docs/context.html) can be used with useContext hook.  
- [redux](https://redux.js.org/) is a predictable state container for JS Apps. Has immutable state. It has more boilerplate than mobx, [redux tradeoffs](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367). [See my redux cheat sheet](redux.md) Typically used with [Redux Toolkit](https://redux-toolkit.js.org/)  

### React Router
prefered: [react router](https://reactrouter.com/) is a declarative react routing framework.
React router supports nested routing.   
React router supports a DOM history which enables the browser back button even though it's used in single page applications.  

### Data fetching
[fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API#Concepts_and_usage) is a web api (natively supported in more recent browsers).  
best practice: If supporting older browsers use a [polyfill](https://developer.mozilla.org/en-US/docs/Glossary/Polyfill) such as [isomorphic-fetch](https://www.npmjs.com/package/isomorphic-fetch) or [fetch](https://github.com/github/fetch).  

[TanStack query](https://tanstack.com/query/latest/docs/framework/react/overview) formerly react query is a popular way to fetch data in react apps.  

alternative: [axios](https://github.com/axios/axios)  

### Front end unit testing
Jest - ([docs](https://jestjs.io/docs/en/getting-started)) test runner, assertion library, and mocking library.  
[snapshot testing](https://jestjs.io/docs/en/snapshot-testing) is a feature that I use.  
Jest expects tests to be in a folder named \_\_tests__ or to be named file_name.test.js  
[react testing library](https://testing-library.com/docs/), a ui testing library, replacing enzyme.  
```
#to run tests
npm test
```

#### Dom and assertion libraries
- [react testing library](https://testing-library.com/docs/react-testing-library/intro) is an alternative to enzyme for dom manipulation and traversal. Written by Kent C. Dodds.    

### End to End Testing
- [cypress](https://www.cypress.io/)  
- [puppeteer](https://pptr.dev/) Headless Chrome Node.js API  

# Server Side
### Node  
[node](https://nodejs.org) - javascript runtime built on chrome v8 javascript engine. Node is frequently run as an [http server](https://nodejs.org/en/docs/guides/getting-started-guide/).     
[n](https://github.com/tj/n) - tool to switch versions of node.  

[Express](https://expressjs.com/) node library for routing http requests.  
[Express application generator](https://expressjs.com/en/starter/generator.html) - tool to generate node express   
Guide: [Routing](https://expressjs.com/en/guide/routing.html) [Using Middleware](http://expressjs.com/en/guide/using-middleware.html)  Middleware, in the context of express, is code between receiving a request and producing a response.  
[4.X API](https://expressjs.com/en/api.html)  
Node contains objects: express, request, response and router.  
Commonly used: app.use(), router.route(), req.params, req.body    

Alternatives node rest APIs:  
- [hapi](https://hapi.dev/) - node rest api that doesn't use middleware. Express was originally designed for server side rendering, not rest apis.    
- [loopback](https://loopback.io/doc/) - node rest api framework that uses express.   

Alternatives:  
- [graphql](https://graphql.org/) - is an alternative to rest apis. GraphQL is a specification for a typed query language similar to sql and runtime which incluces a client (eg. relay, apollo) and server. [Apollo](https://www.apollographql.com/) is a popular graphql implementation. [Relay](https://relay.dev/) is a popular graphql client.     
- [serverless](https://serverless.com/) is a framework that can route to serverless cloud functions such as AWS lambda. Serverless cloud functions can be implemented in a variety of languages.   

# Utilities
For date time libraries I use [Luxon](https://moment.github.io/luxon/).  


# Databases
There are 2 classes of databases: relational (which typically use SQL) and NoSql which include Wide column stores, document stores, key-value stores, and graph databases.  

Best practice for relational databases: [database normalization](https://en.wikipedia.org/wiki/Database_normalization)  

Naming convention: table or document names are singular.  

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


#### Logins and 3rd party service    
I typically implment a [jwt login].  

Projects may benefit from outsourcing their authentication security because the 3rd party can dedicate more resource to making sure the process is secure. For instance, if a [vulnerability](https://auth0.com/blog/critical-vulnerabilities-in-json-web-token-libraries/) is discovered, presumably they would patch it very quickly.  There is less code to write and maintain by not storing and protecting sensitive information including user's passwords, and jwt secret key. They also typically handle, change password, forgot password, social logins, and user management functions. The con is dependence on a 3rd party has risks. Their service can go down and you are powerless to resolve the problem perhaps before an important demo. They can go out of business, get bought out, or change their pricing. They can change their api and force you to change your code on their time schedule. They still run the risk of being compromised.  
- [okta](https://www.okta.com/) / [auth0](https://auth0.com/)
- [Azure AD](https://azure.microsoft.com/en-us/services/active-directory/)  
- [Amazon cognito](https://aws.amazon.com/cognito/)   
- Firebase has builtin authentication, but is integrated with the firebase ecosystem.   
- [fusion auth](https://fusionauth.io/)  

### Rest API best practices
When writing a rest API use standard http repsonses.  
Return response code 200 for success if server completed request as expected.  
Return response code 400 if client sends an invalid request such as missing parameters.  
Return response code 401 if client isn't authenticated.  
Return response code 403 is client is authenticated but doesn't have permission.  
Return response code 404 is client request a route that doesn't exist.  
Return response code 500 if there is a server error.  
Return response code 503 if a service is unavaialble such as a database.  

### Error handling
I make a distinction between two types of errors: user errors and system errors. System errors are typically unexpected errors, they need to be logged with the stack trace, and notify a programming manager. They often require code to be modified to handle the errors more gracefully. User error needs to notify the user how to correct the problem or prevented from making it in the first place. Typically, this type of error doesn't require a change to code but if it's gotten consistently it may represent a UX problem.    

I typically return system errors as 500 errors to the client, and return user errors as 200 with an error message. http is an application level protocol, so it may also be appropriate to return 500 for user errors. More importantly, is to be consistent on a project so you can distinguish the system errors from user errors.     
### Error logging and notification
Using a browser error logging service such as [sentry](https://sentry.io/) helps alert to production problems on the client side.  
On the server side, you can search (grep) system logs. There are also many server side error logging and notification services.

[splunk](https://www.splunk.com/)  
[data dog](https://www.datadoghq.com/)  



### Transactional email services
- [resend](https://resend.com)
- [postmark](https://postmarkapp.com/) - recommended by peter levels.
- Twilio [sendgrid](https://sendgrid.com/) - previous market leader but declining.  
- [mailgun](https://www.mailgun.com/)  
- [mailchimp](https://mailchimp.com/help/about-transactional-email/) mandrill api    
- [Amazon AWS SES](https://aws.amazon.com/ses/)

# Dev Ops

### Hosting on a server 
This is the classic way to set up a node app before cloud services.  
Manage node using [pm2](https://pm2.keymetrics.io/)    
[nginx](https://www.nginx.com/) web server to serve front end, and [reverse proxy to node](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-14-04
).    
You can rack your own servers or deploy on virtual instances such as Amazon aws [ec2](https://aws.amazon.com/ec2/).  
Typially use ssh for setup and use crontab for background jobs.  

One simple option is to serve the front end through node. This avoids cors setup because everything is served from the same domain. You can also put a catch all route in node to serve the root of the spa.    

Pro:  
- Control of the environment. For instance, you can run any version of node you want (an older version for a legacy app or a cutting edge version to take advantage of new features).   
- No proprietary lock in    


### CDN / application container
| service | MS Azure | Amazon AWS | Other | 
|---|---|---|----|
| Front end file hosting | [Azure blob storage](https://azure.microsoft.com/en-us/services/storage/blobs/), [Azure cdn](https://azure.microsoft.com/en-us/services/cdn/) | S3, CloudFront | vercel, cloudflare |   
| Node hosting | [Azure App Services](https://azure.microsoft.com/en-us/services/app-service/) | elastic beanstalk | vercel serverless functions, cloudflare workers 
| Database hosting | [Azure Sql](https://azure.microsoft.com/en-us/services/sql-database/) | RDS |  [mongo db atlas](https://cloud.mongodb.com)|  
| Continuous deployment | Azure Devops Pipelines | CodePipeline | [Jenkins](https://www.jenkins.io/), [Circle CI](https://circleci.com), github actions |

Many cdns such as [vercel](https://vercel.com/) will default sensibly for react apps. For example it will publish when you push to master, redirecting to https and rewriting urls to create deep links.  Where as using azure or amazon they will require you to specify each step.  Using azure yaml pipelines (part of [azure devops](https://dev.azure.com/)) specify each step for continuous deployment (specify the push to master trigger to build deployment, specify the build command etc.).  Azure cdn needs to be purged after changes.  Deploying a spa will require Azure cdn rules such as [redirecting http to https requests](https://docs.microsoft.com/en-us/azure/cdn/cdn-standard-rules-engine) and add a URL rewrite to deep links in the single page app.    


### Serverless functions
Serverless function execute independently. That has pros and cons.  
Pros: 
- fine grain, horizontal scalability  
- pay only for what you use which is typically measured in function executions and execution time   
- serverless can be easier for an architect to manage a large team and application.  

Cons:  
- Cold Starts - if the service hasn't been used recently there can be a delay starting the service.  
- There are varying levels of support for cross-cutting concerns for serverless functions. For instance, all platfroms have proprietary routing apis. Examples also include functionality typically implemented in middleware such as authentication, cors, error logging etc.  
- There are varying levels of support for maintaining shared state such as database connection pooling. For instance, AWS has [RDS proxy](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html) which allows serverless apps to do connection pooling.   


| MS Azure | Amazon AWS | Vercel |  
|---|---|----|  
|[Azure functions](https://azure.microsoft.com/en-us/services/functions/) | [Lambda functions](https://aws.amazon.com/lambda/) | [Serverless functions](https://vercel.com/docs/v2/serverless-functions/introduction) |  
| http triggers and binding |  [API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) / [Lambda authorizers](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html) | |   
 
An early problem for adoption of serverless was running the environment locally for development. Most providers have a local dev environment now. Azure function development is now [integrated into VS Code](https://docs.microsoft.com/en-us/azure/azure-functions/functions-develop-vs-code?tabs=csharp) through a plugin.  

One solution to vendor lockin is to use another 3rd party.  
[serverless](https://serverless.com/) - cli (serverless) + yaml config file w/ routes (serverless.yml). supports aws, azure, google cloud etc.   

### Containers
Another deployment option is to create and deploy docker containers. One advantage of docker containers is you can replicate your environment in development, testing, production etc. You also avoid vendor lock-in between cloud providers. Docker is similar to a VM, but more lightweight.    
To deploy you [build](https://docs.docker.com/engine/reference/commandline/image_build/) an image using a [Dockerfile](https://docs.docker.com/engine/reference/builder/) and push it to a container repository such as Amazon [ECR](https://docs.aws.amazon.com/ecr/) or Docker Hub and then deploy it on a service such as Amazon [ECS](https://docs.aws.amazon.com/ecs/).  

| | Amazon AWS | MS Azure | Other |  
|---|---|---|----|  
| container registry | [ECR](https://docs.aws.amazon.com/ecr/) | [Azure container registry](https://learn.microsoft.com/en-us/azure/container-registry) | [Docker Hub](https://hub.docker.com/) |  
| container service | [ECS](https://docs.aws.amazon.com/ecs/) EKS | [ACI](https://learn.microsoft.com/en-us/azure/container-instances/) AKS | |  

Kubernetes can be used to scale containers to multiple nodes.  

###  Immutable Infrastructure  
[Terraform](https://www.terraform.io/) - teraform configuration language enables infrastructure as code. Cloud agnostic (aws/azure/google etc.) Terraform is used for creating an environment on demand rather than for simply deploying web apps.  

[AWS Cloud Formation](https://docs.aws.amazon.com/cloudformation/) - infrastucture as code. Has AWS lock in.    


# Project management
[Agile manifesto](https://agilemanifesto.org/)  

### Project management software
[Asana](https://app.asana.com/)  
[Atlassian Jira](https://www.atlassian.com/software/jira)  
[basecamp](https://basecamp.com/)    
[pivotal tracker](https://www.pivotaltracker.com/)  
[trello](https://trello.com/) - kanban style list making  

