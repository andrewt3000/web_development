# Web Development

One of the first consideration for building a web app is what stack to use. Is the app for the desktop and/or mobile?   

The stack I prefer for desktop web apps is:  
Server api: Nodejs, express  
Client: Reactjs  

React UI libraries: [styled components](https://www.styled-components.com/)  


## Authentication and Authorization
Authentication is establish the identity of a user.   
Authorization is establishing the user privileges and access.  

Consider using identity as a service providers such as [auth0](https://auth0.com/), okta, and [Amazon cognito](https://aws.amazon.com/cognito/) because you don't have to store and protect sensitive information including user's passwords, and your jwt secret key. It's also simple to implement 3rd party logins such as Google or Faceboook.     

https://medium.com/swlh/a-practical-guide-for-jwt-authentication-using-nodejs-and-express-d48369e7e6d4#0e3b


### JWT 
I prefer using [jwt](https://jwt.io/) because it doesn't require tracking state on the server. JWT has 3 parts: header, payload, and signature. Payload contains stateful fields such as user name, user status, etc. The token is sent to the server in authorization header as Bearer {token}.    

### Implementations
Server side authentication. 
Route all requests through an authentication layer.  

Jemison ERP code uses [auth0 express-jwt](https://github.com/auth0/express-jwt)   
```
const jwt = require("express-jwt")

const app = express()

const jwtCheck = jwt({
  secret: jwks.expressJwtSecret({
    cache: true,
    rateLimit: true,
    jwksRequestsPerMinute: 5,
    jwksUri: config.auth.jwksUri
  }),
  audience: config.auth.audience,
  issuer: config.auth.issuer,
  algorithms: ["RS256"]
})

app.all("/api/*", jwtCheck)
```

Metal view used library 

Authenticate through application level [middleware](http://expressjs.com/en/guide/using-middleware.html). If authenticated, add into to request and call next middleware. Otherwise, respond with 401.  

```
var jwt = require('jsonwebtoken');


app.use(function(req, res, next) {

  let token = ''
  if (req.headers.authorization && req.headers.authorization.split(' ')[0] === 'Bearer') {
    token = req.headers.authorization.split(' ')[1];
  } else if (req.query && req.query.token) {
    token = req.query.token;
  } else {
    if (req.method === 'OPTIONS') {
      next();
      return;
    }else{
      return res.status(403).send({
        success: false,
        message: 'No token provided.'
    });
    }
  }
  jwt.verify(token, req.app.get('secret'), function(err, decodedToken) {
    if(err){
      console.error(err)
      res.status(401).send(err);
      return
    }
    console.log('decodedToken ' + decodedToken)

    if(decodedToken.id !== undefined) {
      console.log('normal')
      req.my_user_id = decodedToken.id;
      req.my_company_id = decodedToken.company_id;
    } else if (decodedToken.quoteId !== undefined) {
      console.log('temp service center')
      req.myQuoteId = decodedToken.quoteId
      req.myQuoteRecipientId = decodedToken.quoteRecipientId
    }

    next();
  });

});

```
