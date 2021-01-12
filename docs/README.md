## Chapter 2 - Decomposition Strategies

- Decomposition Patterns 
 
 1) Decompose by Business capability
 2) Decompose by subdomain

- Domain Driven Design

- The essence of microservice pattern is function decomposition of the application into services.

- The services are organized around business concerns rather than technical concerns.

- Microservice architecture is an architechture style which gives an application high maintainability,   testability and deployability.

- The software architecture of a computing system is a set of structures needed to reason about the system, which comprises of software elements, relation among them and properties of both.

- Its the decomposition of an application into several parts and then the relationship among them that determine the application illities.


### The 4 + 1 view model of software architecture

The purpose of each view are as follows:-

1) The logical view - Elements that are created by developers. For ex. the class and pacakges.

2) Implementation view - This view consist of the modules which represent packaged code and components which are executable and deployable.

3) Process View - The components at runtime.

4) Deployement - Processes running on machines.

### The Microservice architecture

The microservice architecture structures an application as a set of loosely coupled services.

### Overview of Architecture style

- The Layered architecture style

The Layered architecture organizes software elements into layers. And each layer has a well defined set of responsibilties. A layer can depend on the layer above it or below it.

Let's apply this layered architecture to the Logical view:-

It consist of three layers:-

1) The presentation layer

2) The Business logic layer

3) The persistence layer

- The Hexagonal architecture style

The heaxagonal architecture organizes the logical view in such a way that it keeps the business logic at its center.

It have inbound adapters that handle requests from outside by invoking the business logic.

It have outbound adapters that are invoked by the business logic and invoke external applications.

Example of outbound adapters is a data access object class(DAO) that implements operations  for accessing a database.

- The microservice architecture style

Monolitic style that structures the implementation view as a single component: a single executable and a WAR file.

While the microservice architecture style implements the implementation view as a set of multiple components. 

The components are services and the connectors are communication protocols that enable those services to collaborate.

### What is a service?

- A service is a standalone, independently deployable software component that implements some useful functionality.

Every service in a microservice architechture has its own architecture and potentially technology stack.

### What is loose coupling?

As all interactions happens to the service via the API , which encapsulates the implementation details. This enables the implementation of the service to change without impacting its clients. 

### Defining an application's microservice architecture

- System operation - A system operation is an abstraction of a request that the application must handle.It's either a command, which updates data. or a query which retrives data.

- The second step is the decomposition of the services. There can be various strategies to choose from:

1) Services based on Business capbilities 
2) Domain driven design subdomain

- Define services and how they are going to interact with another services in case if they have to.

#### Identifying the system operation 

- The first step is to create a high level domain model consisting of the key classes which provides vocabulary with which to describe the system operations.

- The second step is to identify the system operations and describe's each one behaviour in terms of domain model.

Domain model are derived from the nouns of the user story and system operations are derived from the verbs.

So the basic thing which we would like to achieve with the microservice architecture is the services which revolves around the business rather than the technical concepts.

#### Decomposing a service via business capability pattern

- Identifying Business capabilities - An organization business capability are identified by anylyzing  the purpose, structure and domain process.

Each of these Business capabities can be thought of as the service , except that it is business oriented rather than technical.

A capability can be often  decomposed to sub-capabilities.

#### Defining services by applying the decompose by sub domain pattern

It's an approach to building complex software that is centered on the developement of an object oriented domain model.

Two main concepts of DDD :-

1) Sub domain 
2) Boundend contexts

#### Single Responsibility Principle

Create small and Cohesive services that each have a single responsibility.

This will greatly reduce the size of the service and increase their stability.

#### Common Closure Principle

While creating a microservice we can apply this and package components that change for the same reason into the same service. Doing this will minimize the number of the services that needs to be changes and deployed when some requirements changes. Ideally a change will affect only a single team and single service. CCP is the antidote to the distributed monolith pattern.


### Obstacles while decomposing  an application into services

- Network Latency
- Reduced Availability due to synchronous communication
- Maintaing data consistency across services
- Obtaining consistent view of data
- God classes preventing decomposition


## Chapter 3 - Interprocess communication in a Microservice Architecture

- Interaction Styles

The choice of Interaction styles also impacts the availabilty of the application.

There can be two dimensions where the interaction styles can be defined:-

- First Dimension

1) One to one - Each client request only needs one service to be processed.
2) One to Many  - Each client request may need one or more service to be processed.

- Second Dimension is based of synchronous or asynchronous

1) Synchronous - The client expects a timely response from the service and may even block the service while it waits.

