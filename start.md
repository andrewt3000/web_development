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
mkdir carl2
cd carl2
npx create-react-app web --template redux
npx express-generator server 

#put whole project in git
rm -rf web/.git
git init

#start web app
cd web
npm start

#In another shell
cd server
npm install
npm start

```

### 
By default npm starts web on port 3000, and node on port 4001. 

Change web/package.json by adding line below. This avoids [cors](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)  issues. See [Create React app documentation](https://create-react-app.dev/docs/proxying-api-requests-in-development/)

```
"proxy": "http://localhost:3001",
````
