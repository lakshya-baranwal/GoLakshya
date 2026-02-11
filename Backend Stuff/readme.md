# Backend From First Principles
1. A High Level Understanding 
2. HTTP Protocol 
3. Routing 
4. Serialization and Deserialization 
5. Authentication and Authorization 
6. Validation and Transformation 
7. Middlewares 
8. Request Content 
9. Handlers or Controllers 
10. CRUD 
11. REST Best Practices 
12. Databases 
13. Business Logic Layer (BLL) 
14. Caching 
15. Transactional Emails 
16. Task Queuing and Scheduling 
17. Elasticsearch 
18. Error Handling 
19. Config Management 
20. Logging, Monitoring and Observability 
21. Graceful Shutdown
22. Security
23. Scaling and Performance
24. Concurrency and Parallelism
25. Object Storage and Large Files
26. Realtime Backend Systems
27. Testing and Code Quality
28. 12 Factor App Principles
29. OpenAPI Standard
30. Webhooks
31. DevOps For Backend Engineers

---

## 1. A High Level Understanding
How request from browser flows through different hops, the network firewalls over the internet ? 
How it is routed to our backend server that is situated in a remote AWS server and 
how it responds to that request ? 
What the responses looks like ? 
How a client communicates with a server and how the server responds ?
## 2. HTTP Protocol
Understanding HTTP protocol, what is the role it plays ? 
How the communication is established through HTTP ? How the HTTP raw messages looks like ? 
How HTTP raw messages looks like ? What are the HTTP headers ? What are the role of the headers ? 
What are the different type of headers like request headers, representational headers general headers and security headers ? 
What are different types of HTTP methods like GET, POST, PUT, DELETE and when to use them ?
What are the semantics and what are the principles behind them ?
What is the ??-flow and how does it work ?
How a simple request defers from a preflight request and how a preflight request ?? looks like from our browser to 
the server and back to the browser ?
HTTP responses and their structure ? What are different status codes that server returns and 
when to return which type of code and what are the most commonly used HTTP status codes ?
HTTP caching and what are the different types of caching techniques using HTTP like ETags and max-age headers ?
Differences between HTTP 1.1, HTTP 2.0, HTTP 3.0 and what are the differences between them ?
How content negotiation looks like between client and server using different headers ? 
How persistent connections work in HTTP ? HTTP compression and different types of compression techniques like 
gzip, deflate and BR ? Which is the commonly used technique and security aspect of it the SSL, TLS ?
## 3. Routing
How routing maps URLs to server side logic and what is the connection between routing and HTTP methods ?
What are different components of routes like path parameters and query parameters ? 
What are different types of routes like static routes, dynamic routes, nested routes, hierarchical routes, wild card routes, 
and regular expression based routes ? 
How to do API versioning using HTTP ? 
What are different types of versioning techniques ? 
What is the best way to deprecate it out ? 
What are the best practices in the industry ? 
What are benefits of route grouping and how it helps with versioning permissions and shared middleware ? 
How to secure routes ? 
How to optimize route matching performance ?
## 4. Serialization and Deserialization
How before sending the data over to the network, our server translates the data into a particular format and after receiving the 
data from the client over the internet how it translates the data recieved to its native format that is called deserialization ?
What is the need of it and how it helps with interoperability standard ? 
The different formats that are used in serialization and deserialization. 
Text based formats like JSON, XML; Binary formats like protobuf. 
What are the performance differences between these two and when to use which one ?
How different programming languages implement serialization and deserialization ?
Structure of JSON and the different datatypes like strings, numbers, booleans, arrays and objects ? 
How realization of nested objects and collections are handled in JSON ?
How deserializing into data structures the native ds works like (python dictionary, golang structs, javascript object) ?
What are the common errors while dealing with JSON like handling missing or extra fields, dealing with null values or date, serialization
issues and the timezone issues ? 
How to implement custom serialization while before sending or serializing data into JSON ?
Error handling and serialization deserialization for example invalid data, data conversion errors, unknown fields.
Security concerns like injection attacks. 
Why to do validation before deserialization, validating JSON schemas before processing data using JSON schema validation and
the performance aspect of it like reducing the serialized data through compression and eliminating unnecessary fields like serialization 
performance between text based and binary formats like JSON versus protobuf. 
The tradeoffs between readability and performance because in text based format, one can easily check the payload while that does not work the same in binary format.
There is a valid tradeoff between when we use a binary format and when we use a text based format.
## 5. Authentication and Authorization
Why do we use different types of authentication like stateful, stateless ? 
What are basic authentications and what is better token authentications ?
What are sessions, JWT cookies ? 
What is OAuth protocol and Open ID connect ? 
How API keys work ? 
How multifactor authenications work ? 
What is salting, hashing and different cryptographic techniques used in authorization ? 
What are ACK, RBAC, Rollback ? 
What are the best practices in security like securing cookies, avoiding csrf, xss, mitm like audit logging (which basically means recording authentication,
authorization events for audits and monitoring failed login attempts, privilege escalation and access to sensitive resources) ?
Obfuscating authenticated related error messages preventing information leakage to attackers through detailed error messages like handling edge cases (for
example consistency in responses across different failure models like rate limiting and account lockout).
How to avoid timing attacks (for example attackers can exploit time differences in error responses to infer valid credentials like an error for a wrong 
password might take longer than an error for valid username because to check for a password we have to do some kind of hashing using some
cryptographic techniques which takes some time so it is possible to calculate tiny bit of time differences and guess passwords.
## 6. Validation and Transformation
What are the different types of validation like syntactic validation (for example checking whether an email or a phone number is valid or not, whether
date format is valid or not), semantic validation (for example a date of birth cannot be in future or the age of a person should be between 1 and 120),
and type validation (for example checking the input values match expected types like string, boolean, array, object) ? 
What are the best practices for validation ? 
What is the difference between client side validation and server side validation ? 
What is the importance of server side validation even if client side validation is already implemented ? 
(Because client side validation improves user experience by providing instant feedback but server side validation is
the true security implementation because it is the gateway to business logic)
What is the importance of failing fast by reducing unnecessary processing by returning early ? 
Why to keep consistency between front end validation and backend validation ? 
What are transformations (for example type casting converting a string to a number or a number to a string because in query 
parameters or path parameters all we recieve is a string and if we are expecting an ID field which is a number so before sending it to the handlers, 
we have to convert it into a number which has to be taken care of in the validation pipeline)? 
What is normalization (for example converting an email to lowercase or trimming whitespaces from a string or adding country code to a phone number)? 
What is sanitization for security issues (for example we have to sanitize a string that is submitted by the user to prevent attacks like SQL injection)?
What are different complex validation logic like relationshp based validation and conditional validation ? 
Relationship based validation: a user submitted a form and it has two fields like one is password and another is confirm password so we have to 
check whether the two strings are the same or not. 
Conditional validation: we have two fields in the form, one is partner name and the second is married which is a boolean so a partner field might only be required if the married is true.
Chain validation: converting a string to lowercase then removing special characters and then checking its length.
How error handling is done in validation like sending meaningful error messages to front end so that the user can fix them and aggregating all validation
errors in one response for client side display or obfuscating error messages (instead of saying invalid password, we will say invalid credentials to
prevent differenct types of attacks).
How to gracefully handle failed transformations ? 
(for example an invalid JSON and a failed date conversion and how to let the user know in a meaningful message)
What are performance trade-offs of validation and how to optimize it by returning early, avoiding redundant validations ? 
## 7. Middlewares
What is a middleware and when to use them ? 
What are the common use cases of middlewares ? 
What is the role of a middleware in a request cycle (for example a pre request middleware or a post response middleware) ? 
What is the flow of middlewares (for example techniques like chaining a middleware is executed in a sequence passing control to the next middleware until request reaches its final handler) ?
How to order middlewares appropriately (for example we have to go in this order, log the request, check whether the user is
authenticated or not, validation, route handling, error handling and this order matters in middleware flow)?
## 8. Request Content
## 9. Handlers or Controllers
What is the MVC pattern ? 
What are handlers, controllers and services and what are their responsibilities ? 
And reducing the code with middleware.
What is centralized error handling in handlers, consistent sucess and error message formats and how it is implemented in controllers ?
## 10. CRUD
## 11. REST Best Practices
## 12. Databases
## 13. Business Logic Layer (BLL)
## 14. Caching
## 15. Transactional Emails
## 16. Task Queuing and Scheduling
## 17. Elasticsearch
## 18. Error Handling
## 19. Config Management
## 20. Logging, Monitoring and Observability
## 21. Graceful Shutdown
## 22. Security
## 23. Scaling and Performance
## 24. Concurrency and Parallelism
## 25. Object Storage and Large Files
## 26. Realtime Backend Systems
## 27. Testing and Code Quality
## 28. 12 Factor App Principles
## 29. OpenAPI Standard
## 30. Webhooks
## 31. DevOps For Backend Engineers
