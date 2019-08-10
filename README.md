# Authentication

Guidelines for authentication:

Server: Nodejs, express  
Client: Reactjs  

Consider using authentication as a service providers such as [auth0](https://auth0.com/) 

### JWT 
Consider using [jwt](https://jwt.io/)  
Server side authentication. 
Route all requests through an authentication layer.  

```
const app = express()
app.all("/api/*", jwtCheck)
```
