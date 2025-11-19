# SOLID Principles in Object-Oriented Programming

**SOLID** is an acronym for five object-oriented design principles that help make software easier to maintain, extend,
and understand. These principles encourage loose coupling and high cohesion, meaning components depend on abstractions
and have focused responsibilities. In practice, following SOLID leads to code that is more maintainable, flexible, and
scalable. Each letter in SOLID stands for one principle:

- **S** - Single Responsibility Principle (SRP)
- **O** - Open/Closed Principle (OCP)
- **L**  - Liskov Substitution Principle (LSP)
- **I**  - Interface Segregation Principle (ISP)
- **D**  - Dependency Inversion Principle (DIP)

Together, these guide developers to design classes and interfaces so that each has a clear purpose, changes require
minimal impact on existing code, and dependencies flow toward abstractions

## Single Responsibility Principle (SRP)

**Definition**: A class should have only one reason to change, meaning it should have a single responsibility or job. In
other words, every class or module should focus on one concern

**Conceptual Explanation**: If a class does more than one thing, changes related to one responsibility can break or
complicate the other. By keeping each class focused, the code becomes easier to understand and modify . For example, if
a class handles both business logic and database access, a change in the database layer might force changes in the
business logic code. SRP prevents this by isolating responsibilities. Key benefits include:

- **Maintainability**: Smaller, focused classes are easier to read and update.
- **Testability**: Unit tests can target one behavior at a time.
- **Flexibility**: Changes to one feature have minimal impact on unrelated parts.

**Real-World Example**: Imagine a baker whose sole job is baking bread. Baking is the baker’s single responsibility. If
the baker were also asked to manage inventory, order supplies, serve customers, or clean the bakery, their effectiveness
in baking would suffer. Each of those tasks is a separate job. Assigning them to different roles (inventory manager,
server, cleaner) keeps each person focused – analogous to having one class per responsibility in code.

**Violation (Anti-Pattern)** Example:

```java

@Getter
public class User {
    private String name;
    private String email;

    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    // Violation: This method does two unrelated things
    public void updateEmail(String newEmail) {
        // Change the email
        this.email = newEmail;
        // Send notification (unrelated to updating data)
        sendConfirmationEmail();
    }

    private void sendConfirmationEmail() {
        System.out.println("Email sent to " + email);
    }
}
```

**Adhering to SRP** – Refactored Example

```java

@Getter
@Setter
public class User {
    private String name;
    private String email;

    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }
}

public class EmailService {
    public void sendConfirmationEmail(User user) {
        System.out.println("Email sent to " + user.getEmail());
    }
}
// Now, User only stores user data (one responsibility) and EmailService only handles emailing (another responsibility).

```

## Open/Closed Principle (OCP)

**Definition**: “Software entities should be open for extension, but closed for modification.” This means you should be
able to add new functionality without changing existing code.

**Conceptual Explanation**: Under OCP, once a class or module is tested and working, its code should not need to change
when requirements evolve. Instead of modifying existing code (which risks introducing bugs), you extend behavior through
inheritance, interfaces, or composition. This enables new features to plug in without altering proven logic, keeping the
code base stable over time.

- **Extensibility**: New features can be added by adding new code, not by editing old code
- **Stability**: Reduces risk of breaking existing functionality when adding requirements.
- **Flexibility**: The design can adapt to change easily by using abstractions.

**Violation Example:**

```java
class AreaPrinter {
    public void printArea(Object shape) {
        if (shape instanceof Rectangle) {
            Rectangle r = (Rectangle) shape;
            System.out.println("Area: " + (r.getWidth() * r.getHeight()));
        } else if (shape instanceof Circle) {
            Circle c = (Circle) shape;
            System.out.println("Area: " + (Math.PI * c.getRadius() * c.getRadius()));
        }
        // If we add a Triangle, this class must be modified – violating OCP.
        // Each new shape forces modification of AreaPrinter (not closed for modification). 
        // As the principle notes, this approach prevents the system from scaling easily
    }
}
```

**Adhering to OCP – Refactored Example**:

```java
interface Shape {
    double area();
}

@Getter
class Rectangle implements Shape {
    private int width, height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}

@Getter
class Circle implements Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

class AreaPrinter {
    public void printArea(Shape shape) {
        System.out.println("Area: " + shape.area());
    }
    // Now AreaPrinter.printArea() does not change when new shapes are added. 
    // To support a new shape (e.g., Triangle), simply create a class that implements Shape and defines area(). 
    // No existing code is modified – the code is open for extension (new classes) and closed 
    // for modification (no need to edit AreaPrinter)
}
```

## Liskov Substitution Principle (LSP)

**Definition**: “Objects of a superclass should be replaceable with objects of its subclasses without affecting the
correctness of the program.” In practice, a subclass must fulfill the expectations (the contract) of its base class.

**Conceptual Explanation**: LSP ensures that a subclass can stand in for its parent class without causing errors or
unexpected behavior. This means a subclass should not strengthen preconditions or weaken postconditions of the base
class methods. Methods in a subclass should accept the same inputs and honor the same outputs as defined by the base
class. Following LSP is crucial for reliable polymorphism: code that works with a base class should continue to work if
given an instance of a derived class.

