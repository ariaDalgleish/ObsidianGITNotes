### SOLID Design Principles — Overview

Guidelines for OOP that help eliminate "code smells" by refactoring code to be legible and extensible.

### S — Single Responsibility Principle (SRP)

- A class should have only **one reason to change** / one responsibility
- Example violation: `UserService` handling both `registerUser()` and `sendEmail()` — mixes user logic with email logic
- Fix: split into `UserService` (implements `IUserService`) and `EmailService` (implements `IEmailService`), each responsible for one concern

### O — Open-Closed Principle (OCP)

- Software entities should be **open for extension, but closed for modification**
- Open for extension: add new functionality without altering existing code
- Closed for modification: don't touch what already works
- Achieved via **abstraction and polymorphism** (inheritance/composition)
- Example violation: `calculateVehicle()` using `instanceof` checks (Car, MotorBike) — adding a `Truck` means editing the method
- Fix: define an `IVehicle` interface with `calculateVehicle()`; each vehicle type (Car, MotorBike, Truck) implements its own version — no existing code changes needed to add Truck

### L — Liskov Substitution Principle (LSP)

- Subclasses must be **substitutable for their base class** without breaking correctness
- Subtypes should be _behaviourally_ substitutable, not just structurally
- Classic violation: `Square extends Rectangle`, overriding `setWidth`/`setHeight` to keep both sides equal — breaks client code that assumes width/height are independent (e.g., `assert(rec.area() == 20)` fails)
- Fix: make `Rectangle` and `Square` siblings, both implementing a common `Shape` interface (`area()`)
- Key idea: **design entities by how they behave, not what they "are"**

### I — Interface Segregation Principle (ISP)

- Clients shouldn't be forced to depend on **interfaces (methods) they don't use**
- Keep interfaces small and cohesive ("when more means less")
- Example violation: a single bloated `ATM UI` interface with deposit/withdrawal/transfer/insufficient-funds methods — every UI variant (Speech, Braille, Screen) forced to implement all of them
- Fix: split into separate interfaces — `Deposit UI`, `Withdrawal UI`, `Transfer UI` — so each transaction type only depends on what it needs

### D — Dependency Inversion Principle (DIP)

- High-level modules should not depend on low-level modules — **both should depend on abstractions**
- Abstractions shouldn't depend on details; details should depend on abstractions
- Example violation: `Button` depends directly on concrete `Lamp` class (`TurnOn()`/`TurnOff()`) — can't reuse `Button` for anything else
- Fix: introduce a `Switchable` interface (`activate()`/`deactivate()`); `Button` depends on `Switchable`, and `Lamp` implements it — dependency is "inverted," both now depend on the abstraction

### Summary table

|Letter|Principle|Core idea|
|---|---|---|
|S|Single Responsibility|One class, one job|
|O|Open-Closed|Extend without modifying|
|L|Liskov Substitution|Subclasses must behave correctly in place of base class|
|I|Interface Segregation|Don't force unused methods on clients|
|D|Dependency Inversion|Depend on abstractions, not concrete classes|
