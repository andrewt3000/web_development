## How to start building an app

Download [Visual Studio Code](https://code.visualstudio.com/download), and [node js](https://nodejs.org/en/download/).  

### Command Line
Many javascript libraries and tools use a [command line interface](https://en.wikipedia.org/wiki/Command-line_interface).  
[basic cli commands](cli.md)    
- MacOS [terminal](https://en.wikipedia.org/wiki/Terminal_(macOS)) 
- Windows [DOS](https://en.wikipedia.org/wiki/MS-DOS).  
- Windows PowerShell

### Generate App
``` zsh
#make project directory
mkdir userManager
cd userManager
npx create-react-app web
npx express-generator server 

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
run ncu and upgrade to latest packages.  
remove jade because it's obsolete and a view engine is not need for a rest api.  
```
npm uninstall jade
```
remove the views folder and these lines from app.js
```javascript
// view engine setup
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'jade');
```
change index.js to not call view engine.   

### Problem: web and server run on same port
By default the react and node generators start both process on [port](https://en.wikipedia.org/wiki/Port_(computer_networking)) 3000. I change node to run on 3001 (modify , and proxy node to port 3000). Proxying avoids [cors](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)  issues. See [Create React app documentation](https://create-react-app.dev/docs/proxying-api-requests-in-development/)

Change web/package.json to proxy node.  
```
"proxy": "http://localhost:3001",
````

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
```
npm run dev
```

Check that the front and back end work by pulling them up in the browser.  

### Create routes to first screens
[Install web react router](https://reacttraining.com/react-router/web/guides/quick-start).  
``` 
npm install react-router-dom
```
Delete the react boiler plate and copy/paste the [quick start](https://reacttraining.com/react-router/web/guides/quick-start).  
- change the title in public/index.html (search the project)
- Create Login Screen  

