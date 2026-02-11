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
and regular expression based routes ? How to do API versioning using HTTP ? Different types of versioning techniques ? 
What is the best way to deprecate it out ? What are the best practices in the industry ? Benefits of route grouping and how it 
helps with versioning permissions and shared middleware ? How to secure routes ? How to optimize route matching performance ?
## 4. Serialization and Deserialization
How before sending the data over to the network, our server translates the data into a particular format and after receiving the 
data from the client over the internet how it translates the data recieved to its native format that is called deserialization ?
What is the need of it and how it helps with interoperability standard ? The different formats that are used in serialization and 
deserialization. Text based formats like JSON, XML; Binary formats like protobuf. 
What are the performance differences between these two and when to use which one ?
How different programming languages implement serialization and deserialization ?
Structure of JSON and the different datatypes like strings, numbers, booleans, arrays and objects ? How realization of nested objects
and collections are handled in JSON ? How deserializing into data structures the native ds works like (python dictionary, golang structs, 
javascript object) ?
What are the common errors while dealing with JSON like handling missing or extra fields, dealing with null values or date, serialization
issues and the timezone issues ? How to implement custom serialization while before sending or serializing data into JSON ?
Error handling and serialization deserialization for example invalid data, data conversion errors, unknown fields.
Security concerns like injection attacks. Why to do validation before deserialization, validating JSON schemas before processing data
using JSON schema validation and the performance aspect of it like reducing the serialized data through compression and eliminating
unnecessary fields like serialization performance between text based and binary formats like JSON versus protobuf. The tradeoffs between readability
and performance because in text based format, one can easily check the payload while that does not work the same in binary format.
There is a valid tradeoff between when we use a binary format and when we use a text based format.
## 5. Authentication and Authorization
Why do we use different types of authentication like stateful, stateless ? What are basic authentications and what is better token authentications ?
What are sessions, JWT cookies ? 
## 6. Validation and Transformation

## 7. Middlewares

## 8. Request Content

## 9. Handlers or Controllers

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