- **Correctness:** Guara ity, so inheritance is sate.
- **Reusability & Polymorphism:** Subclasses can be used interchangeably with base classes, making
  code more flexible and reusable.
- **Predictability:** Replacing a superclass with a subclass won't break client code if LSP is honored

**Violation Example:**

```java
class Animal {
    public void makeSound() {
        System.out.println("Some generic animal sound");
    }

    public void fly() {
        System.out.println("The animal is flying");
    }
}

class Duck extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Quack quack!");
    }

    @Override
    public void fly() {
        System.out.println("Duck is flying with wings");
    }
}

class Ostrich extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Boom boom hiss");
    }

    @Override
    public void fly() {
        throw new UnsupportedOperationException("Ostriches can't fly!");
    }
}
```

**Adhering to LSP – Refactored Example**: Avoid improper inheritance. Instead, define a common interface or use
composition so each class meets its own contract.

```java
// Common things ALL animals can do
abstract class Animal {
    public abstract void makeSound();
}

// Only animals that can actually fly implement this interface
interface Flyable {
    void fly();
}

// Only animals that can swim implement this
interface Swimmable {
    void swim();
}

class Duck extends Animal implements Flyable, Swimmable {
    @Override
    public void makeSound() {
        System.out.println("Quack quack!");
    }

    @Override
    public void fly() {
        System.out.println("Duck is flying with wings");
    }

    @Override
    public void swim() {
        System.out.println("Duck is swimming");
    }
}

class Ostrich extends Animal implements Swimmable {
    @Override
    public void makeSound() {
        System.out.println("Boom boom hiss");
    }

    @Override
    public void swim() {
        System.out.println("Ostrich can swim a little");
    }

    // No fly() method → perfectly fine and expected
    public void runFast() {
        System.out.println("Ostrich runs at 70 km/h!");
    }
}

class Penguin extends Animal implements Swimmable {
    @Override
    public void makeSound() {
        System.out.println("Honk honk!");
    }

    @Override
    public void swim() {
        System.out.println("Penguin swims elegantly");
    }
}
```

## Interface Segregation Principle (ISP)

**Definition**: “Clients should not be forced to depend on interfaces they do not use.” In other words, it’s better to
have many specific interfaces rather than one large general-purpose interface.

**Conceptual Explanation**: ISP addresses the problem of “fat” interfaces. If an interface has methods that a client
class doesn’t need, the client is burdened with irrelevant dependencies. This creates unnecessary coupling and extra
work implementing unused methods. By splitting interfaces into smaller, focused ones, each client only sees the methods
it actually uses. This yields cleaner, more maintainable code and avoids forcing classes to implement no-op or
irrelevant methods.

- **Decoupling**: Reduces unneeded dependencies between classes (more modular code).
- **Clarity**: Clients implement or use only the methods they need.
- **Maintainability**: Smaller interfaces are easier to understand and update.

**Violation Example**:

```java
interface Worker {
    void work();

    void eat();            // Robots don't eat!
}

class Human implements Worker {
    public void work() {
        System.out.println("Human working");
    }

    public void eat() {
        System.out.println("Human eating");
    }
}

class Robot implements Worker {
    public void work() {
        System.out.println("Robot working");
    }

    public void eat() {
        throw new UnsupportedOperationException("Robots don't eat");
        // or empty method → violates ISP
    }
}
```

**Adhering to ISP – Refactored Example:**

```java
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

class Human implements Workable, Eatable {
    // logic
}

class Robot implements Workable {
    // logic
}
```

## Dependency Inversion Principle (DIP)

**Definition** (official wording by Uncle Bob):

1. High-level modules should not depend on low-level modules. Both should depend on abstractions.
2. Abstractions should not depend on details. Details should depend on abstractions.

**In simple terms**: Depend on interfaces/abstract classes, **never** on concrete classes.

**Why it matters**:

- Decouples high-level business logic from low-level details (DB, API, file system, etc.)
- Makes swapping implementations trivial
- Enables easy unit testing with mocks

**Violation Example**: High-level class depends on a concrete class:

```java
class EmailService {
    void send(String msg) { ...}
}

class OrderService {
    private EmailService emailService = new EmailService();  // Hard-coded!

    public void placeOrder() {
        // ... business logic
        emailService.send("Order confirmed");   // Can't send SMS without changing this class
    }
}
```

**Adhering to DIP – Refactored Example**: Introduce an abstraction for the database connection:

```java
interface MessageService {
    void send(String message);
}

class EmailService implements MessageService { ...
}

class SmsService implements MessageService { ...
}

class PushService implements MessageService { ...
}

class OrderService {
    private final MessageService notifier;

    public OrderService(MessageService notifier) {  // Injected
        this.notifier = notifier;
    }

    public void placeOrder() {
        // ... business logic
        notifier.send("Order confirmed");  // Works with Email, SMS, Push, etc.
    }
}
```