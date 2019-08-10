# Authentication

Guidelines for authentication:

Server: Nodejs, express  
Client: Reactjs  

Consider using authentication as a service providers such as [auth0](https://auth0.com/) 

### JWT 
Consider using [jwt](https://jwt.io/) because it doesn't require tracking state on the server. JWT has 3 parts: header, payload, and signature. Payload contains stateful fields such as user name, user status, etc.    

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
```
var jwt = require('jsonwebtoken');
```
