SOLID: OOPs Design Priciples
Single Responsiblity: A class should have only one reason to change. interface/class defenition with only related props and member functions

Open Closed:Classes should be open for extension, but closed for modifications
Fully good with Liskov's substitution also. If the implementaiton is only for employee type converted to abstract class it solved Open Closed. 
IEmployee, IBonus, Abstract Employee:IEmployee, IBounus, PermenentEmp:Employee, TempEmp:Employee, ContractEmp:IEmployee

Liskov Substitution: S is a subtype of B. Objects of type B may be replaced with object of S. Derived objects must be completely substitutable for their base objects. ObjBase Base = new Derived()
IEmployee, IBonus, Abstract Employee:IEmployee, IBounus, PermenentEmp:Employee, TempEmp:Employee, ContractEmp:IEmployee

Interface Segrigation:No client should be forced to depend on method it does not use. See with printer option and fat interfaces needs to be split to many smaller interfaces.

Dependency Inversion:High level modules should not depend on low-level modules. Both should depend on abstractions. 
public interface IDAL {void Save(Object obj)}
public class DAL:IDAL {public void Save(Object obj){//Save logic}}
public class BLL{private readonly IDAL _dal; 
public BLL(IDAL dal) {
    _dal = dal;
}
public void SavefromClient(object obj) {_dal.Save(obj);}
}
MicroServices:
Monolethic architecutre is like a big container where in all the software components of an application are assembled together and tightly packaged.
-> Large complex applicaiaotn and break the modularity and qulaity compramized
-> Slow development
-> Less productive due to large contanier
-> Frequent deployment complexity due to one big container
-> Unscalable, resources sharing for all components and if we need to add the instance its for all components
-> Unreliable : Tightly coupled app. so one goes down it impact others too
-> Inflexible : Difficult to change the framework or arch as its single big component
Microservices architecture is an architectural style that strucrures an application as a collection of small autonomous services, modelled around a business domain. Each service is a self contained and implements a single business capability. Each microservices is respnsible for its data model and data and communicate between them via api call. They dont share the data structure, but communicate via api.
Management : Responsible for Placing services on nodes. Idtifying failures, rebalancing services across nodes.
Service Discovery : Maintain list of services and which nodes they are located. it enables service look up to find the endpoint of a service.
API Gateway : Entry point for client. API Gateway forward the call to the appropirate services in the backend. API Gateway might aggregate the responses from multiple services and return the aggregated response. 
Fatures of Microservices Architecture:
Small Focused, Loosely coupled, Language Neutral, Bonded Context : Each service does needs to understanded the implementaiton details of other services.
Advantages of Microservices:
Independent developmet, Independent Deployment, Fault Isolution, Mixed Tech stack, Granular scaling
MicroServices Architecture:
Decomposition:
Decompose by business capability:
    Product catalog management, Inventory management, Order management, Delivery management
Decompose by subdomain
    Product catalog, Inventory management, Order management, Delivery management
Self-contained Service
    Self contained services using Saga participent service, CQRS data owner service
Service per team
    Each team is responsible for one or more business functions (e.g. business capabilities). A team owns (has sole responsibility for changing) a code base consisting of one or more modules. 
Data management:
Database per Service : Keep each microservice’s persistent data private to that service and accessible only via its API. A service’s transactions only involve its database.
Shared database: Use a (single) database that is shared by multiple services. Each service freely accesses data owned by other services using local ACID transactions.
Saga:  A saga is a sequence of local transactions. Each local transaction updates the database and publishes a message or event to trigger the next local transaction in the saga. If a local transaction fails because it violates a business rule then the saga executes a series of compensating transactions that undo the changes that were made by the preceding local transactions.
Choreography  Saga: An e-commerce application that uses this approach would create an order using a choreography-based saga that consists of the following steps:
The Order Service receives the POST /orders request and creates an Order in a PENDING state
It then emits an Order Created event
The Customer Service’s event handler attempts to reserve credit
It then emits an event indicating the outcome
The OrderService’s event handler either approves or rejects the Order
Orchestration Saga: An e-commerce application that uses this approach would create an order using an orchestration-based saga that consists of the following steps:
The Order Service receives the POST /orders request and creates the Create Order saga orchestrator
The saga orchestrator creates an Order in the PENDING state
It then sends a Reserve Credit command to the Customer Service
The Customer Service attempts to reserve credit
It then sends back a reply message indicating the outcome
The saga orchestrator either approves or rejects the Order
API Composition: Implement a query by defining an API Composer, which invoking the services that own the data and performs an in-memory join of the results.
CQRS: Define a view database, which is a read-only replica that is designed to support that query. The application keeps the replica up to data by subscribing to Domain events published by the service that own the data.
Domain event: Organize the business logic of a service as a collection of DDD aggregates that emit domain events when they created or updated. The service publishes these domain events so that they can be consumed by other services.
Event sourcing: A good solution to this problem is to use event sourcing. Event sourcing persists the state of a business entity such an Order or a Customer as a sequence of state-changing events. Whenever the state of a business entity changes, a new event is appended to the list of events. It provides an API that enables services to subscribe to events. When a service saves an event in the event store, it is delivered to all interested subscribers.

DMZ or Perimeter Network : Either secure with common firewall or seperate firwall from Internet to DMZ and DMZ to Private network

Proxy (proxy and signle server, caching, security ) and Reverse Proxy (multiple servers, caching, load balancing, Canary deployments are a pattern for rolling out releases to a subset of users or servers. The idea is to first deploy the change to a small subset of servers, test it, and then roll the change out to the rest of the servers.)

Canary deployment is like blue-green, except it's more risk-averse. Instead of switching from blue to green in one step, you use a phased approach. With canary deployment, you deploy a new application code in a small part of the production infrastructure. 

Docker:
docker build -t console101 .
docker images
docker run console101
docker run -p 8080:80 console101
docker ps - show list of running containers
docker stop <containerid>
docker push console101
sudo docker --version 
sudo docker run -p 8080:80 consoler101 - Use tag run the docker image in different machine
sudo docker ps

Http Error Codes:
Informational responses (100–199),
Successful responses (200–299),
Redirects (300–399),
Client errors (400–499),
and Server errors (500–599).
400 Bad Request. ...
401 Unauthorized. ...
403 Forbidden. ...
404 Not Found. ...
500 Internal Server Error. ...
502 Bad Gateway. ...
503 Service Unavailable. ...
504 Gateway Timeout.

HTTP defines a set of request methods to indicate the desired action to be performed for a given resource. Although they can also be nouns, these request methods are sometimes referred to as HTTP verbs.
GET
The GET method requests a representation of the specified resource. Requests using GET should only retrieve data.
HEAD
The HEAD method asks for a response identical to that of a GET request, but without the response body.
POST
The POST method is used to submit an entity to the specified resource, often causing a change in state or side effects on the server.
PUT
The PUT method replaces all current representations of the target resource with the request payload.

DELETE
The DELETE method deletes the specified resource.
CONNECT
The CONNECT method establishes a tunnel to the server identified by the target resource.

OPTIONS
The OPTIONS method is used to describe the communication options for the target resource.
TRACE
The TRACE method performs a message loop-back test along the path to the target resource.

PATCH
The PATCH method is used to apply partial modifications to a resource.
