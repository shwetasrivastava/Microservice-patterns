### Chapter 2 - Decomposition Strategies

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

- The purpose of each view are as follows:-

1) The logial view - Elements that are created by developers. For ex. the class and pacakges.

2) Implementation view - This view consist of the modules which represent packaged code and components which are executable and deployable.

3) Process View - The components at runtime.

4) Deployement - Processes running on machines.

### The Microservice architecture

 - The microservice architecture structures an application as a set of loosely coupled services.

#### Overview of Architecture style

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

#### What is a service?

- A service is a standalone, independently deployable software component that implements some useful functionality.

Every service in a microservice architechture has its own architecture and potentially technology stack.

#### What is loose coupling?

As all interactions happens to the service via the API , which encapsulates the implementation details. This enables the implementation of the service to change without impacting its clients. 





