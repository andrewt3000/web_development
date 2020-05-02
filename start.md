## How to start building a MERN web app
I am going to build a simple web app with login screen and a crud screen.  


Download and install [Visual Studio Code](https://code.visualstudio.com/download), and [node js](https://nodejs.org/en/download/).  

### Command Line
Many javascript libraries and tools use a [command line interface](https://en.wikipedia.org/wiki/Command-line_interface).  
[basic cli commands](cli.md)    
- MacOS [terminal](https://en.wikipedia.org/wiki/Terminal_(macOS)) 
- Windows [DOS](https://en.wikipedia.org/wiki/MS-DOS).  
- Windows PowerShell

### Generate App
``` zsh
#make project directory. typically project name is domain.
mkdir userManager
cd userManager
#typically the names are the subdomain.
npx create-react-app www
npx express-generator api 

#put whole project in git
rm -rf web/.git
git init

#start web app
cd web
npm start

#start node server
cd server
npm install
npm start

```

### Problem: Express generator installs jade which is out of date
run ncu in server and upgrade to latest packages.  
remove jade because it's obsolete and a view engine is not need for a rest api.  
``` zsh
npm uninstall jade
```
remove the views and public folders because we are building a rest api, not serving web pages.  
remove these lines from app.js. 
```javascript
// view engine setup
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'jade');

// catch 404 and forward to error handler
app.use(function(req, res, next) {
  next(createError(404));
});
```
in app.js change res.render() to res.send() call for handling 500 errors to not use view engine. (near bottom)  
in server/routes/index.js change res.render to res.send()  

### Problem: web and server run on same port
By default the react and node generators start both process on [port](https://en.wikipedia.org/wiki/Port_(computer_networking)) 3000.  
First, change node to run on another port (eg. 3001)  
Then you have 2 options:  
Option 1: Proxy node to port 3001 to port 3000. Proxying avoids [cors](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)  issues. See [Create React app documentation](https://create-react-app.dev/docs/proxying-api-requests-in-development/)

Change web/package.json to proxy.  
```javascript
"proxy": "http://localhost:3001",
````
Option 2: setup cors. 
- Install node cors library, and add middleware to routes. [Example](https://expressjs.com/en/resources/middleware/cors.html) See [wikipedia "simple example"](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) for high level explanation of cors. 
``` zsh
npm install cors
```

``` javascript
var cors = require('cors')
var corsOptions = {
  origin: 'http://localhost:3000',
  optionsSuccessStatus: 200 // some legacy browsers (IE11, various SmartTVs) choke on 204
}
app.all("/*",  cors(corsOptions))
```

This is the preferred way to do it, but you will have to add the url of the web sites for production.  

Also change the method that calls your api to go to the node port. This will also have to configured differently for live.   

### Configure nodemon
[nodemon](https://nodemon.io/) is a tool that helps develop node.js based applications by automatically restarting the node application when file changes in the directory are detected.  

Install nodemon  
```
npm -g install nodemon
```

Changer server/package.json to run nodemon in dev but not in production.  
```
"scripts": {
    "dev": "nodemon ./bin/www",
    "start": "node ./bin/www",
  },
```

Now start node with command
``` zsh
npm run dev
```

Check that the front and back end work by pulling them up in the browser.  

### Create routes to first screens
[Install web react router](https://reacttraining.com/react-router/web/guides/quick-start).  
``` 
npm install react-router-dom
```
Delete the react boiler plate and copy/paste the [quick start](https://reacttraining.com/react-router/web/guides/quick-start).  
- change the title in web/public/index.html to User Manager
- create routes to 2 screens: root is login screen, /users is user list.    

### Configure Node to connect to database
Consider implications of putting a real password in source control, especially if it's open source project.  
Password are often put in config file not in source control or in an environment variable.  
Password can also be encrypted for security however then you have to secure the encryption keys.  

