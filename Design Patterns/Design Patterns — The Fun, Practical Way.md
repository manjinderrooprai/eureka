# Design Patterns — The Fun, Practical Way

Think of **design patterns as “proven solutions to common problems”** in software design.
Just like traffic rules—boring to read, invaluable in practice.

We’ll learn them in **3 levels**:

1. What problem it solves (story)
2. How it works (idea)
3. Where you actually use it (real projects)

---

## 1️⃣ Singleton — *“Only One Boss Allowed”*

### Story

Your company has **one CEO**.
If every employee could create their own CEO, chaos.

### Problem

You want **only one instance** of a class across the application.

### Idea

* Private constructor
* One global access point

### Real Usage

* Configuration manager
* Database connection manager
* Logger

### Mental Hook

> “If more than one instance breaks logic → Singleton”

---

## 2️⃣ Factory — *“Don’t Ask How, Just Give Me the Object”*

### Story

You go to a restaurant.
You don’t cook—you just **order food**.

### Problem

Object creation logic becomes messy and tightly coupled.

### Idea

* Move object creation to a **factory**
* Client only asks for what it needs

### Real Usage

* Creating service implementations
* Payment gateway selection (UPI / Card / Wallet)
* Notification providers (Email / SMS / Push)

### Mental Hook

> “If `new` is everywhere → Factory”

---

## 3️⃣ Builder — *“Make It Step by Step”*

### Story

Ordering a custom pizza:

* Size
* Cheese
* Toppings
* Crust

### Problem

Constructors with **too many parameters**.

### Idea

* Build object **step by step**
* Final `build()` creates it

### Real Usage

* Complex DTOs
* HTTP request builders
* Test data builders

### Mental Hook

> “Too many constructor arguments → Builder”

---

## 4️⃣ Strategy — *“Same Task, Different Ways”*

### Story

You travel from office to home:

* Bus
* Cab
* Bike

Same goal, **different strategies**.

### Problem

You want to **change behavior at runtime**.

### Idea

* Encapsulate algorithms
* Switch strategies dynamically

### Real Usage

* Sorting algorithms
* Discount calculation
* Authentication methods

### Mental Hook

> “If `if-else` keeps growing → Strategy”

---

## 5️⃣ Observer — *“You Subscribe, I Notify”*

### Story

You subscribe to a YouTube channel.
Creator uploads → you get notified.

### Problem

Many objects depend on **one object’s state change**.

### Idea

* Observers subscribe
* Subject notifies automatically

### Real Usage

* Event listeners
* UI updates
* Kafka consumers
* Webhooks

### Mental Hook

> “One change → many reactions → Observer”

---

## 6️⃣ Decorator — *“Add Features Without Breaking Things”*

### Story

You buy coffee:

* Coffee
* * Milk
* * Sugar
* * Cream

### Problem

You want to **add behavior dynamically** without changing the class.

### Idea

* Wrap object inside another object
* Add features layer by layer

### Real Usage

* Logging
* Security checks
* Input validation
* Java I/O streams

### Mental Hook

> “Need add-ons without inheritance → Decorator”

---

## 7️⃣ Adapter — *“Plug Converter”*

### Story

Your phone charger doesn’t fit a socket.
You use an **adapter**.

### Problem

Two interfaces don’t match.

### Idea

* Adapter converts one interface to another

### Real Usage

* Legacy system integration
* Third-party APIs
* Data format converters

### Mental Hook

> “Interface mismatch → Adapter”

---

## 8️⃣ Facade — *“One Button, Many Things”*

### Story

You press **‘Start Car’**.
Internally:

* Engine
* Fuel pump
* Sensors
* Electronics

### Problem

Complex subsystem exposed to clients.

### Idea

* Simple interface over complex system

### Real Usage

* Service layer
* SDKs
* APIs

### Mental Hook

> “Too complex to use directly → Facade”

---

## 9️⃣ Proxy — *“Control Access”*

### Story

You can’t directly meet the CEO.
You go through a **PA**.

### Problem

You need **controlled access** to an object.

### Idea

* Proxy acts as a middleman

### Real Usage

* Lazy loading
* Security
* Caching
* Remote calls

### Mental Hook

> “Need access control → Proxy”

---

## 🔟 Command — *“Wrap Action as Object”*

### Story

You press a TV remote button.
Button → command → TV action.

### Problem

You want to **decouple requester from action**.

### Idea

* Encapsulate request as object

### Real Usage

* Undo/Redo
* Job queues
* UI buttons

### Mental Hook

> “Action should be stored or replayed → Command”

---

## 11️⃣ Template Method — *“Same Recipe, Different Flavors”*

### Story

Tea and coffee:

* Boil water
* Brew
* Pour
* Add extras (differs)

### Problem

Algorithm structure is fixed, steps vary.

### Idea

* Base class defines skeleton
* Subclasses customize steps

### Real Usage

* Workflow processing
* Framework hooks

### Mental Hook

> “Common steps + customization → Template”

---

## How to Remember All Patterns Easily

### Group Them:

**Creational**

* Singleton
* Factory
* Builder

**Behavioral**

* Strategy
* Observer
* Command
* Template

**Structural**

* Adapter
* Decorator
* Facade
* Proxy

