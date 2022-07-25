# The Pros and Cons of using 3rd party services

Pros
- dedicate more resource to making sure the process is secure.  For instance, if a [vulnerability](https://auth0.com/blog/critical-vulnerabilities-in-json-web-token-libraries/) is discovered, presumably they would patch it very quickly.  
- There is less code to write and maintain by not storing and protecting sensitive information including user's passwords, and jwt secret key. 
- They also typically handle, change password, forgot password, social logins, and user management functions. 

Cons: 
The con is dependence on a 3rd party has risks. 
- Their service can go down and you are powerless to resolve the problem perhaps before an important demo. They still run the risk of being compromised.  
- They can go out of business, get bought out, or change their pricing. 
- They can change their api and force you to change your code on their time schedule. 
