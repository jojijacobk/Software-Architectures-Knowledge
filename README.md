   * [Software Architectures](README.md#software-architectures)
      * [Blackboard System](README.md#blackboard-system)
      * [Client Server Model](README.md#client-server-model)
      * [Component Based](README.md#component-based)
      * [Microservice Architecture (MSA)](README.md#microservice-architecture-msa)
         * [Microservice vs Monolithic](README.md#microservice-vs-monolithic)
         * [Microservice vs Component](README.md#microservice-vs-component)
      * [Service Oriented Architecture (SOA)](README.md#service-oriented-architecture-soa)
      * [Event Driven Architecture (EDA)](README.md#event-driven-architecture-eda)
   * [Notes](README.md#notes)
      * [Interface Description Language](README.md#interface-description-language)
      * [Design by Contract (DbC)](README.md#design-by-contract-dbc)


# Software Architectures

[ https://en.wikipedia.org/wiki/Software_architecture]

The following are most reusable software architectures :

## Component Based

-   It is about separation of concerns in a large software into loosely coupled components
-   It encapsulates a set of related functions & data into a component (like an object in OOP)
-   A component is based on an Interface, so that it becomes substitutable
-   It enables Sevice Oriented Architecture (SOA)
-   It helps to establish Event Driven Architecture (EDA), where the components can produce/consume events.

Example of technologies based on components based architecture :

1.  REST in web services 
2.  REACT in javascript
3.  Java EE from Sun
4.  Web components (shadow DOM, html imports etc)

These components adhere to some *Interface Description Language (IDL)* which ensures that the components publicly exhibit an interface to enable interoperability between components.

<u>Related terms :</u>

-   Interface-based programming (**aka** Interface-based architecture) [ https://en.wikipedia.org/wiki/Interface-based_programming] : For example, Eclipse Foundation publishes their interface and most of the Eclipse plugins are developed by third party vendors satisfying the interface contract.
-   Modular programming [ https://en.wikipedia.org/wiki/Modular_programming]
-   Design by contract : for example, phone manufacturers could publish a specification on the charger needed. Hence, any vendors (including the manufacturers) could produce chargers and it works!.
-   Defensive design : for example, socket and plug should be designed defensively so that it is physically impossible to insert a plugin incorrectly in the socket.
-   Microservice architecture

## Microservice Architecture (MSA)

 [ https://en.wikipedia.org/wiki/Microservices]

-   It is like component based architecture. It is a refined form of service oriented architecture. 
-   Each services communicate each other using REST or Interprocess Communication mechanisms such as shared memory.
-   So they are messaging enabled
-   Each services should be automated for CI/CD
-   Easily replaceable
-   It represents a capability like billing service, recommendation service, logistics service, routing service, collaboration service etc.
-   Most common form is Service Mesh style where each service instance is coupled with a reverse proxy, and both the service & reverse-proxy are shared by a container, where the containers are managed by kubernetes.

### Microservice vs Monolithic

**Micorservice Architecture**

-   It is the approach of designing a single application as suite of small services, where
    -   each service is running on its own process
    -   each service communicates to each other using a lightweight mechanism (usually HTTP resources APIs)
    -   each service is independently deployable by fully automated deployment machinery
    -   each service can be scaled individually by adding more instances of that particular service alone instead of entire monolithic application. Hence, resource needed for scaling is optimal
    -   each service has a firm boundary, which allows each service to be written in a different programming language, and also could be done by different teams

**Monolithic Architecture**

-   It is the approach for designing application as a single unit
-   Usually Enterprise applications are built over 3 main parts
    -   View : the HTML/CSS/JS combination to render on browser of display devices
    -   Backend Server : to handles the request/response logic. It handles all the logic to work on a request and deliver response in a single process
    -   DB : to store data. The backend server read/update data on DB. The problem lies here, the server handles all the logic for the application in a monolithic style.
-   Scaling could be done only horizontally by adding up more instances behind a load balancer. Thus to scale only a part of the functionality you still need large resources enough to accommodate a new instance.
-   A change made to small part of application requires the entire monolithic application to be rebuilt and deployed.

### Microservice vs Component

[ https://www.theregister.co.uk/2016/01/06/inside_microservices/]

-   Microservice is a refined form of Component. 
-   Microservices are supposed to run standalone also and it should work just fine. But, components are generally supposed to work within the larger application.   
    Eg: Spell checker feature in Microsoft Word is not a stand alone utility, and it is hence a Component. Had it been a Microservice, it should have been run as a stand alone service and any other process could invoke it to get result.
-   Components are not supposed to be written in any different context than their parent bigger application context - such as another programming language or different OS or different databases that has no relation to the larger application.   
    For example, you don't think that Spell checker feature in Microsoft can be written in a different programming language or run on a different OS different than Microsoft word is built with.
-   You may categorize a few Microservices into components such as Database component,  App server logic component,  Presentation/UI component

## Service Oriented Architecture (SOA)

[ https://en.wikipedia.org/wiki/Service-oriented_architecture]

-   SOA is a general term for Microservice Architecture
-   Most common form of SOA implementation is Webservice SOAP, REST (though other forms such as message passing also do exist)
-   Evolution goes like this : Distributed Computing →  SOA →  SaaS, where SaaS is group of a lot of Microservices. 
-   *Software as a Service (SaaS)* is the current trend of SOA, where each service is a microservice.

## Event Driven Architecture (EDA)

[ https://en.wikipedia.org/wiki/Event-driven_architecture]

-   EDA complements Service Oriented Architecture. Events may trigger the firing up of services in the SOA.
-   An event can be defined as a significant change in the application state
-   Events may be sent as just event notification with not much details about event, or my sent the event itself

Event driven system generally consists of :

-   Event generator : Who monitors application to application and senses a change of state. This change is represented into a technical structure forming the event message.
    -   **Eg:** System monitors
-   Sink (Event Processing Engine) : Who receives the events and triggers corresponding reaction. 
    -   **Eg:** If an event comes as "stock of Product_ID is low", the *Sink* triggers notification to do bulk order of "Product\_ID".
-   Channel : Conduit to transfer event notification from generator to the subscribers. 
    -   **Eg**: Email, TCP/IP network transfer, Flat files read/write (XML, JSON etc)

Event message structure : 

-   Head : Name, timestamp and type of event
-   Body : Technical structured representation of event 

Event processing styles :

-   Simple : events that are directly related to specific measurable condition.
    -   **Eg:** when petrol tank is near empty, show warning in dashboard
-   Stream : continuos stream of all events for real time in flow of information and it's processing 
-   Complex : infer something from a pattern of different events. Figure out a problem by recognizing patterns of different symptoms coming together.

## Blackboard System

[ https://en.wikipedia.org/wiki/Blackboard_(computing)]

-   It begins with a large blackboard with problem specification
-   A group of specialists watching the blackboard for an opportunity to apply their expertise to developing solution.
-   While someone writes on the blackboard with their contribution, that paves way to other specialists to apply their expertise.
-   This repeats until the final solution is derived.

In programming (like AI) this model defines 3 main components :

-   a blackboard : which is a structured global memory containing objects from solution space
-   knowledge sources : specialized modules with their own interpretation
-   a control component : selects, configures and executes modules/knowledge sources

## Client Server Model

[ [https://en.wikipedia.org/wiki/Client–server\_model](https://en.wikipedia.org/wiki/Client–server_model) ]

# Notes

## Interface Description Language

[ https://en.wikipedia.org/wiki/Interface_description_language]

Interface Description language is a specification language used to describe a software component's API.

Example of IDL are :

-   Open API Specification : a standard for REST interface, used by technologies like swagger.
-   WSDL : a standard for SOAP interface
-   JSON Web-Service Protocol (JSON-WSP)

## Design by Contract (DbC)

[ https://en.wikipedia.org/wiki/Design_by_contract]

-   It expects the Caller of the program has strictly followed the **preconditions** such as passing right input data, right type of input etc.
-   It expects the Callee of the method to strictly follow the **postconditions** and **invariants** such as the expected return data is given in right signature.  
    [ https://en.wikipedia.org/wiki/Invariant_(computer_science)]  
    [ https://en.wikipedia.org/wiki/Class_invariant]

Here, each program methods are obliged to strictly follow the guidelines prescribed by the contract. It can be achieved by :

-   Documenting comments in code
-   Running Test Suite

The language which supports DbC provides several assertions to handle the contracts. For example :

-   isNull
-   isArray
-   isEmpty  
    etc

Other languages can include such assertion libraries to handle with contracts within program methods.

## Defensive Design

[ https://en.wikipedia.org/wiki/Defensive_design]

-   It is the practice of planning for contingencies in the planning stage.
-   Murphy's law is the need for a defensive design
-   It is the opposite of Design by contract.
