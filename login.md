## Login
This article explains how to build a login system for a single page app with a rest api.  

#### Password Hash
When a user signs up (or changes their password) the password is stored in the database as a one way, [cryptographic hash](https://en.wikipedia.org/wiki/Cryptographic_hash_function). When the user attempts to login by submiting username and password, the user submitted password is hashed and compared to the stored hashed password to determine the validity of the credentials. Since it's a one way hashing function, the password can not easily be decrypted and it maintains the confidentiality of the user's password. Password hashing mitigates the risk of a data breach for the users (since users often use the same password on multiple sites) and for the organization's reputation.  

There are many cryptographic hash algorithms but I recomend using a hash algorithm designed for passwords such as [bcrypt](https://github.com/kelektiv/node.bcrypt.js). It is also a best practice to use a salt and select an appropriate cost factor for the hash algorithm.  

#### JWT  
If the username and hashed passwords match, the server [digitally signs](https://en.wikipedia.org/wiki/Digital_signature) and returns a [jwt](https://jwt.io/) (JSON web token)([RFC 7519](https://tools.ietf.org/html/rfc7519)) to the client. The jwt payload contains user authorization claims such as user id or customer id.  
Trade off: jwt tokens have an expiration. The pro of longer expirations is convenience for users. The con is longer sessions are less secure.   

#### JWT secret
Generate a secure, random jwt secret. I typically use [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) and it's default algorithm, HS256, with a key length of at least 32 characters. I typically generate a random jwt secret using openssl. The trade off with jwt secret length is performance versus security. For instance, HS512 algorith with 172 byte secret would be very secure.  
```
openssl rand -base64 172 | tr -d '\n'
```
Store the jwt secret securely. I typically store it in an environment varialbe. Don't put the jwt secret in the source code. If the jwt secret is compromised change it. 

After a successful login, on the browser client, store the token in sessionStorage or localStorage so the single page app data doesn't lose authtenticaion information if there is a  browser refresh. sessionStorage is chosen when you want logins to persist over multiple browser sessions.  

#### Client side authentication
- On the client side wrap react router's Route object with logic to redirect if the user isn't logged in [Example](https://reacttraining.com/react-router/web/example/auth-workflow). The user's login status, user name, etc. can be stored in a global store or Context. Client side authentication is for convenience, the pages without data are typically not secure assets. Also if the store is empty check localStorage or sessionStorage to restore login infomation after a user refresh.      

#### Use jwt to authenticate each rest api call. 
- On the client, authenticated api calls are sent through a library function to add the jwt token to all ajax requests in the authorization header using Bearer {token} scheme. 
- The node api has [middleware](http://expressjs.com/en/guide/using-middleware.html) that filter routes to protected data calls. If the request doesn't has a valid authenticated token, the api responds with unauthorized (http error 401). If the token is valid the request for data is continued. User authorization data from the token payload can be trusted and used to authorize or filter database queries based on permission. If the user is authenticated but is requesting information that it doesn't have permission to access respond with http error code 403.    

#### Additional considerations 
- Enforce a password policy with minimum complexity requirements (example minimum number of characters).  

- Require an email address during account creation for password recovery. Validate the user's email address.    

- You can implement [refresh tokens](https://auth0.com/learn/refresh-tokens/) or 2 form authentication for additional security.  

- Keep packages up to date to avoid security vulnerabilities.  

- Consider security [authentication risks](https://owasp.org/www-project-top-ten/2017/A2_2017-Broken_Authentication).  
Also consider more general security risk such as session hijacking, xss, and csrf. [OWASP Top 10 Web Application Security Risks](https://owasp.org/www-project-top-ten/)  

#### Alternatives: 3rd party service    
Projects may benefit from outsourcing their authentication security because the 3rd party can dedicate more resource to making sure the process is secure. For instance, if a [vulnerability](https://auth0.com/blog/critical-vulnerabilities-in-json-web-token-libraries/) is discovered, presumably they would patch it very quickly.  There is less code to write and maintain by not storing and protecting sensitive information including user's passwords, and jwt secret key. They also typically handle, change password, forgot password, social logins, and user management functions. The con is dependence on a 3rd party has risks. Their service can go down and you are powerless to resolve the problem perhaps before an important demo. They can go out of business, get bought out, or change their pricing. They can change their api and force you to change your code on their time schedule. They still run the risk of being compromised.  
- [okta](https://www.okta.com/) / [auth0](https://auth0.com/)
- [Azure AD](https://azure.microsoft.com/en-us/services/active-directory/)  
- [Amazon cognito](https://aws.amazon.com/cognito/)   
- Firebase has builtin authentication, but is integrated with the firebase ecosystem.   
- [fusion auth](https://fusionauth.io/)  
