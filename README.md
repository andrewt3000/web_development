# Web Development
Resources for building web applications.  

### React  
[Reactjs](https://reactjs.org/docs/getting-started.html)    
[create react app](https://github.com/facebook/create-react-app)  

React UI libraries:  
[styled components](https://www.styled-components.com/)   
[antd](https://ant.design/docs/react/introduce)  
[react bootstrap](https://react-bootstrap.github.io/)  
[material UI](https://material-ui.com/)  

[react router](https://reacttraining.com/react-router/web/guides/philosophy)  


### Node basics
request object: req.params, req.body  
[Middleware](http://expressjs.com/en/guide/using-middleware.html)


## Authentication and Authorization
Authentication is establish the identity of a user.   
Authorization is establishing the user privileges and access.  

Consider using identity as a service providers such as [auth0](https://auth0.com/), okta, and [Amazon cognito](https://aws.amazon.com/cognito/) because you don't have to store and protect sensitive information including user's passwords, and your jwt secret key. It's also simple to implement 3rd party logins such as Google or Faceboook.     

https://medium.com/swlh/a-practical-guide-for-jwt-authentication-using-nodejs-and-express-d48369e7e6d4#0e3b


### JWT 
I prefer using [jwt](https://jwt.io/) because it doesn't require tracking state on the server. JWT has 3 parts: header, payload, and signature. Payload contains stateful fields such as user name, user privileges, company_id etc. 

If the user login is successful it returns a jwt token to the client. I typically store the token in localStorage and have a function to add the jtw token to all ajax requests in authorization header as Bearer {token}. The node api has middleware that filters out routes that are not authenticated. 

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

### Interesting technologies
[serverless](https://serverless.com/)  
[graphql](https://graphql.org/)  