2) Asynchronous - The client dosen't block and teh response if any, need'nt to sent immediately.

- Different types of one to one interaction :-

1) Resquest/Response - Request is being sent , client is blocking the service and will wait until a response is received.
2) Asynchronous Request/Response - request is sent , no blocking of service and the service is called asynchronously and the response is not required immediately to be sent.
3) One way notifications - Request is send and however no no response is expected.



- Different type of one - many interactions:-

1) Publish/subscribe  - A client publishes a notification message, which is consumed by Zero or more interested services.
2) Publish/async responses  - A client publishes a request message and then waits for a certain amount of time for responses for interested services.


- Semantic Versioning of an API

- Major , Minor or Patch

1) Major - when u make an Incompatible change to an API
2) Minor - When u make backward compatible enhancements to API    
3) Patch - When u make backward compatible bug fig

- Minor Changes 

1) Adding optional attributes to the request
2) Adding attributes to response
3) Adding new Operation

- Major changes - Breaking changes

1) We need to either include the version in the API like V1 or V2
2) We can also include the version in the MIME type

### Communicating using the synchronous Remote Procedure Invocation Pattern

RPI - Remote Procedure Invocation 

Takes a request and process it and send back the response , some of them expects response timely while other does not.

The Proxy interface will encapsulate the underlying communication protocol.

- Using REST

REST is an architectural style which emphasize on the components scalibility , which can be deployed independently and enforce security, reduce interaction latency.

REST identifies resources which are basically nothing but business object.

They uses HTTP verbs like GET and POST for manipulating resources.

### Handling Partial failure using the "Circuit Breaker Pattern"

Mobile App -->(Create Order Endpoint) API Gateway (Order Service Proxy) --> Order Service

Here the Order services is unresponsive ; how shall be handle it otherwise it will lead to ultimately all the resources to be used up and then finally API will be unavailable.

It's essential for us to design our services in such a way to prevent the partial failures to cascade throughout your application.

Basically it can be done in the below two ways:-

1)  Use RPI proxies(Order service proxy in our case) , to handle unresponsive remote services.

2) You need to decide how to recover from a failed remote service.

- Developing Robust RPI Proxies 

 Below approach consist of a combination of the following mechanisms , where when one service call another service synchronously it should protect itself:-

 1) Network Timeouts  - use timeouts when waiting for a response, this way the resources are never tied indefinetly.
 2) Limiting the number of ourstanding request from the client to a service - place an upper limit to the number of request that the client can send to the server, once that threshold has been reached the attempts should fail immediately.
 3) Circuit Breaker Pattern - Track the number of successful and failed requests, if the error rate exceeds some threshold, trip the circuit breaker immeiately. After a timeout period the client sud try again and if successful , close the cicuit breaker.

 Netflix Hystrix is an open source library that implements this pattern.

 - Recovering from an unavailable service

 1) Either return a cached response when it is critical to show some response or return error message
 2) In case when the response is not critical the responses can be omitted to the client.


### Using service discovery

An application must use service discovery mechanism ; you can't statically configure a client with the IP address of the services.

The key concept of service discovery is simple, its key component is service registry which is a database of network locations of an application service's instances.

There are two ways to implement the service discovery:-

1) The services and their clients interact directly with the service registry.
2) The deployement infrastructure handles the service discovery.

- Applying the application level service discovery patterns

This constitutes of two patterns:-

1) Self Registration pattern - A service instance invoke the service registry's registration API to register its network location. It may also supply a health check URL.  A helath check URL is an API endpoint which service registry invoke to ensure that the service instance is healthy and shall be able to handle the request. Also a service registry may require a "Heartbeat API" to be invoked by  the service instance in order to prevent its registration from expiring.

2) Client Side Discovery pattern - When a service client wants to invoke a service, it queries the service registry to obtain the list of service instances. For better performance a Service client can also cache the service registry. The service client then uses the load balancing algorithm to direct the request to the particular service instance.

- Applying the platform-provided service discovery patterns

When using patform-provided service discovery patterns the platform itself is responsible for self registration, discovery and request routing.

This approach as well is a combination of two patterns:-

1) 3rd party registration pattern - Instead of service registry registring itself to service registry, a thrid party called registrar which is part of the deployment paltform handles this.

2) Server-side discovery pattern -  Instead of client querying the service registry, it makes a request to the DNS name, which resolves to the request router that queries the service reqgistry and load balances the request.

### Communicating using the asynchronous messaging pattern

























