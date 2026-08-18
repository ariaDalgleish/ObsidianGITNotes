Object Oriented Analysis
and Design (OOAD)

### Four Key Stages of Software Development

1. **Requirement Analysis** → produces Requirement Specification
2. **System/Program Design** → produces system architecture & diagrams
3. **Implementing the Design** → produces system, requirement/design docs, test cases
4. **Testing**

### Unified Modelling Language (UML)

- **Language**: expresses ideas — NOT a methodology or procedure
- **Modelling**: describes a software system at a high level of abstraction
- **Unified**: UML is a world standard (maintained by the Object Management Group, OMG)
- A **graphical language** for visualising, specifying, constructing, and documenting software artefacts; simplifies complex design and helps gain an overall system view

#### UML Diagram Categories

- **Structure Diagrams** — represent _static_ aspects; document software architecture (e.g. Class, Package, Component, Deployment, Object, Composite Structure diagrams)
- **Behaviour Diagrams** — represent _dynamic_ aspects; describe system functionality (e.g. Use Case, Activity, State Machine diagrams)
- **Interaction Diagrams** — a subset of behaviour diagrams; emphasize flow of control/data between elements (Sequence, Communication, Interaction Overview, Timing diagrams)

### Use-Case Diagrams

- A **use case** = model of interaction between external users (**actors**) and the software product itself
- Depicts who/what interacts with the system; captures user requirements; acts as a **contract** between end users and developers
- Key elements: **System name/boundary**, **Actor** (a role a user plays, human or system), **Use Case** (oval — a set of interaction scenarios incl. alternatives), **Association** (line connecting actor ↔ use case)

#### Relationships in Use-Case Diagrams

|Relationship|Symbol|Meaning|
|---|---|---|
|Association|plain line|communication between actor and use case|
|Generalisation|line + hollow triangle|child use cases (or actors) inherit/modify a parent's common behaviour|
|Include|dashed arrow `<<include>>`|base use case includes another use case's functionality (mandatory subtask)|
|Extend|dashed arrow `<<extend>>`|one use case optionally extends another's behaviour (often with a condition)|

- **Use Case Descriptions**: document detail at two levels
    - **Brief description** — short summary of actor/system interaction
    - **Fully developed description** — most formal method; includes use case name, scenario, triggering event, actors, related use cases, stakeholders, pre/post-conditions, step-by-step actor/system flow of activities, and exception conditions

### Activity Diagrams

- Describe user/system activities, who performs each, and their sequential flow
- Useful for documenting **workflows** of business processes
- **"Activity Diagram for Use Case"**: documents the activity flow for one specific use case, supplementing its use case description
- **Basic symbols**: starting/ending activity (pseudo-nodes), activity (rounded box), transition arrow, decision (diamond, with [yes]/[no] branches), synchronization bars (split/join for parallel flows), **swimlanes** (columns dividing activities by responsible actor/subsystem, e.g. Customer vs System)
- Example (order fulfilment): shows flow across **Order subsystem, Inventory subsystem, Warehouses, Shipping company** swimlanes
- Example (shopping cart): pink ovals represent _other_ use cases invoked mid-flow (e.g. "Search and view accessories")

### Class Design

Steps: recall class diagrams → design classes from the narrative → identify classes/objects → describe attributes & methods → establish relationships → create classes

#### Domain Model vs Design Class Diagrams

- **Domain model class diagram**: models real-world things in the problem domain; used to capture requirements
- **Design class diagram**: used to design actual software classes (includes attributes + method signatures)

#### Identifying Classes and Objects

- Classes/objects are generally identified from **nouns** in the requirements narrative
- Not all nouns become classes — some are just **attributes** of other objects
- A **plural noun** in the spec often signals a needed class (e.g. "products", "users")
- Complex attributes that can't be represented by a primitive value need their **own class** (e.g. an employee's salary with ranks/bounds)

#### Static Variables and Methods

- **Static (class) variable**: one field shared by _all_ instances of a class — changing it via one object changes it for all
- **Static (class) method**: callable via the class name, no instantiation needed (e.g. `Math.sqrt(81)`)

#### Final Classes, Variables, and Methods

- **Final class**: cannot be subclassed
- **Final method**: cannot be overridden/hidden by subclasses (protects critical/consistent behaviour)
- **Final variable**: can only be initialized once (via initializer or assignment); if it's a reference, it can't be re-bound to another object — but the object it points to can still be mutable internally

### Class Relationships

Four main types: **Association, Aggregation, Composition, Generalization/Specialization (inheritance)**

- **Association**: general "uses" relationship — one class's methods invoke another's (e.g. `Driver` uses `Key` to `startEngine()`, without owning it)
- **Aggregation**: a "has-a" relationship — special type of association where an object is made up of other objects, but the parts can exist independently and be swapped (e.g. `Car` holds an `Engine` passed into its constructor, stored in a non-final field)
- **Composition**: a _special, stronger_ form of aggregation — the child **cannot exist independently** of the parent; often implemented via a `final` field created inside the parent's own constructor (e.g. `Car` creates its own `Engine` internally)
- **Generalization/Specialization**: hierarchical relationship (inheritance) — subclasses are subsets of a superclass's objects (e.g. `Sale` → `OnlineSale`, `InStoreSale`, `TelephoneSale`)

### Simple Principles of Designing a Class

- A class = single entity with a set of similar operations (e.g. `String.toUpperCase()`, `String.toLowerCase()`)
- Follow Java naming conventions: `ClassName`, `methodName`, `memberField`
- Use informative names for classes, fields, methods
- Order: data declarations → constructors → methods
- Always provide a constructor and initialize variables to avoid errors

### Recall: Class Design of Tika (layered industrial design pattern)

Three-layer class design pattern common in industrial projects:

1. **Interfaces** (e.g. `Parser`) — define the specification; large interfaces can be split into smaller ones
2. **Abstract classes** (e.g. `Abstract Parser`) — implement the interface(s)
3. **Concrete classes** (e.g. `PDFParser`, `WordPerfectParser`, `HtmlParser`) — extend the abstract class