### 1.How many features does Java have?

> Key modern Java features (Java 21+) include:

1. **Platform Independent** – “Write once, run anywhere” via JVM bytecode.
2. **Object-Oriented** – Strong encapsulation, inheritance, and polymorphism.
3. **Simple and Familiar** – Minimal low-level constructs like pointers or manual memory management.
4. **Secure** – ClassLoader and bytecode verifier ensure safe runtime execution.
5. **Robust** – Strong type checking, exception handling, and memory safety.
6. **Multithreaded** – Native support for concurrency with threads, executors, and virtual threads (since Java 21).
7. **High Performance** – JIT compilation, adaptive optimizations, and GraalVM integration.
8. **Distributed** – Built-in support for RMI and networked applications.
9. **Dynamic** – Runtime class loading, reflection, and module system (JPMS).
10. **Scalable and Modern** – Features like records, pattern matching, sealed classes, and Loom’s virtual threads
    improve developer productivity and runtime efficiency.

---

### 2.What is a Compiler?

> A compiler translates Java source code into platform-independent bytecode (`.class` files).
> In Java, the **`javac` compiler** converts `.java` files into **bytecode**, an intermediate representation executed by
> the JVM. This design
> separates compilation from execution, enabling portability across operating systems.  
> Compilation includes lexical analysis, syntax checking, semantic validation, and bytecode generation optimized for JVM
> interpretation and JIT compilation.
---

### 3.What is an Interpreter?

> An interpreter in Java is the JVM component responsible for executing compiled bytecode instructions dynamically,
> line by line, by translating them into machine-level operations. This mechanism allows Java programs to be
> platform-independent —
> the same `.class` file can run unmodified across operating systems and hardware architectures.
---

### 4. What is JDK?

> The JDK includes the **JRE (Java Runtime Environment)**, the **Java compiler (javac)**, and development tools like
`javadoc`, `jar`, `javap`, `javac` `jshell` and debugging utilities.  
> It provides everything needed to build and package Java programs — from source code compilation to bytecode execution
> on
> the JVM.
---

### 5. What is JLS?

> The JLS is a **technical specification** that dictates how Java code must behave — covering type system, syntax,
> generics, memory model, and language rules.  
> It ensures all Java compilers and JVM implementations behave consistently across platforms.  
> Every Java version (e.g., JLS 21) comes with an updated JLS that reflects language changes such as records, pattern
> matching, or switch expressions.
---

### 6. What is JRE?

> It includes the **JVM**, **core class libraries**, and **runtime support files**, but **not** development tools like
> the compiler.  
> The JRE is responsible for executing compiled Java bytecode in a consistent, platform-independent way.
---

### 7. What is JVM?

> The JVM is the execution engine of the Java platform — responsible for running bytecode safely and efficiently across
> any hardware.
> It processes bytecode, the platform-independent output of Java compilation, through a layered architecture that
> includes
> class loading, memory management, and an execution engine.
> Modern JVMs combine interpreter and JIT compilation with sophisticated GC algorithms, making Java applications both
> portable and high-performance.
---

### 8. What is Bytecode?

> Bytecode is the intermediate representation of compiled Java programs — an abstract instruction set executed by the
> JVM.  
> It enables platform independence by decoupling compilation from hardware.  
> Before execution, the JVM verifies bytecode for security and translates it into optimized native code at runtime.
---

### 9. What is a Token?

> A token is the smallest meaningful unit in Java source code recognized by the compiler during lexical analysis.
---

### 10. How many types of Tokens are there in Java?

> Tokens are the smallest lexical units that make up Java source code.  
> The compiler recognizes five categories:

1. **Keywords** – Reserved words defining Java syntax (`class`, `if`, `while`, `return`, etc.).
2. **Identifiers** – User-defined names for variables, methods, classes, etc.
3. **Literals** – Fixed values like numbers, characters, strings, or booleans.
4. **Operators** – Symbols that perform operations (`+`, `-`, `*`, `/`, `=`, `==`, etc.).
5. **Separators** – Punctuation symbols used to structure code (`;`, `,`, `()`, `{}`, `[]`).

---

### 11. What is a Character Set in Java?

> A character set defines the collection of valid characters that Java source code can use.
> Java’s character set is based on Unicode, providing global language support and consistent representation across
> systems.
---

### 12. What are Identifiers and what are their rules?

> Identifiers are names given to classes, variables, methods, packages, or other elements in Java code.
> **Rules for identifiers:**

1. Must begin with a **letter**, **currency symbol ($)**, or **underscore (_)**.
2. Subsequent characters can include digits (0–9).
3. Cannot start with a digit.
4. Cannot be a **Java keyword** or **reserved literal** (`true`, `false`, `null`).
5. Are **case-sensitive** (`Count` ≠ `count`).
6. No whitespace or special symbols (like `@`, `#`, `%`).

---

### 13. How many types of comments are there in Java?

> Java supports **three types of comments** — single-line, multi-line, and documentation comments.
---

### 14. How many types of variables are there in Java?

> Java defines **three main types of variables** — **Local**, **Instance**, and **Static (Class)** variables.

- **Local Variables** – Declared within a method, constructor, or block; exist only during that execution scope.
- **Instance Variables** – Declared inside a class but outside any method; each object has its own copy.
- **Static (Class) Variables** – Declared with the static keyword; shared across all instances of the class.

---

### 15. What is the difference between Primitive and Non-Primitive (Instance) types in Java?

> - **Primitive types** are built-in data types that hold simple, immutable values such as numbers, characters, or
    booleans.  
    Examples: `int`, `boolean`, `char`, `double`, etc.  
    These are stored directly on the **stack** for fast access.

> - **Non-primitive types** (also known as **reference** or **instance** types) refer to objects or arrays created from
    classes.  
    Examples: `String`, `Integer`, `List`, `User`, etc.  
    They are stored in the **heap**, with the variable holding only a **reference** (memory address) to the object.
---

### 16. What is Variable Scope?

> Scope determines **visibility** and **lifetime** of variables.  
> A variable can only be accessed within the block or method where it is declared.  
> Outside that scope, it is undefined and cannot be referenced.
---

### 17. How many types of scopes are there in Java?

> 1. **Local Scope:**  
     Variables declared inside a method, constructor, or block.  
     They exist only during the method's execution and are destroyed when the method finishes.
> 2. **Instance Scope:**
     Variables declared inside a class but outside any method or constructor. Each object has its own copy of these
     variables.
> 3. **Static (Class) Scope:**
     Variables declared with the static keyword.
     Shared across all instances of the class and belong to the class itself.
---

### 18. How many types of data types are there in Java?

> 1. **Primitive Data Types (8 types):**  
     Built-in types representing raw values stored directly in memory (stack).  
     These are **not objects** and have fixed sizes.

- **Numeric:**
    - **Integral:** `byte`, `short`, `int`, `long`
    - **Floating-point:** `float`, `double`
- **Non-numeric:**
    - **Character:** `char`
    - **Boolean:** `boolean`

| Type    | Size (bits)       | Default Value |
   |---------|-------------------|---------------|
| byte    | 8                 | 0             |
| short   | 16                | 0             |
| int     | 32                | 0             |
| long    | 64                | 0L            |
| float   | 32                | 0.0f          |
| double  | 64                | 0.0d          |
| char    | 16                | '\u0000'      |
| boolean | 1 (JVM-dependent) | false         |

> 2. **Non-Primitive (Reference) Data Types:**  
     Represent objects or references to data in the heap.  
     They store the **memory address** of the object rather than the value itself.  
     Examples:
     - **String**
     - **Arrays**
     - **Classes**
     - **Interfaces**
     - **Enums**
     - **Records** (Java 16+)
---

### 19. What is an Operator in Java?

> An operator is a symbol that performs an operation on operands (variables or values).
---

### 20. How many types of Operators are there based on the number of operands?

> There are **three** types — **Unary**, **Binary**, and **Ternary** operators.

- **Unary:** Operates on a single operand.
- **Binary:** Operates on two operands.
- **Ternary:** Operates on three operands (only one in Java: `?:`).

---

### 21. What is a Unary Operator?

> A unary operator acts on a single operand to perform increment, decrement, negation, or logical inversion.
---

### 22. What is a Binary Operator?

> A binary operator operates on two operands to perform arithmetic, comparison, logical, or bitwise operations.
---

### 23. What is a Ternary Operator?

> It’s a conditional operator that evaluates a Boolean expression and returns one of two values.
---

### 24. What is an if statement?

> The if statement executes a block of code when a specified Boolean condition is true.
---

### 25. What is a Loop?

> A loop repeatedly executes a block of code until a condition becomes false.
---

### 26. How many types of Control Flow exist in Java?

> Java supports three main control flow types — Sequential, Selection, and Iteration (plus Jump statements).

- **Sequential** – Default top-to-bottom execution.
- **Selection** – Conditional branching (if, switch).
- **Iteration** – Repetition (for, while, do-while).
- **Jump** – Alter flow (break, continue, return).

---

### 27. What is the purpose of the Unicode system?

> Unicode provides a universal character encoding standard supporting all written languages.
---

### 28. What is the difference between a Function and a Method?

> In Java, every function must be defined inside a class — hence, it’s called a **method**.  
> A function (in general programming) can exist standalone, but Java’s object-oriented model doesn’t allow top-level
> functions
---

### 29. What is a Method Definition?

> A **method definition** provides the complete implementation of a method — including the declaration and body.
---

### 30. What is a Method Declaration (header)?

> The method declaration (or header) specifies the modifiers, return type, method’s name, and parameters — but not its
> body.
---

### 31. What is a Method Signature?

> A method signature consists of the method name and its parameter types (order and count).
---

### 32. What is a Stack?

> Each thread in Java has its own **JVM stack**, created when the thread starts.  
> It operates in a **LIFO (Last In, First Out)** manner — every method call pushes a new frame, and returning from the
> method pops that frame.  
> It is used for:

- Storing local variables and primitive values
- Tracking method call order and return addresses
- Managing function parameters

---

### 33. What is a Stack Frame?

> A **stack frame** is a memory block within the JVM stack created for each method invocation.
> Each stack frame contains:

- **Local Variable Array** – stores parameters and local variables
- **Operand Stack** – used for intermediate expression evaluation
- **Frame Data** – includes method metadata, constant pool reference, and return address

> When a method is called, a new frame is pushed; when it returns, the frame is popped.  
> The JVM uses these frames to manage method execution state efficiently.
---

### 34. What is Recursion?

> **Recursion** is the process where a method calls itself directly or indirectly until a base condition is met.
---

### 35. What is a String in Java?

> A **String** in Java is an immutable sequence of characters represented by the `java.lang.String` class.
> It supports efficient text manipulation, comparison, and storage, with immutability providing safety and
> predictability
> in multi-threaded and security-sensitive environments.
---

### 36. In how many ways can we create a String in Java?

> There are two primary ways to create a String — using string literals or the new keyword.

```java
// literal
String s1 = "Hello";

// new keyword
String s2 = new String("Hello");
```

---

### 37. Why is String immutable in Java?

> Strings are immutable for security, thread-safety, and performance (interning) reasons.

- **Security:** Prevents malicious modification of strings used in class loading, file paths, or network connections.
- **Caching & Interning:** Enables JVM to reuse common string literals safely.
- **Thread-safety:** Immutable objects can be shared without synchronization.
- **HashCode stability:** Allows strings to be cached safely in collections like HashMap and HashSet.

---

### 38. What is an Array?

> An Array in Java is a fixed-size, ordered collection of elements of the same type, stored in contiguous memory.
---

### 39. Can we change the size of an Array after it is created in Java?

> No, arrays in Java have a fixed size once created.
> This immutability allows the JVM to perform optimized bounds checking and memory layout decisions.
---

### 40. Can we assign a negative number as an Array size?

> No, using a negative number as an array size throws `NegativeArraySizeException`.
---

### 41. Can we declare an Array without specifying its size?

> You can declare an array without specifying its size, but you must define the size before using it.
---

### 42. Where is an Array stored in JVM memory?

> Arrays are stored in the heap area of JVM memory. An array’s reference lives on the stack (in the method frame),
> while its actual data structure resides on the heap.
---

### 43. What are the advantages and disadvantages of Arrays?

> Advantages:
> Constant-time access (O(1)) by index.
> Cache-friendly due to contiguous memory layout.
> Simple and low-overhead structure.
> Useful for fixed-size, performance-critical data.

> Disadvantages:
> Fixed length — cannot grow or shrink.
> Inefficient insertions/removals (require shifting elements).
> No built-in methods for search, sorting, or resizing.
> Type homogeneity limits mixed-type usage.
---

### 44. What is the String Constant Pool in Java?

> The String Constant Pool (SCP) is a special memory area in the heap
> where Java stores unique string literals to optimize memory and performance.
> The String Constant Pool is a heap-based memory optimization that ensures identical string literals are stored only
> once.
> It improves both memory efficiency and equality performance by enabling reference reuse across the JVM.
---

### 45. Why does Java use String literals?

> Java uses string literals for efficient memory management and faster runtime behavior.
> Through the String Constant Pool and immutability, literals provide safe, shared, and memory-optimized string
> instances
> reused across the JVM,
> making them fundamental to Java’s performance model and class metadata handling.
---

### 46. Is String thread-safe?

> Yes, `String` is thread-safe because it is immutable.
> Once created, a `String` object’s value cannot be changed.  
> All operations that appear to modify a string actually create a new instance, ensuring that no two threads can alter
> the
> same object’s internal state.  
> This makes it inherently safe to share across threads without synchronization.
---

### 47. What are the disadvantages of the String class?

> Strings are immutable, which can cause performance and memory overhead in certain cases.
> Each string modification (e.g., concatenation) creates a new `String` object, increasing garbage generation.  
> For heavy text manipulation, this can lead to unnecessary heap churn.  
> Additionally, `String` consumes more memory than primitive arrays due to object headers and character encoding.
---

### 48. Is String a wrapper class?

> `String` is not a wrapper class; it’s a core reference type for text handling, distinct from primitive wrappers that
> provide object representations of basic types.
---

### 49. What is the purpose of the intern() method in String?

> When called, `intern()` checks the pool for an equivalent string.  
> If present, it returns the pooled reference; otherwise, it adds the current string to the pool.  
> This improves memory efficiency and allows equality comparison using `==`.
---

### 50. What is DRY?

> **DRY** stands for *Don’t Repeat Yourself* — a software principle aimed at reducing duplication.
> In large systems, DRY reduces cognitive load and defect propagation by ensuring single sources of truth.  
> It applies not just to code but also to infrastructure, configuration, and documentation.
---

### 51. What is KISS?

> **KISS** stands for *Keep It Simple, Stupid* — a design principle promoting simplicity.
> KISS reminds engineers to prefer simple, clear, and direct solutions over overly complex ones — ensuring long-term
> maintainability and resilience.
---

### 52. What is YAGNI?

> **YAGNI** stands for *You Aren’t Gonna Need It* — a principle discouraging speculative features.
> YAGNI advises implementing only the features currently required — deferring speculative work until there is proven
> need.  
> This keeps systems lean, maintainable, and aligned with actual user value.
---

# MODULE - 2

### 53. What are Programming Paradigms and what types are there?

> A paradigm represents an approach to organizing logic and data flow in programs.  
> Each paradigm provides a distinct way to express computation — influencing design, maintainability, and concurrency
> behavior.  
> Common paradigms include:

- **Procedural Programming** — focuses on functions and procedures.
- **Object-Oriented Programming (OOP)** — models software as interacting objects.
- **Functional Programming (FP)** — emphasizes pure functions and immutability.
- **Reactive Programming** — focuses on asynchronous data streams and event propagation.
- **Declarative Programming** — describes *what* should happen, not *how*.
- **Logic Programming** — defines rules and relationships, e.g., in Prolog.

---

### 54. What is Procedural Programming?

> Procedural programming is a paradigm based on organizing code into reusable procedures or functions.
> In procedural models, the focus is on *how* to perform tasks, often with global state management.  
> Java supports this via static methods and sequential execution patterns, though OOP typically dominates Java
> applications.
---

### 55. What is OOP (Object-Oriented Programming)?

> Object-Oriented Programming organizes software around interacting objects rather than procedures.  
> By modeling real-world relationships and promoting encapsulation, OOP improves modularity, extensibility, and code
> reuse — making it Java’s primary paradigm.

---

### 56. What is Functional Programming?

> Functional programming treats computation as the evaluation of pure functions without mutable state or side effects.
> Functional programming in Java promotes declarative, side-effect-free logic.  
> By combining lambdas, immutability, and stream-based transformations, it produces concise, parallel-friendly, and
> maintainable code aligned with modern multi-core design.
---

### 57. What is Reactive Programming?

> Reactive programming is a paradigm focused on asynchronous, non-blocking, event-driven data streams.
> It models data as continuous streams that propagate changes automatically — enabling systems to react to updates in
> real time.  
> Core concepts include:

- **Observable streams** — sequences of events over time.
- **Backpressure** — controlling flow between producers and consumers.
- **Non-blocking IO** — efficient resource usage.
- **Event propagation** — automatic updates on data changes.

---

### 58. What are the concepts of OOP?

> OOP concepts define how software models real-world entities through objects and their interactions.
> The core concepts include:

- **Class** — blueprint or template for creating objects.
- **Object** — instance of a class containing state and behavior.
- **Encapsulation** — hiding internal details from external access.
- **Abstraction** — exposing only essential features.
- **Inheritance** — deriving new classes from existing ones for reuse.
- **Polymorphism** — enabling a unified interface for multiple implementations.

---

### 59. What are the main pillars of OOP?

> The four main pillars of OOP are **Encapsulation**, **Abstraction**, **Inheritance**, and **Polymorphism**.

- **Encapsulation** — protects object integrity by restricting direct access to fields.
- **Abstraction** — defines essential behavior while hiding implementation details.
- **Inheritance** — enables class hierarchies and behavior reuse.
- **Polymorphism** — allows objects of different types to be treated uniformly via interfaces or base classes.

---

### 60. What is a Class?

> A class is a blueprint that defines the structure and behavior of objects.
> It specifies fields (state) and methods (behavior) shared by all its instances.  
> Classes can also include constructors, nested types, and access modifiers to control visibility and inheritance.  
> They represent static definitions until instantiated into runtime objects.
---

### 61. What is an Object?

> An object is a runtime instance of a class containing specific data and behavior.
> Internally, each object holds a header (with hash, synchronization info, and class reference) and its data fields.  
> The `Klass` pointer links the object to its class metadata for method resolution and type checks.
> Objects are allocated on the heap and consist of:

- **State:** represented by field values.
- **Behavior:** implemented through methods.

> Each object operates independently but follows the same class definition.

---

### 62. What is a Method?

> A method defines a block of code representing a behavior or operation within a class.
> It enables logic encapsulation, reuse, and polymorphic behavior — forming the behavioral foundation of OOP systems.
---

### 63. What is a Field?

> A field is a variable defined within a class that represents the state of an object.
> In memory, instance fields are stored within the object’s heap layout, while static fields reside in the class
> metadata area.  
> The JVM ensures alignment and efficient access through field offset calculations performed during class loading.

> A field defines an object’s state within its class, stored in the heap or class area depending on its type.  
> Fields, together with methods, form the complete structural and behavioral blueprint of any Java object.
---

### 64. What is a Constructor used for?

> A constructor initializes an object’s state when it is created.
> Constructors are special methods invoked automatically during object creation using the `new` keyword.  
> They set up initial values for fields and ensure the object is in a valid state before use.  
> Constructors cannot have a return type and must share the same name as the class.
---

### 65. What types of Constructors exist?

> - **Default Constructor** – Automatically generated by the compiler when no constructors are defined.
> - **No-Arg Constructor** – Explicitly defined by the developer without parameters.
> - **Parameterized Constructor** – Accepts parameters to initialize object fields.
> - **Copy Constructor** – Creates a new object by copying another object’s state.
> - **Chaining Constructor** – Calls another constructor within the same class (`this()`) or parent class (`super()`),
    enabling reuse of initialization logic.
> - **Compact Constructor (Records only)** – Simplified constructor in Java Records used for validation or normalization
    without redefining parameters.

---

### 66. If we create a constructor manually, will the class still have a default constructor?

> Java automatically provides a no-argument constructor only when no other constructors exist.  
> If you define at least one constructor manually, the compiler does not create a default one — it must be added
> explicitly if needed.
---

### 67. When is a Constructor called?

> A constructor is called automatically when a new object is created.
> During `new` object creation, the JVM allocates memory, sets default values, and then calls the constructor to perform
> initialization.  
> Constructors are invoked only once per object lifetime and cannot be called explicitly like regular methods.
---

### 68. Can a class have multiple constructors?

> Yes, Java allows multiple constructors through overloading.
> A class can define multiple constructors with varying parameters, known as constructor overloading.  
> This pattern enhances flexibility by supporting multiple initialization paths while keeping object creation concise
> and
> maintainable.
---

### 69. What is a Default Constructor?

> A default constructor is a no-argument constructor automatically generated by the compiler when no constructors are
> explicitly defined.
---

### 70. What is a No-Arg Constructor?

> A no-arg constructor is a user-defined constructor with no parameters.  
> It allows controlled initialization while maintaining default call order to the superclass constructor.
---

### 71. What is a Parameterized Constructor?

> A parameterized constructor accepts arguments to initialize object fields with specific values.
> It allows creating objects in pre-defined states by passing parameters during instantiation.  
> This improves flexibility and clarity, ensuring required data is available at object creation time.
---

### 72. What is a Copy Constructor?

> A copy constructor creates a new object by copying the state of another object of the same class.
> by passing same type of object to constructor params.
---

### 73. What is a Chaining Constructor?

> A chaining constructor calls another constructor within the same class or its superclass to reuse initialization
> logic.
> A chaining constructor reuses initialization logic by invoking another constructor (`this()` or `super()`), ensuring
> hierarchical and maintainable object initialization across inheritance and overloaded constructors.
---

### 74. What is a Compact Constructor?

> compact constructor is a special constructor syntax used in Java records to validate or transform constructor
> arguments.
> The compiler automatically assigns constructor parameters to record fields before executing the compact constructor
> body.  
> This eliminates boilerplate while ensuring that records remain final and immutable with consistent state enforcement.
---

### 75. What is Encapsulation?

> Encapsulation is the OOP principle of bundling data (fields) and behavior (methods) into a single unit while
> restricting direct access to internal state.
> It ensures that the internal representation of an object is hidden from the outside world.  
> Objects expose controlled access through public methods instead of allowing direct modification of fields.
---

### 76. Why is it called Data Hiding?

> “Data Hiding” refers to the practice of restricting access to class fields using access modifiers like `private`.  
> External classes can only interact with the data through public methods, ensuring that the internal state cannot be
> changed arbitrarily or incorrectly.
---

### 77. How do we achieve Encapsulation?

> By making fields private and providing controlled access via public getter and setter methods.
---

### 78. What are the advantages of Encapsulation?

> Key advantages include:

- **Data protection** – prevents invalid or inconsistent state.
- **Ease of maintenance** – internal changes don’t affect external code.
- **Reusability** – encapsulated components can evolve independently.
- **Improved abstraction** – hides implementation complexity.
- **Enhanced testing** – promotes predictable and controlled behavior.

---

### 79. What is the purpose of Getter and Setter methods?

> They act as an interface between an object’s internal data and the outside world.  
> Getters retrieve field values, while setters validate or transform inputs before updating the field.  
> They preserve encapsulation while allowing flexibility for validation, logging, or transformation logic.
---

### 80. Why do we need Packages?

> Packages organize related classes and interfaces into namespaces, improving modularity, readability, and access
> control.
> They prevent naming conflicts between classes, structure large codebases logically, and control visibility using
> access modifiers (`public`, `protected`, package-private).  
> Packages also define modular boundaries for APIs, allowing selective exposure of classes while hiding internal
> implementations.
---

### 81. What are Package members?

> Package members are classes, interfaces, enums, and annotations declared within a package.
> In the JVM, each package member is a separate `.class` file under the package directory.  
> Access control is enforced during class loading, ensuring package-private types and members are visible only within
> the
> same package boundary.
---

### 82. What is Inheritance?

> Inheritance is an OOP mechanism that allows one class to acquire the properties and behaviors of another class.
> It enables code reuse and hierarchical classification by letting a subclass extend a superclass.  
> The subclass inherits accessible fields and methods, and it can override or extend them to provide specialized
> behavior.  
> This forms an “is-a” relationship between classes.
---

### 83. Why do we need Inheritance?

> To promote code reuse, consistency, and polymorphism across related classes.
> We use inheritance to reuse logic, maintain consistent interfaces across hierarchies, and enable polymorphism — key
> for extensible and maintainable system architectures.
---

### 84. What are the types of Inheritance?

> Java supports single, multilevel, hierarchical, and hybrid inheritance (via interfaces).

1. **Single Inheritance** – One class extends another (`class B extends A`).
2. **Multilevel Inheritance** – A class extends a subclass of another class (`C extends B extends A`).
3. **Hierarchical Inheritance** – Multiple classes share a common parent (`B extends A`, `C extends A`).
4. **Hybrid Inheritance** – Combination of multiple inheritance types achieved using interfaces.

---

### 85. Can we use multiple inheritance in Java?

> No, Java does not support multiple inheritance with classes — only through interfaces.
> To avoid the **diamond problem**, where ambiguity arises from inheriting the same method from multiple parents, Java
> restricts classes to single inheritance.  
> Interfaces provide a safe alternative, allowing multiple inheritance of type but not state.
---

### 86. What are Superclass and Subclass?

> A **Superclass** is a parent class whose properties and behaviors are inherited by other classes.

> A **Subclass** is a child class that extends the superclass and can override or add new functionality.
---

### 87. What does a Subclass inherit from a Superclass?

> A subclass inherits all accessible fields, methods, and nested types from its superclass except private members and
> constructors.
> The subclass gains:

- **Public and protected fields/methods** – directly accessible.
- **Package-private members** – accessible only if in the same package.
- **Inherited behavior** – can be overridden to provide custom logic.
-

> What it **does not inherit**:

- Private members.
- Constructors.
- Static initializers and blocks (executed per class).

---

### 88. What is a Cosmic class?

> The **Cosmic class** refers to `java.lang.Object`, the root class of all classes in Java.
> Every class in Java implicitly extends `Object` (directly or indirectly).  
> It provides the base behavior and structure common to all Java objects.  
> This makes `Object` the ancestor of all reference types in the JVM, ensuring uniform operations like comparison,
> synchronization, and identity.
---

### 89. What methods does the Cosmic class (Object) have?

- **`public final Class<?> getClass()`** – returns the runtime class of the object.
- **`public int hashCode()`** – returns the object’s hash value.
- **`public boolean equals(Object obj)`** – compares object equality.
- **`protected Object clone()`** – creates a shallow copy (if `Cloneable`).
- **`public String toString()`** – returns a string representation.
- **`protected void finalize()`** *(deprecated)* – called before GC (no longer recommended).
- **`public final void wait()` / `wait(long)` / `wait(long, int)`** – thread synchronization methods.
- **`public final void notify()` / `notifyAll()`** – notifies waiting threads.

---

### 90. Why do we need Access Modifiers?

> Access modifiers define the visibility and accessibility of classes, methods, and fields in Java.
> They control how program components interact, enforcing encapsulation and modularity.  
> By restricting access, developers can protect internal logic, prevent misuse, and design clean, maintainable APIs.  
> Access modifiers are essential for secure and predictable object-oriented design.
---

### 91. What are the types of Access Modifiers? Define each.

1. **public** – Accessible from anywhere in the application.
2. **protected** – Accessible within the same package and by subclasses (even in different packages).
3. **default (package-private)** – Accessible only within the same package; no keyword used.
4. **private** – Accessible only within the same class.

---

### 92. Can we create a Private Constructor? What is its purpose?

> Yes, a class can have a private constructor to restrict direct instantiation.
> Private constructors are commonly used in:

- **Singleton patterns** – to prevent multiple object creation.
- **Static utility classes** – to prevent instantiation.
- **Factory methods** – when object creation is controlled externally.

> They enforce controlled object creation and encapsulate instantiation logic.

---

### 93. Which Access Modifiers can be used with classes?

> Only **public** and **default (package-private)** modifiers are allowed for top-level classes.
> - **public** – The class is visible from any package.
> - **default (no modifier)** – The class is visible only within the same package.  
    Nested (inner) classes, however, can use **private** and **protected** as well, since they exist within another
    class’s scope.

---

### 94. Where is the Private Modifier used, and what does it allow access to?

> `private` is used to restrict access to members within the same class only.
> Private members (fields, methods, constructors, or inner classes) are inaccessible outside their defining class.  
> This ensures strict encapsulation and prevents unintended external modifications.  
> It is fundamental for maintaining object integrity and secure internal behavior.
---

### 95. What types of relationships exist between Classes?

> Classes in Java can have three main relationships: **Is-A**, **Has-A**, and **Uses-A**.

- **Is-A (Inheritance)** – defines a superclass–subclass relationship.
- **Has-A (Composition/Aggregation)** – defines ownership or containment.
- **Uses-A (Dependency)** – defines a temporary or functional relationship where one class depends on another.

> These relationships represent different levels of coupling.  
> Inheritance creates strong coupling via the class hierarchy, while composition and dependency promote looser coupling,
> improving maintainability and testability.

---

### 96. Where is the “Uses-A” relationship used?

> The **Uses-A** relationship is used when one class depends on another to perform a specific task.
> It typically appears as a **method-level dependency**, where a class creates, receives, or calls methods of another
> class temporarily without storing it as a field.  
> This is common in utility, service, or helper class interactions.
---

### 97. Where is the “Has-A” relationship used?

> A **Has-A** relationship is used when one class contains or owns another class as a field.
> It represents a **whole–part** relationship, typically modeled via fields (instance variables).  
> For example, a `Car` has an `Engine`.  
> This enables modular and reusable designs, supporting both **composition** and **aggregation** forms.

---

### 98. Where is the “Is-A” relationship used?

> The **Is-A** relationship is used to model inheritance or type hierarchy.
> It expresses that a subclass is a specialized form of its superclass (e.g., `Dog is a Animal`).  
> This allows polymorphism — objects of the subclass can be treated as instances of the superclass type.
> The JVM represents Is-A relationships through class metadata and vtable inheritance.  
> Type checks (`instanceof`, method dispatch) rely on the Is-A hierarchy for runtime behavior consistency.
---

### 99. Which keywords are used to achieve the “Is-A” relationship?

- **`extends`** – used for class inheritance (one class inherits another).
- **`implements`** – used for interface inheritance (class implements interface).

> Both create Is-A relationships, enabling polymorphic behavior and type substitution.

---

### 100. What are the types of “Has-A” relationships?

- **Composition** – strong ownership; the contained object’s lifecycle depends on the container.
- **Aggregation** – weak ownership; the contained object exists independently of the container.

> Both represent structural containment but differ in lifecycle dependency.

---

### 101. What are the differences between Composition, Aggregation, and Association?

> All are object relationships, but differ in ownership and lifecycle control.

| Relationship    | Ownership        | Lifecycle Dependency | Example                     |
 |-----------------|------------------|----------------------|-----------------------------|
| **Association** | No ownership     | Independent          | A teacher works in a school |
| **Aggregation** | Weak ownership   | Independent          | A department has professors |
| **Composition** | Strong ownership | Dependent            | A car has an engine         |

- **Association** – general connection without ownership.
- **Aggregation** – has-a relationship with shared object lifecycle.
- **Composition** – has-a relationship with dependent object lifecycle.

---

### 102. What is Polymorphism?

> Polymorphism is the ability of an object to take multiple forms and behave differently based on its runtime type.
> It allows methods with the same name to perform different behaviors depending on the object invoking them.  
> Polymorphism promotes flexibility and extensibility in software design.
---

### 103. What are the types of Polymorphism?

> Java supports two main types of polymorphism: **Static (Compile-time)** and **Dynamic (Runtime)**.

- **Static Polymorphism** – achieved through **method overloading**, resolved by the compiler.
- **Dynamic Polymorphism** – achieved through **method overriding**, resolved by the JVM at runtime.

---

### 104. What is Static Polymorphism? (Overload, Compile-time)

> Static polymorphism occurs when multiple methods share the same name but differ in parameters (method overloading).
> The compiler determines which method to call based on parameter types, order, and count.  
> It’s resolved during compilation, making it faster and type-safe.
---

### 105. What is Dynamic Polymorphism? (Override, Runtime)

> Dynamic polymorphism occurs when a subclass overrides a superclass method, and the method call is resolved at runtime.
> When a superclass reference points to a subclass object, the subclass’s overridden method is executed, enabling
> runtime behavior flexibility.
---

### 106. What is the difference between Polymorphism and Inheritance?

> Inheritance defines relationships between classes; polymorphism defines behavior based on those relationships.

- **Inheritance** – allows one class to derive from another, reusing attributes and methods.
- **Polymorphism** – allows objects of different subclasses to be treated as instances of a common superclass, executing
  behavior specific to their type.

> Inheritance is structural (class hierarchy), while polymorphism is behavioral (method resolution).  
> The JVM implements inheritance through metadata linkage, while polymorphism leverages dynamic dispatch mechanisms.

---

### 107. What are the advantages of Polymorphism?

- Enables **runtime flexibility** through method overriding.
- Reduces **code duplication** via shared interfaces and abstractions.
- Improves **maintainability** by decoupling code behavior from specific implementations.
- Supports **open/closed principle** — open for extension, closed for modification.
- Simplifies **testing** and **mocking** through interface-based design.

---

### 108. What is Overloading?

> Overloading allows multiple methods in the same class to share the same name but differ in parameter lists.
> Method overloading is a form of **compile-time polymorphism** that improves readability and flexibility.  
> The compiler determines which version to invoke based on the number, type, and order of parameters provided during the
> call.
---

### 109. What are the rules for Method Overloading?

1. Parameter list must differ — this is the only valid differentiator.
2. Return type does **not** affect method overloading.
3. Access modifiers may differ.
4. Static, final, or abstract modifiers don’t affect overload validity.
5. Overloading can occur in the same class or between a superclass and subclass.

---

### 110. Can we overload Static methods?

> Yes, static methods can be overloaded.
> Overloading depends on method signatures, not binding or inheritance.  
> Static methods follow the same rules as instance methods when overloaded.  
> Each version is resolved at compile time based on its parameter list.
---

### 111. Can we create methods with the same signature but different return types?

> No, Java does not allow methods with the same signature but different return types.
> The compiler identifies methods by **name and parameter list** — return type is not part of the method signature.  
> Hence, two methods differing only by return type cause a compile-time error.
---

### 112. Can Overloading be an example of Dynamic Binding?

> No, overloading is **static binding**.
> In overloading, the method call is resolved during compilation based on parameter types — not at runtime.  
> Only overriding supports dynamic binding through runtime dispatch based on the actual object type.
---

### 113. What is Overriding?

> Overriding occurs when a subclass provides a specific implementation of a method already defined in its superclass.
> It allows subclass objects to redefine inherited behavior, enabling **runtime polymorphism**.  
> The method signature (name, parameters, and order) must be identical to the superclass method.  
> The overriding method executes based on the **object’s runtime type**, not the reference type.
---

### 114. What are the rules for Method Overriding?

1. **Same method name and parameters** — identical signature required.
2. **Return type** — must be the same or a subtype (**covariant return**).
3. **Access level** — cannot be more restrictive (e.g., public → protected is invalid).
4. **Static methods** — cannot be overridden; only hidden.
5. **Final methods** — cannot be overridden.
6. **Constructors** — cannot be overridden.
7. **Exception rules** — overriding method cannot throw broader checked exceptions.

---

### 115. Can we change the signature of an overridden method?

> No, changing the method signature creates **overloading**, not overriding.
> Overriding demands an identical signature — if parameters differ in type, number, or order, the compiler treats it as
> a new overloaded method instead of an override.  
> Thus, the superclass version remains unaffected.
---

### 116. Can class fields be overridden?

> No, fields cannot be overridden — they are **hidden**, not overridden.
> If a subclass declares a field with the same name as a superclass field, both exist independently.  
> Access is determined by the **reference type**, not the object type, meaning it’s resolved at compile time.
---

### 117. What is Binding?

> Binding is the process of linking a method call to its actual method implementation.
> Binding determines when and how method calls are resolved — either at **compile time (static binding)** or **runtime (
dynamic binding)**.  
> This mechanism defines whether the JVM must determine the target method before or during execution.
---

### 118. What is Static Binding?

> Static binding occurs when method resolution happens at compile time.
> It applies to **static**, **final**, and **private** methods — the compiler knows exactly which method to call.  
> Static binding ensures faster invocation since no runtime lookup is required.
---

### 119. What is Dynamic Binding?

> Dynamic binding occurs when method resolution happens at runtime based on the actual object type.
> It applies to **overridden instance methods**.  
> When a superclass reference points to a subclass object, the subclass method executes.  
> This mechanism enables **runtime polymorphism**.

---

### 120. Can we override Static methods?

> No, static methods cannot be overridden — they can only be **hidden**.
> Static methods belong to the **class**, not to an instance.  
> When a subclass defines a static method with the same signature, it hides the superclass method instead of overriding
> it.  
> The method to execute is determined by the **reference type**, not the object type.

---

### 121. Can we override Final methods?

> No, final methods cannot be overridden.
> A `final` method is declared to prevent modification by subclasses, preserving consistent behavior across inheritance
> hierarchies.  
> Attempting to override it causes a **compile-time error**.

---

### 122. Can we override Private methods?

> No, private methods cannot be overridden.
> Private methods are **not inherited** by subclasses; thus, they are invisible outside their defining class.  
> If a subclass defines a method with the same name and parameters, it is treated as a **new, independent method**, not
> an
> override.

---

### 123. Can we override a Protected method with a different Access Modifier?

> Yes, but only if the new access level is **equal or more permissive**.
> An overriding method can widen access but not restrict it.  
> For example, a `protected` method can be overridden as `public`, but not as `private` or package-private.  
> This rule ensures consistent visibility for overridden methods across inheritance hierarchies.
---

### 124. What is Abstraction?

> Abstraction is the process of hiding implementation details and exposing only the essential functionality to the user.
> It focuses on **what** an object does rather than **how** it does it.  
> Abstraction helps design cleaner interfaces, reduces complexity, and allows changes in implementation without
> affecting
> the higher-level code.
---

### 125. How do we achieve Abstraction?

- **Abstract classes** define partial implementations and shared state.
- **Interfaces** define complete abstraction via method contracts only.

> Both approaches enable design by contract and polymorphism through common types.
---

### 126. What is a Concrete Class?

> A concrete class is a fully implemented class that can be directly instantiated.
> It provides complete method implementations and defines actual object behavior.  
> Unlike abstract classes, it cannot contain unimplemented (abstract) methods.
---

### 127. What are the differences between a Concrete Class and an Abstract Class?

> A concrete class is fully implemented; an abstract class may contain unimplemented methods.

| Feature        | Abstract Class                         | Concrete Class                    |
|----------------|----------------------------------------|-----------------------------------|
| Instantiation  | Cannot be instantiated                 | Can be instantiated               |
| Implementation | May have abstract and concrete methods | Must have full implementation     |
| Purpose        | Serves as a base or template           | Represents actual object behavior |
| Constructor    | Can have constructors for subclass use | Has constructors for direct use   |

---

### 128. What are the rules of an Abstract Class?

> Abstract classes define partial implementations and cannot be instantiated.

1. Declared using the `abstract` keyword.
2. May contain both abstract and non-abstract methods.
3. Can have constructors, fields, and static methods.
4. Cannot be `final` or `private`.
5. Must be extended by a subclass to provide complete functionality.

---

### 129. What are the rules of an Abstract Method?

> Abstract methods declare a contract without providing an implementation.

1. Declared with the `abstract` keyword and no body.
2. Must be inside an abstract class or interface.
3. Cannot be `static`, `final`, or `private`.
4. Must be implemented by the first concrete subclass.

---

### 130. What are the advantages of Abstraction?

> Abstraction simplifies complex systems and enhances flexibility.

- Reduces code complexity by hiding low-level details.
- Promotes modular design and loose coupling.
- Enables easier maintenance and scalability.
- Supports interface-based polymorphism.
- Improves testability through mockable contracts.

---

### 131. Can Abstract methods be static?

> No, abstract methods cannot be static.
> Static methods belong to the class, not an instance.  
> Since abstract methods require overriding through subclass instances, static context violates the abstraction
> principle.

---

### 132. Can we create an object from an Abstract Class?

> No, abstract classes cannot be instantiated directly.
> Since abstract classes may contain incomplete methods, they cannot produce a valid object on their own.  
> They must be subclassed by a concrete class providing full implementations.
---

### 133. Does an Abstract Class have a constructor?

> Yes, abstract classes can have constructors.
> Constructors in abstract classes are used to initialize fields and state common to subclasses.  
> They are invoked when a concrete subclass object is created, forming part of the object’s construction chain.

---

### 134. What is an Interface?

> An interface is a fully abstract type in Java that defines a contract (set of methods) a class must implement.
> Interfaces specify *what* operations a type can perform, not *how* they are performed.  
> They are used to define common behavior across unrelated classes.
---

### 135. Why do we need an Interface?

> Interfaces enable abstraction, polymorphism, and multiple inheritance of behavior.

- Decouple code from concrete implementations.
- Support dependency injection and testing.
- Allow multiple classes to share common contracts.
- Enable flexible and extensible system design.

---

### 136. What are the characteristics of an Interface?

> Interfaces are abstract, behavioral contracts that define methods and constants.

1. Methods are implicitly **public** and **abstract** (unless default or static).
2. Fields are implicitly **public**, **static**, and **final**.
3. Interfaces cannot have constructors.
4. A class can implement multiple interfaces.
5. From Java 8+, interfaces can have **default** and **static** methods.
6. From Java 9+, they can also have **private** methods.

---

### 137. What are the rules of an Interface?

> Interfaces define abstract contracts that implementing classes must follow.

1. Declared using the `interface` keyword.
2. Cannot be instantiated directly.
3. Can extend multiple interfaces (multiple inheritance).
4. Cannot extend a class.
5. All fields are `public static final`.
6. Methods are `public abstract` by default (except default, static, private).
7. Implementing classes must define all abstract methods.

---

### 138. Which Access Modifiers can be used in Interface methods?

| Method Type        | Allowed Modifiers     | Description                                 |
|--------------------|-----------------------|---------------------------------------------|
| Abstract (default) | `public` (implicitly) | Must be implemented by implementing classes |
| Default method     | `public`              | Provides a default implementation           |
| Static method      | `public` or `private` | Belongs to interface itself                 |
| Private method     | `private`             | Used internally by other default methods    |

---

### 139. Can we create objects of an Interface?

> Interfaces don’t have constructors or complete implementations.  
> You can only create an object of a class that implements the interface.
---

### 140. Can we define static methods inside an Interface?

> Yes, from Java 8 onward.
> Static methods in interfaces belong to the interface itself and cannot be overridden or inherited by implementing
> classes.
---

### 141. Does an Interface support multiple inheritance?

> Yes, interfaces support multiple inheritance of type.
> A single interface can extend multiple other interfaces, and a class can implement multiple interfaces.
---

### 142. What are the differences between an Abstract Class and an Interface?

| Aspect           | Abstract Class                               | Interface                                          |
|------------------|----------------------------------------------|----------------------------------------------------|
| Purpose          | Provides base functionality and common state | Defines a behavioral contract                      |
| Methods          | Can have abstract and concrete methods       | Only abstract, default, static, or private methods |
| Fields           | Can have instance fields                     | Only `public static final` constants               |
| Inheritance      | Single inheritance                           | Multiple inheritance allowed                       |
| Constructors     | Can have constructors                        | Cannot have constructors                           |
| Access Modifiers | Supports all modifiers                       | Methods are `public` by default                    |
| Use Case         | When classes share behavior or state         | When classes share common abilities                |

---

### 143. What is a Marker Interface?

> A marker interface is an empty interface used to signal metadata or behavior to the JVM or frameworks.
> It doesn’t contain any methods or fields — it marks a class to indicate special processing or capability.

---

### 144. Give examples of Marker Interfaces.

- `java.io.Serializable`
- `java.lang.Cloneable`
- `java.util.RandomAccess`
- `java.rmi.Remote`

---

### 145. If a Marker Interface is empty, why is it needed?

> Because it provides **compile-time type checking** and **runtime metadata**.

- The JVM or framework can recognize and handle marked objects differently.
- Prevents accidental misuse (e.g., serializing non-`Serializable` objects).
- Enables metadata tagging without external configuration or annotations.

---

### 146. What are Wrapper Classes?

> Wrapper classes are object representations of primitive data types.
> They allow primitives (like `int`, `char`, `boolean`) to be used as objects in collections, generics, or APIs that
> require objects.

---

### 147. Why do we need Wrapper Classes?

> Because Java collections and generic types work only with objects, not primitives.

1. To use primitives in data structures like `List<Integer>`.
2. To perform conversions and parsing (e.g., `Integer.parseInt()`).
3. To handle `null` values (primitives cannot).
4. To use utility methods like `Double.compare()` or `Character.isDigit()`.

---

### 148. What types of Wrapper Classes exist?

> Each primitive type has a corresponding wrapper class.

| Primitive Type | Wrapper Class |
|----------------|---------------|
| `byte`         | `Byte`        |
| `short`        | `Short`       |
| `int`          | `Integer`     |
| `long`         | `Long`        |
| `float`        | `Float`       |
| `double`       | `Double`      |
| `char`         | `Character`   |
| `boolean`      | `Boolean`     |

---

### 149. What kind of classes are Wrapper Classes?

> Wrapper classes are **immutable**, **final**, and **object representations** of primitives.

- Declared `final` to ensure immutability.
- Provide caching mechanisms for small values (`Integer`, `Long`, `Short`, `Byte`, `Character`).
- Extend `Number` (except `Character`, `Boolean`).
- Stored in the heap as objects.

---

### 150. Which classes are subclasses of the Number class?

`Number` subclasses are numeric wrappers that support conversion and arithmetic operations.

**List:**

- `Byte`
- `Short`
- `Integer`
- `Long`
- `Float`
- `Double`
- `BigInteger` (indirectly related via Number hierarchy)
- `BigDecimal` (same as above)

---

### 151. What types of Big Numbers are there?

> Java provides two classes for handling very large or precise numbers: **BigInteger** and **BigDecimal**.

- **BigInteger** is used for arbitrary-precision integer arithmetic.
- **BigDecimal** is used for arbitrary-precision decimal arithmetic, suitable for financial and scientific calculations.

---

### 152. What is the BigDecimal class?

> `BigDecimal` represents immutable, arbitrary-precision decimal numbers.
> It stores numbers as an unscaled value and a scale (decimal position).  
> Used in financial, monetary, or scientific contexts where floating-point rounding errors are unacceptable.
---

### 153. What is the BigInteger class?

> `BigInteger` represents immutable integers of arbitrary size.
> It supports all standard arithmetic, bitwise, and modular operations without overflow.  
> Useful for cryptography, combinatorics, and large numerical computations.
---

### 154. Can we use arithmetic operators (+, −, *, /) with these classes?

> No, arithmetic operators cannot be used with `BigInteger` or `BigDecimal`.
> They are objects, not primitives.  
> Instead of operators, they provide methods such as `add()`, `subtract()`, `multiply()`, and `divide()`.
---

### 155. Why do we need AutoBoxing and UnBoxing?

> To seamlessly convert between primitives and their wrapper classes.
> Java collections and generics work only with objects.  
> AutoBoxing and UnBoxing eliminate the need for manual conversion when storing or retrieving primitives from
> object-based
> structures.
---

### 156. What is AutoBoxing?

> Automatic conversion of a primitive type to its corresponding wrapper class.
> Occurs implicitly when a primitive is assigned to an object reference (e.g., `int` → `Integer`).  
> The compiler inserts `valueOf()` calls behind the scenes.
---

### 157. What is UnBoxing?

> Automatic conversion of a wrapper object to its primitive value.
> Occurs when a wrapper is used in a primitive context (e.g., arithmetic operations or comparisons).  
> The compiler adds `xxxValue()` calls automatically (e.g., `intValue()`).
---

### 158. What are Narrowing and Widening?

> They are two types of type conversions between primitive data types.

- **Widening** (implicit): Converting a smaller type to a larger one (e.g., `int` → `long` → `double`). Safe and
  automatic.
- **Narrowing** (explicit): Converting a larger type to a smaller one (e.g., `double` → `int`). Requires casting and may
  cause data loss.

---

### 159. What is an Inner Class?

> An Inner Class is a class defined within another class.
> It allows logically grouping classes that are used only in one place, improving encapsulation and readability.  
> Inner classes have access to the members (including private ones) of the outer class.

---

### 160. What are the advantages of using Inner Classes?

1. **Encapsulation** – Inner classes can access private members of the outer class, enabling cohesive design.
2. **Namespace Control** – Reduces namespace pollution by keeping helper classes hidden.
3. **Logical Grouping** – Ties related functionality together within the same context.
4. **Event Handling** – Commonly used in frameworks and GUI code (e.g., listeners in Swing or Android).
5. **Improved Maintainability** – Easier to manage and modify internal logic.

---

### 161. What types of Inner Classes exist?

> There are four main types of inner classes in Java.

1. **Non-static Inner Class (Member Inner Class)** – Associated with an instance of the outer class.
2. **Static Nested Class** – Declared static; cannot access non-static members of the outer class directly.
3. **Local Inner Class** – Defined inside a method or block, visible only within that scope.
4. **Anonymous Inner Class** – A class without a name, defined and instantiated simultaneously, usually to override
   methods.

---

### 162. Can a Static Inner Class access non-static fields of the Outer Class?

> No, a static inner class cannot access non-static members of the outer class.
> Because static nested classes do not hold a reference to an instance of the outer class, they can only access static
> fields and methods.  
> To access non-static members, they require an explicit reference to an outer class instance.

---

### 163. Can Local Inner Classes be declared with access modifiers?

> No, local inner classes cannot have access modifiers.
> They are declared within methods or blocks, where access modifiers (`public`, `private`, `protected`) are not
> allowed.  
> Their visibility is inherently limited to the enclosing block.
---

### 164. What is Memory Management?

> Memory management is the process of efficiently allocating, using, and freeing memory resources in a program.
> In Java, memory management is primarily handled by the **JVM**, which automatically allocates memory for objects and
> reclaims unused memory through **Garbage Collection (GC)**.  
> It ensures stable performance, prevents memory leaks, and optimizes runtime efficiency.
---

### 165. What are the types of memory?

1. **Heap Memory** – Stores objects and their associated data.
2. **Stack Memory** – Stores method calls, local variables, and references.
3. **Metaspace (formerly PermGen)** – Stores class metadata and static information.
4. **Code Cache** – Stores compiled native code (JIT-compiled bytecode).
5. **Native Memory** – Used by the JVM and native libraries outside the managed heap.

> Each memory area serves distinct roles — Stack for execution, Heap for object lifecycle, and Metaspace for type
> metadata.  
> Garbage Collection primarily targets the Heap.


---

### 166. Which ones are considered primary memory?

> Heap and Stack memory are considered primary runtime memory areas.
> They store dynamic objects and execution data essential for program operation.

- **Heap** holds objects and class instances.
- **Stack** holds method calls and references to those objects.

---

### 167. What type of memory is Stack Memory?

> Stack memory is a **thread-specific, linear memory area** used for method execution and local variable storage.
> Each thread has its own stack that stores **Stack Frames** for active methods.  
> When a method is called, a frame is pushed; when it completes, the frame is popped.
> Stack memory operates at the thread level and is managed automatically by the JVM.  
> Its size is fixed per thread and crucial for recursion and method call depth.
> Stack memory is a per-thread linear memory area managed by the JVM to store method execution data and maintain the
> call
> stack lifecycle.
---

### 168. What is a Stack Frame?

> It contains local variables, method parameters, return addresses, and references to objects on the heap.  
> When a method is invoked, the JVM creates a new frame; when it completes, the frame is destroyed.
> A Stack Frame is a method execution context holding variables, operands, and control data, created and removed
> dynamically as methods are invoked and completed.
> Each frame holds:

- **Local Variable Array**
- **Operand Stack**
- **Frame Data** (return info, references)

> Stack frames are crucial for JVM bytecode execution and control flow.

---

### 169. What are the advantages of Stack Memory?

> Stack memory is fast, efficient, and thread-safe.

> Stack memory is efficient and self-managed, offering fast access and automatic cleanup per thread without involving
> the garbage collector.

1. **Speed** – Simple LIFO structure enables quick push/pop operations.
2. **Thread Safety** – Each thread has its own isolated stack.
3. **Automatic Management** – Memory is reclaimed immediately after method completion.
4. **Low Overhead** – No need for garbage collection.

---

### 170. What is LIFO?

> LIFO stands for **Last In, First Out**.
> It’s a data handling principle where the most recently added element is the first to be removed — exactly how the call
> stack operates.  
> The last method called is the first to complete and pop from the stack.
> The JVM enforces LIFO order in method invocation and return mechanisms, ensuring predictable and efficient call flow
> management.
> LIFO (Last In, First Out) defines the execution order of stack operations, ensuring structured method call and return
> sequencing in the JVM.
---

### 171. When does a StackOverflow occur?

> A StackOverflowError occurs when the thread’s stack memory limit is exceeded.
> It typically happens due to **deep or infinite recursion** or **excessive local variable allocation** that consumes
> all
> available stack space.
> The JVM allocates a fixed stack size per thread. When frame allocation exceeds this limit, it throws
`java.lang.StackOverflowError`.  
> Each recursive call consumes a new frame until stack exhaustion.
---

### 172. What are the parts of the Heap?

> Heap memory is divided into **Young Generation** and **Old Generation (Tenured Space)**.

1. **Young Generation** – Where new objects are created.

- Includes **Eden Space** and **Survivor Spaces (S0, S1)**.

2. **Old Generation (Tenured Space)** – Where long-lived objects are stored after surviving multiple garbage
   collections.

> The division improves GC efficiency by focusing frequent collections on short-lived objects in the Young Generation.  
> Modern GCs (like G1, ZGC, Shenandoah) optimize this layout dynamically
---

### 173. What is the Nursery Space?

> Nursery Space is the part of the Heap where **newly created objects** are initially allocated.
> It is located inside the **Young Generation** and consists of:

- **Eden Space** – where new objects are created.
- **Survivor Spaces (S0, S1)** – temporary regions for objects that survive minor garbage collections.

---

### 174. What are the key points about Nursery Space?

> Nursery Space manages short-lived objects and supports fast GC cycles.

- Most objects are created and destroyed here.
- Minor GC occurs frequently in this region.
- Objects surviving several GCs are moved to the Tenured Space.
- It minimizes full GC frequency by reclaiming memory early.
- Performance tuning often focuses on Eden and Survivor sizes.

---

### 175. What is the Tenured Space?

> Tenured Space (Old Generation) stores **long-lived objects** that have survived several Minor GCs.
> After an object remains alive through multiple GC cycles in the Young Generation, it is **promoted** to the Old
> Generation.  
> Garbage collection here is called a **Major GC** or **Full GC** and is less frequent but more expensive.
> The Tenured Space represents stable application data, such as cached objects or session data, which persist longer in
> memory.  
> Efficient tuning reduces the frequency and duration of Full GCs.
---

### 176. What is the Permanent Generation?

> Permanent Generation (PermGen) was the JVM memory area that stored **class metadata**, **method information**, and *
*interned strings** before Java 8.

> It contained data describing loaded classes, method definitions, and static fields.  
> However, it was **removed in Java 8** due to frequent memory issues and replaced by **Metaspace**.

> PermGen was part of the Heap and required manual size tuning (`-XX:PermSize`, `-XX:MaxPermSize`), leading to
`OutOfMemoryError: PermGen space` in large applications.

---

### 177. What is the Metaspace?

> Metaspace is the **native memory region** introduced in Java 8 to replace PermGen.
> It stores **class metadata**, **method information**, and **annotations**, but unlike PermGen, it uses **native memory
** (outside the Java heap).  
> Its size grows dynamically unless limited by `-XX:MaxMetaspaceSize`.
> Metaspace eliminates the fixed-size limitation of PermGen, reducing memory errors for applications with many
> dynamically
> loaded classes (e.g., web apps or frameworks like Spring).
---

### 178. What is the Method Area?

> The Method Area is a **logical JVM memory region** that stores class-level information and metadata.

- Class definitions and constant pools
- Method code and field metadata
- Static variables and runtime constant data

> Although conceptually part of the JVM specification, its physical implementation depends on the JVM version:

- **PermGen** in Java 7 and below
- **Metaspace** in Java 8 and above

---

### 179. What are the types of Method Parameters?

> Java supports two main types of parameters — **Actual Parameters** and **Formal Parameters**.

- **Actual Parameters:** The real values or arguments passed to a method when it is called.
- **Formal Parameters:** The variables defined in the method declaration that receive the values of actual parameters.

---

### 180. What is Passing by Value?

> Passing by Value means that a **copy of the variable’s value** is sent to the method.
> The method operates on a copy, not the original variable.  
> Any changes made inside the method **do not affect** the original data in the caller.
> In Java, both primitives and object references are passed by value:

- For **primitives**, the value itself is copied.
- For **objects**, the reference (memory address) is copied, not the object itself.

---

### 181. What is Passing by Reference?

> Passing by Reference means passing the **actual memory address** of a variable to a method.
> In true pass-by-reference systems, the called method can directly modify the caller’s variable since both share the
> same
> memory reference.
> This concept does **not apply** in Java.  
> Even though object references are passed, Java still passes a **copy of the reference**, not the reference itself.
---

### 182. Does Java support Passing by Reference?

> No, Java does **not** support pass-by-reference — it is always **pass-by-value**.
> When an object is passed to a method, a **copy of the reference** (not the object) is passed.  
> Hence, the method can modify the object’s internal state but cannot make the reference point to a new object.

---

### 183. What are Variable Arguments?

> Variable Arguments (varargs) allow a method to accept **a variable number of arguments** of the same type.
> Varargs are represented by an ellipsis (`...`) after the parameter type.  
> Inside the method, varargs are treated as an **array**, allowing iteration over all arguments.
> They simplify method calls where the number of parameters can vary (e.g., logging or formatting).  
> Rules:

- Only **one varargs parameter** is allowed per method.
- It must be the **last** parameter in the method declaration.

---

### 184. What is the Garbage Collector and what is its purpose?

> The Garbage Collector (GC) is a JVM mechanism that **automatically manages memory** by reclaiming space from objects
> no longer reachable by any references.
> GC identifies and removes unused objects from the Heap to prevent memory leaks and optimize application performance.  
> It operates transparently in the background, freeing developers from manual memory management and ensuring safe,
> efficient memory reuse.

> The Garbage Collector automatically reclaims memory occupied by unreachable objects, maintaining Heap health and
> preventing OutOfMemoryError.  
> It relies on reachability analysis from GC Roots and operates through a combination of marking, sweeping, and
> compacting
> phases to ensure efficient memory utilization.
---

### 185. Types of Garbage Collectors (all)

> Modern JVMs support several Garbage Collectors, each optimized for different workloads and latency requirements.

[GC Types](assets/gc_types.png)

1. **Serial GC (`-XX:+UseSerialGC`)**
    - Single-threaded, simple, and best for small applications or single-core systems.
    - Uses stop-the-world pauses for all GC operations.

2. **Parallel GC (`-XX:+UseParallelGC`)**
    - Multi-threaded GC for both young and old generations.
    - Focuses on throughput; suitable for batch or CPU-bound applications.

3. **CMS (Concurrent Mark-Sweep) GC (`-XX:+UseConcMarkSweepGC`)** *(Deprecated since Java 9)*
    - Performs most GC work concurrently with the application.
    - Reduces pause times but causes fragmentation.

4. **G1 (Garbage-First) GC (`-XX:+UseG1GC`)** *(Default since Java 9)*
    - Region-based collector balancing throughput and low latency.
    - Performs concurrent marking and incremental compaction.

5. **ZGC (`-XX:+UseZGC`)**
    - Ultra-low pause GC (<10ms) using colored pointers and load barriers.
    - Suitable for very large heaps (multi-terabyte).

6. **Shenandoah GC (`-XX:+UseShenandoahGC`)**
    - Low-pause concurrent collector developed by Red Hat.
    - Compacts the heap concurrently to avoid long pauses.

---

### 186. What are the stages of the JVM Garbage Collector?

> GC operates in three primary stages — **Mark**, **Sweep**, and **Compact**.

1. **Mark:**
    - Identify all live objects reachable from GC Roots.
    - Unreachable objects are marked as garbage.

2. **Sweep:**
    - Reclaim memory occupied by unreachable (dead) objects.
    - Marks free regions available for future allocations.

3. **Compact (optional):**
    - Rearranges live objects to eliminate memory fragmentation.
    - Updates object references after relocation.

---

### 187. What are the types of Sweeping?

1. **Normal (Non-Compacting) Sweep:**
    - Frees memory of unreachable objects without rearranging live objects.
    - May cause **heap fragmentation** over time.

2. **Compacting Sweep:**
    - Frees memory and **moves live objects together** to form a contiguous space.
    - Eliminates fragmentation but requires **updating references**.

---

### 188. What are the types of Non-Access Modifiers?

> Non-access modifiers define **behavioral or structural properties** of classes, methods, and variables, rather than
> visibility.

- **final** — prevents modification (class inheritance, method overriding, or variable reassignment).
- **static** — associates members with the class rather than instances.
- **abstract** — defines incomplete classes or methods meant to be implemented by subclasses.
- **synchronized** — ensures thread-safe access to methods or code blocks.
- **volatile** — ensures visibility of variable changes across threads.
- **transient** — excludes variables from serialization.
- **native** — marks methods implemented in non-Java code (e.g., C via JNI).
- **strictfp** — enforces consistent floating-point behavior across platforms.

---

### 189. Where is each Non-Access Modifier used?

| Modifier       | Used With              | Purpose                                          |
|----------------|------------------------|--------------------------------------------------|
| `final`        | Classes, methods, vars | Prevents extension, overriding, or reassignment  |
| `static`       | Vars, methods, blocks  | Class-level association; shared across instances |
| `abstract`     | Classes, methods       | Defines incomplete contracts for subclassing     |
| `synchronized` | Methods, blocks        | Thread-safety via intrinsic locking              |
| `volatile`     | Variables              | Guarantees visibility of variable changes        |
| `transient`    | Variables              | Excludes from serialization                      |
| `native`       | Methods                | Implemented in non-Java language (JNI)           |
| `strictfp`     | Classes, methods       | Consistent FP computations across JVMs           |

---

### 190. What are Record Classes?

> A Record Class is a **special type of class** in Java used for immutable data carriers with automatic field,
> constructor, and method generation.
> Introduced in Java 16, records are final, immutable, and implicitly extend `java.lang.Record`.  
> They automatically generate:

- private final fields,
- canonical constructor,
- `equals()`, `hashCode()`, and `toString()` methods.

---

### 191. What types of constructors does a Record Class have?

1. **Canonical Constructor** — Matches all record components in order; auto-generated if not declared.
2. **Compact Constructor** — Declared without parameters to validate or normalize fields before assignment.
3. **Custom Constructor** — Overloaded constructor with different parameters, calling the canonical one explicitly.

---

### 192. What are Sealed Classes?

> Sealed classes restrict which other classes can extend or implement them.
> Introduced in Java 17, a sealed class uses the `permits` keyword to declare permitted subclasses explicitly.  
> Each subclass must declare itself as `final`, `sealed`, or `non-sealed`.
---

### 193. Why are Sealed Classes used?

> To **control inheritance** and enforce **restricted extensibility**.
> They prevent unwanted subclassing, maintaining predictable behavior and enabling exhaustive pattern matching in switch
> expressions.  
> Common in domain modeling where only known variants should exist.

> Sealed Classes ensure controlled, predictable, and secure inheritance hierarchies — useful in closed-domain systems,
> compiler checks, and exhaustive type handling.
---

### 194. Why is an Instance Initializer Block used?

> An Instance Initializer Block (IIB) initializes instance variables when constructors cannot handle all initialization
> logic.
> It runs **every time** an object is created, before the constructor executes.  
> Used to share common initialization code across multiple constructors.
---

### 195. When does an Instance Initializer Block execute?

> It executes **before the constructor**, every time a new object is created.

Execution order:

1. Memory allocation.
2. Default field initialization.
3. Explicit field initializers.
4. Instance Initializer Block.
5. Constructor body.

---

### 196. When does a Static Block execute?

> Static Blocks execute **once when the class is first loaded** by the JVM.
> They initialize static variables or perform one-time setup operations like loading configurations or establishing
> static resources.
---

### 197. What are the differences between Static and Instance Initializer Blocks?

> Static Blocks run once per class; Instance Blocks run for every new object.

| Feature        | Static Block           | Instance Initializer Block                  |
|----------------|------------------------|---------------------------------------------|
| Execution Time | Once, when class loads | Before every constructor call               |
| Access         | Only static members    | Can access both instance and static members |
| Purpose        | Class-level setup      | Object-level setup                          |
| Frequency      | Executes once          | Executes per instance                       |

---

### 198. What is Variable Shadowing?

> Variable shadowing occurs when a **local variable or parameter** has the same name as a **field** in the enclosing
> scope, temporarily hiding the outer variable.
> Within the inner scope (like a method or block), the local variable takes precedence, making the outer variable
> inaccessible directly.  
> The outer variable can still be accessed using the `this` keyword (for instance fields) or `ClassName.` (for static
> fields).

---

### 199. What is Variable Hiding?

> Variable hiding occurs when a **subclass defines a field with the same name** as one in its superclass.
> The subclass field hides the superclass field but does not override it.  
> Accessing the variable depends on the **reference type**, not the actual object type.
---

### 200. What is Type Inference?

> Type inference is the JVM compiler’s ability to **automatically determine variable or expression types** from context.
> Introduced with Java 10’s `var` keyword, it allows the compiler to infer a local variable’s type at compile time based
> on the assigned value.  
> The type remains **static and final** — inference happens only once and is not dynamic.
---

### 201. When can we use the `var` keyword, and when can’t we use it?

> `var` can be used for **local variables with an initializer**, but not for fields, method parameters, or uninitialized
> declarations.

**Allowed:**

- Local variables inside methods, loops, and try-with-resources.
- When the type can be inferred from the initializer expression.

**Not allowed:**

- For class fields or parameters.
- When no initializer is provided.
- With `null` assignments (type inference impossible).
- In lambda parameter declarations.

---

### 202. What are Enum Classes?

> Enum Classes represent **fixed sets of constants** — special types in Java that extend `java.lang.Enum`.
> Each constant in an enum is a **singleton instance** of the enum type.  
> Enums can have fields, constructors, and methods, and can even implement interfaces.  
> They provide type safety and prevent invalid values at compile time.
---

### 203. Can we create objects from an Enum Class?

> No, enum objects **cannot be created manually**.
> All enum constants are instantiated automatically by the JVM when the enum class is loaded.  
> The constructor of an enum is implicitly `private` to prevent external instantiation.
---

### 204. What are the advantages of Enum Classes?

> Enums provide **type safety**, **readability**, and **immutability** for predefined constant sets.

- Ensure compile-time safety (no invalid constants).
- Replace unstructured `int` or `String` constants.
- Can contain logic, methods, and interfaces.
- Are thread-safe singletons by design.
- Support iteration, comparison, and switch expressions.

---

### 205. Can Enum Classes implement interfaces?

> Yes, Enums can implement interfaces.
> This allows each enum constant to provide its own behavior for the implemented methods, enabling polymorphic behavior
> within a fixed constant set.
---

### 206. Can we define a constructor in an Enum Class?

> Yes, but it must be **private or package-private**.
> Enum constructors initialize constant-specific fields or behaviors and are called **once per constant** during class
> loading.  
> They cannot be invoked explicitly.
---

### 207. What kind of class is the `Objects` class?

> `java.util.Objects` is a **final utility class** that provides **static helper methods** for operating on objects.
> It cannot be instantiated or extended.  
> Its methods simplify common operations like equality checks, null handling, and hash code generation.

---

### 208. What methods does the `Objects` class have?

> The `Objects` class provides **null-safe static methods** for equality, hashing, comparison, and validation.

**Key methods:**

- `equals(Object a, Object b)` – Null-safe equality check.
- `deepEquals(Object a, Object b)` – Deep comparison for arrays.
- `hash(Object... values)` – Generates combined hash codes.
- `hashCode(Object o)` – Returns object hash code safely.
- `compare(T a, T b, Comparator<? super T> c)` – Compares using a comparator.
- `requireNonNull(T obj)` – Ensures a reference is not null, otherwise throws `NullPointerException`.
- `isNull(Object obj)` / `nonNull(Object obj)` – Null check predicates.
- `toString(Object o)` / `toString(Object o, String nullDefault)` – Null-safe string conversion.

---

### 209. What is JavaDoc?

> JavaDoc is a **documentation generation tool** included with the JDK.
> It extracts specially formatted comments (`/** ... */`) from source code and converts them into structured HTML
> documentation.
---

### 210. Why is JavaDoc used?

> To create **standardized, readable API documentation** directly from source code.
> It ensures consistency between code and documentation, helps developers understand class contracts, and enables IDE
> tooltips and online API references.
---

### 211. What is a UUID?

> A UUID (Universally Unique Identifier) is a 128-bit value used to uniquely identify information across systems.
> Represented as 32 hexadecimal digits (commonly in 8-4-4-4-12 format), it ensures global uniqueness without requiring a
> central authority.
---

### 212. Why is a UUID used?

> To generate unique identifiers across systems, databases, or services without coordination.
> UUIDs are used for:
> Unique database keys
> Distributed systems (no central ID generator)
> Object or entity identification
> Session or transaction tracking
---

### 213. What do M and N represent in a UUID?

> M and N indicate the version and variant of the UUID.

> M → Version (defines how the UUID was generated):

- 1 → Time-based
- 3 → Name-based (MD5)
- 4 → Random
- 5 → Name-based (SHA-1)
- 7 → Unix time & randomness (newer standard)

> N → Variant (defines the UUID layout and encoding scheme):
> 8, 9, A, or B → RFC 4122 (standard format)
---

# MODULE 3

### 214. What is an Exception?

> An Exception is an **unexpected event** that occurs during program execution and disrupts the normal flow of
> instructions.
> It represents abnormal conditions like invalid input, resource unavailability, or arithmetic errors that the program
> can
> handle at runtime.
---

### 215. What causes Exceptions to occur?

- Invalid user input
- Accessing null references
- Dividing by zero
- Array index out of bounds
- File or network issues
- Resource unavailability

---

### 216. Why is it important to handle Exceptions?

> Exception handling prevents program crashes and ensures graceful recovery from errors.
> It allows developers to define alternative execution paths, log errors, release resources, and maintain system
> stability.


---

### 217. What is the superclass (parent) of all Exceptions and Errors?

- `java.lang.Throwable`

> `Throwable` is the root class for both:

- `Exception` – recoverable conditions
- `Error` – serious, unrecoverable conditions

---

### 218. What is an Error, and when does it occur?

> An Error represents **serious system-level issues** that occur outside the program’s control.
> Errors indicate problems like memory exhaustion or JVM malfunction that applications usually cannot recover from.
---

### 219. What is the difference between an Exception and an Error?

- **Exception:** Recoverable, handled by the program.
- **Error:** Unrecoverable, indicates system failure.

| Aspect               | Exception                         | Error                                |
|----------------------|-----------------------------------|--------------------------------------|
| Recoverable          | Yes                               | No                                   |
| Handled by developer | Yes                               | Rarely                               |
| Examples             | IOException, NullPointerException | OutOfMemoryError, StackOverflowError |
| Package              | java.lang.Exception               | java.lang.Error                      |

---

### 220. How many types of Exceptions are there?

1. **Checked Exceptions**
2. **Unchecked Exceptions**

- **Checked Exceptions:** Checked at compile time; must be declared or handled (e.g., `IOException`, `SQLException`).
- **Unchecked Exceptions:** Occur at runtime; not required to handle explicitly (e.g., `NullPointerException`,
  `ArithmeticException`).

---

### 221. Why do we need to create custom Exception classes?

> To represent **application-specific error conditions** clearly.
> Custom exceptions improve code readability and error handling by expressing domain-specific problems (e.g.,
`InsufficientBalanceException`).
> Extend `Exception` for checked or `RuntimeException` for unchecked behavior.

---

### 222. What is Exception Propagation?

> Exception propagation is the **process by which an exception is passed up the call stack** until it’s handled.
> If a method does not catch an exception, it is automatically thrown to its caller, continuing up until caught or the
> program terminates.
---

### 223. What does “catching an Exception” mean?

> Catching an exception means **intercepting** a thrown exception and handling it to prevent program termination.
> When an exception occurs, the JVM searches for a matching `catch` block in the call stack. If found, it executes the
> handler; otherwise, the program terminates.
---

### 224. How are Exceptions caught?

> Exceptions are caught using a `try-catch` block.
> Code that might throw an exception is placed inside the `try` block.  
> When an exception occurs, control is transferred to the matching `catch` block, which handles the specific exception
> type.

---

### 225. Why do we need to catch Exceptions?

> To prevent program termination and recover from runtime errors.
> Catching exceptions allows resource cleanup, error logging, user notifications, and recovery from abnormal situations.

---

### 226. How are multiple Exceptions caught?

> By using multiple `catch` blocks or a **multi-catch** block.
> Each `catch` block can handle a different exception type.  
> Since Java 7, multiple exception types can be caught in a single block using the `|` operator to reduce redundancy.

---

### 227. What changes were introduced to try-catch in Java 7?

> Java 7 introduced **multi-catch** and **try-with-resources** features.

- Multi-catch: allows handling multiple exception types in a single catch block.
- Try-with-resources: automatically closes resources implementing `AutoCloseable`, eliminating the need for explicit
  finally blocks.

---

### 228. What is Try-with-Resources, and what are its advantages?

> It’s a feature that automatically closes resources after use.
> Introduced in Java 7, the try-with-resources statement automatically calls `close()` on all resources that implement
`AutoCloseable`, even if exceptions occur.

**Advantages:**

- No need for explicit `finally` blocks
- Prevents resource leaks
- Cleaner, safer code

---

### 229. Which interface must our classes implement to be used in Try-with-Resources?

- **AutoClosable**

---

### 230. What are the advantages of using Exceptions?

> They separate error handling from business logic and improve code reliability.

- Clean separation of normal and error logic
- Centralized error management
- Better debugging and logging
- Improved fault tolerance

---

### 231. What are the types of Exceptions?

1. **Checked Exceptions**
2. **Unchecked Exceptions**

> Checked exceptions are validated at compile-time and must be declared or handled.  
> Unchecked exceptions occur at runtime and are not mandatory to handle.
---

### 232. What is the difference between Checked and Unchecked Exceptions?

- **Checked:** Must be declared or handled.
- **Unchecked:** Not required to be declared or handled.

| Aspect         | Checked                   | Unchecked                                 |
|----------------|---------------------------|-------------------------------------------|
| Checked at     | Compile-time              | Runtime                                   |
| Must declare   | Yes                       | No                                        |
| Common classes | IOException, SQLException | NullPointerException, ArithmeticException |
| Package        | java.lang.Exception       | java.lang.RuntimeException                |

---

### 233. What are the best practices or tips for using Exceptions?

1. **Use exceptions for exceptional conditions only** – not for control flow.
2. **Prefer specific exceptions** over generic ones.
3. **Do not ignore exceptions** (avoid empty catch blocks).
4. **Wrap low-level exceptions** in meaningful, domain-specific exceptions.
5. **Clean up resources** using try-with-resources.
6. **Never swallow or suppress exceptions** unless absolutely required.
7. **Include contextual information** in exception messages.
8. **Avoid checked exceptions for recoverable runtime operations** unless business rules demand it.
9. **Log exceptions once**, not multiple times.
10. **Propagate wisely** — don’t overuse `throws` clauses.

---

### 234. What are Generics?

> Generics enable **type-safe, reusable code** by allowing classes, methods, and interfaces to operate on *
*parameterized types**.
> They provide compile-time type checking and eliminate the need for manual casting.  
> Generics introduce type parameters (e.g., `<T>`) that are replaced with actual types at compile time, ensuring
> stronger
> type safety without runtime overhead.

---

### 235. What are the advantages of using Generics?

> Type safety, reusability, and cleaner code.

- **Compile-time type checking** prevents `ClassCastException`.
- **Code reusability** through generic algorithms and collections.
- **Elimination of explicit casting** improves readability.
- **Improved maintainability** and **self-documenting APIs**.

---

### 236. Where can we declare Generics?

> Generics can be declared in **classes**, **interfaces**, **methods**, and **constructors**.

- **Class-level:** For generic data structures like `List<T>`.
- **Interface-level:** For abstract type-safe contracts.
- **Method-level:** For independent type parameters (`<T> void process(T item)`).
- **Constructor-level:** For type-safe instantiation logic.

---

### 237. What is a Single Bound?

> A Single Bound restricts a generic type parameter to **one upper type**.
> Defined using the `extends` keyword (for classes or interfaces), it allows only the specified type or its
> subclasses/implementations.  
> Example: `<T extends Number>` means `T` can be `Integer`, `Double`, etc.

---

### 238. Why do we use Bounded Types?

> To **limit generic type parameters** to specific hierarchies or capabilities.
> Bounded types let you restrict operations to types that meet certain contracts — for example, allowing only numeric
> types or comparable types for sorting.  
> This enables **safer and more meaningful** operations inside generic code.

---

### 239. What types of Bounds are there?

> There are **three** types of bounds in Generics.

1. **Upper Bound (`extends`)** – allows type and its subtypes (`<T extends Number>`).
2. **Lower Bound (`super`)** – allows type and its supertypes (`<? super Integer>`).
3. **Unbounded (`?`)** – allows any type but limits available operations.

---

### 240. What is a Multiple Bound?

> A Multiple Bound restricts a type parameter with **multiple constraints**.
> Defined as `<T extends ClassA & InterfaceB & InterfaceC>`, where a type can extend one class and implement multiple
> interfaces.  
> The **class must come first**, followed by interfaces.

---

### 241. What is Type Erasure?

> Type Erasure is the process by which **generic type information is removed at compile time**.
> During compilation, the compiler replaces all generic type parameters with their upper bounds (or `Object` if none).  
> This ensures backward compatibility with pre-Java 5 code that lacks generics.  
> At runtime, the JVM sees only raw types — meaning generic type parameters do not exist.

---

### 242. Does Type Erasure occur in methods as well?

> Yes, Type Erasure applies to methods too.
> Generic methods lose their type parameter information after compilation.  
> The compiler replaces type parameters in method signatures and bodies with their erasure (upper bound or `Object`).  
> If two methods differ only by their generic parameters, they cause **erasure conflicts** because both will have
> identical bytecode signatures after erasure.

---

### 243. What is a Raw Type?

> A Raw Type is a **generic class or interface used without specifying type parameters**.
> For example, using `List` instead of `List<String>`.  
> This disables generic type checking, causing the compiler to treat it as a legacy (non-generic) type, allowing unsafe
> operations.

---

### 244. What are Warnings?

> Compiler warnings indicate **potentially unsafe or non-generic operations**.
> When using raw types or unchecked casts, the compiler issues warnings like *“unchecked conversion”*.  
> They highlight areas where type safety cannot be verified at compile time.
---

### 245. Why should we avoid using Raw Types?

> Because they **disable type safety** and can lead to `ClassCastException` at runtime.
> Raw types bypass compile-time checks, allowing insertion of incompatible objects into collections or generic
> structures.  
> They compromise the primary purpose of generics — type-safe, reusable code.

---

### 246. What restrictions exist when using Generics?

1. Cannot create instances of type parameters (`new T()` not allowed).
2. Cannot declare static fields of type parameters.
3. Cannot use primitive types as type arguments (`List<int>` invalid).
4. Cannot use `instanceof` or reflection with parameterized types (`instanceof List<String>` invalid).
5. Cannot create arrays of parameterized types (`new List<String>[10]` invalid).

---

### 247. What are the rules for inheritance when working with Generics?

> Generics are **invariant**, meaning subtype relationships do not automatically apply to parameterized types.
> For example, `List<Integer>` is **not** a subtype of `List<Number>`, even though `Integer` extends `Number`.  
> To handle polymorphism safely, use **wildcards** like `List<? extends Number>` or `List<? super Integer>`.

---

### 248. Can we assign a subclass array to a superclass array declared with Generics?

> No, because **arrays are covariant**, but **generics are invariant**.
> You can assign a `String[]` to an `Object[]`, but you cannot assign a `List<String>` to a `List<Object>`.  
> This is because arrays are reified (runtime type checked), while generics rely on type erasure and do not preserve
> type
> information at runtime.
---

### 249. What problems exist with regular Arrays?

> Regular arrays in Java are **fixed-size and type-restricted**, which limits flexibility.

1. **Fixed Length:**  
   Once created, the array size cannot be changed. To add more elements, a new array must be created and copied
   manually.

2. **Manual Management:**  
   Developers must handle resizing, insertion, deletion, and shifting elements manually.

3. **Limited Functionality:**  
   Arrays do not provide built-in operations like search, sort, or dynamic resizing (unlike `ArrayList`).

4. **Potential Wasted Memory:**  
   If over-allocated to anticipate growth, unused slots waste memory.

5. **Type Inflexibility:**  
   Arrays can only hold elements of a single type (though generics or `Object[]` can store different types, that breaks
   type safety).

---

### 250. What are the advantages of Dynamic Arrays?

> Dynamic arrays automatically resize and provide convenient, high-level operations.

1. **Automatic Resizing:**  
   The array expands automatically when more elements are added (e.g., `ArrayList` doubles capacity internally).

2. **Simplified Management:**  
   Insertion, deletion, and access operations are handled internally without manual index or copy logic.

3. **Type Safety (with Generics):**  
   Dynamic arrays like `ArrayList<T>` ensure compile-time type checking.

4. **Rich API:**  
   Methods such as `add()`, `remove()`, `contains()`, and `sort()` simplify manipulation.

5. **Efficient Memory Handling:**  
   Automatically manages resizing strategy for optimal performance and minimal memory waste.

---

### 251. What is the Collections Framework?

> The **Java Collections Framework (JCF)** is a unified architecture that provides a set of interfaces, classes, and
> algorithms to store, manage, and manipulate groups of objects efficiently.
---

### 252. What are the advantages of the Collections Framework?

1. **Reusability:** Standardized data structures can be reused across applications.
2. **Performance:** Optimized implementations (e.g., HashMap, ArrayList).
3. **Consistency:** Unified API and hierarchy across all collection types.
4. **Interoperability:** Easily interchangeable implementations (e.g., List to Set).
5. **Reduced Development Time:** Prebuilt algorithms and utilities (`Collections`, `Arrays`).
6. **Type Safety:** Generics prevent runtime `ClassCastException`.

---

### 253. What are the types of Collections?

1. **List** – Ordered collection, allows duplicates (e.g., `ArrayList`, `LinkedList`).
2. **Set** – Unordered collection, no duplicates (e.g., `HashSet`, `TreeSet`).
3. **Queue / Deque** – Ordered by insertion or priority (e.g., `ArrayDeque`, `PriorityQueue`).
4. **Map** – Key-value pairs (e.g., `HashMap`, `TreeMap`) — not part of `Collection` but part of the framework.

---

### 254. Does Map belong to the Collection hierarchy?

> No. `Map` is **not a subinterface of Collection** because it stores **key-value pairs**, not individual elements.  
> However, it is part of the **Collections Framework**.

---

### 255. Can we use primitive types in Collections?

> No.  
> Collections can only store **objects**, not primitives.  
> To store primitive values, we must use **Wrapper Classes** (e.g., `Integer`, `Double`).
---

### 256. Why do we need Collections?

- To replace **arrays** with **dynamic, resizable, and flexible** data structures.
- To provide **standardized data manipulation algorithms** (sorting, searching, filtering).
- To enable **generic, reusable, and efficient** data management in applications.

---

### 257. In which package is the Collections Framework located?

> All core Collection classes and interfaces are in the **`java.util`** package.
---

### 258. Name the main interfaces of the Collections Framework.

1. `Collection<E>`
2. `List<E>`
3. `Set<E>`
4. `Queue<E>`
5. `Deque<E>`
6. `Map<K, V>`
7. `SortedSet<E>`
8. `SortedMap<K, V>`
9. `NavigableSet<E>`
10. `NavigableMap<K, V>`

---

### 259. Which main interfaces are used for sorting in the Collections Framework?

1. **`Comparable<T>`** – Defines **natural ordering** via `compareTo()`.
2. **`Comparator<T>`** – Defines **custom ordering** via `compare()`.
3. Classes like `TreeSet` and `TreeMap` use these interfaces for sorting elements or keys.

---

### 260. What is the List interface?

> The **List** interface in Java is a subinterface of `Collection` that represents an **ordered collection** of
> elements.  
> It allows **duplicate elements** and provides **positional access** (by index) to elements.

---

### 261. What are the main characteristics of the List interface?

1. **Ordered Collection:** Elements are stored and retrieved in a defined sequence (based on insertion order).
2. **Index-Based Access:** Each element has an index (starting from 0).
3. **Allows Duplicates:** Same element can appear multiple times.
4. **Allows Null Values:** Most implementations allow storing `null`.
5. **Supports Iteration:** Provides `Iterator` and `ListIterator` for traversal in both directions.
6. **Supports CRUD Operations:** Methods like `add()`, `remove()`, `get()`, `set()` enable modification.

---

### 262. What are the advantages of the List interface?

1. **Dynamic Size:** Automatically resizes when elements are added or removed.
2. **Random Access (depending on implementation):** Efficient element retrieval by index (e.g., `ArrayList`).
3. **Insertion Order Maintained:** Useful when the order of elements matters.
4. **Versatile Implementations:** Choice between performance characteristics (e.g., `ArrayList` vs. `LinkedList`).
5. **Enhanced Iteration:** `ListIterator` allows bidirectional traversal and element modification.

---

### 263. Which classes implement the List interface?

1. **`ArrayList`** – Dynamic array, fast random access, slower insertion/removal in middle.
2. **`LinkedList`** – Doubly linked list, efficient insertions/removals, slower random access.
3. **`Vector`** – Legacy synchronized dynamic array.
4. **`Stack`** – Legacy subclass of `Vector`, implements LIFO (Last-In-First-Out) behavior.
5. **`CopyOnWriteArrayList`** – Thread-safe version of `ArrayList` (from `java.util.concurrent`).

---

### 264. What is an ArrayList?

> `ArrayList` is a **resizable array implementation** of the `List` interface in Java.  
> It provides **dynamic memory allocation**, **fast random access**, and **automatic resizing** when elements are added
> or
> removed.
---

### 265. Which interface does ArrayList implement?

> `ArrayList` implements the **`List`**, **`RandomAccess`**, **`Cloneable`**, and **`Serializable`** interfaces.
---

### 266.Which marker interfaces does ArrayList implement?

1. **`Serializable`** — Enables serialization (object persistence).
2. **`Cloneable`** — Allows cloning via the `clone()` method.
3. **`RandomAccess`** — Indicates that `get(index)` has constant-time complexity (O(1)).

---

### 267. What are the main characteristics of ArrayList?

1. **Dynamic Resizing:** Automatically grows when capacity is exceeded.
2. **Ordered Collection:** Maintains insertion order.
3. **Allows Duplicates and Nulls:** Supports multiple identical elements and `null` values.
4. **Fast Random Access:** Direct access by index (O(1)).
5. **Slower Insertions/Deletions:** Inserting/removing in the middle shifts elements (O(n)).
6. **Not Thread-Safe:** Must be synchronized manually for concurrent access.

---

### 268.Does ArrayList allow duplicate elements?

> **Yes**, `ArrayList` allows duplicate elements because it preserves insertion order and does not enforce uniqueness.

---

### 269. Can we add null values to an ArrayList?

> **Yes**, `ArrayList` allows multiple `null` elements.
---

### 270. How does ArrayList store elements in memory?

> Internally, `ArrayList` uses a **dynamic Object array (`Object[] elementData`)**.  
> When capacity is full, it creates a **new larger array** (usually 1.5× bigger) and copies old elements to the new one.

---

### 271.What is the difference between ArrayList and Array?

| Feature     | Array                            | ArrayList                              |
|-------------|----------------------------------|----------------------------------------|
| Size        | Fixed                            | Dynamic                                |
| Type        | Can store primitives and objects | Stores only objects                    |
| Memory      | Static allocation                | Dynamic allocation                     |
| Performance | Faster for primitive types       | More flexible, slower for resizing     |
| Features    | No built-in methods              | Rich API (add, remove, contains, etc.) |

---

### 272.What are the disadvantages of ArrayList?

1. **Slower Insertions and Deletions** (O(n)) due to element shifting.
2. **Memory Overhead** due to dynamic resizing.
3. **Not Thread-Safe** (requires synchronization for concurrent access).
4. **Boxing/Unboxing Overhead** when storing primitive types.
5. **Possible Memory Waste** when capacity is larger than actual size.

---

### 273. What is the load factor (capacity growth ratio) of ArrayList?

> When capacity is exceeded, **new capacity = old capacity × 1.5** (i.e., 50% increase).
---

### 274.How many ways are there to retrieve elements from an ArrayList?

1. **Using for loop** with index access (`get(index)`).
2. **Using enhanced for-each loop.**
3. **Using Iterator.**
4. **Using ListIterator.**
5. **Using Streams (Java 8+).**
6. **Using forEach() method with lambda expression.**

---

### 275.What is a LinkedList?

> `LinkedList` is a **doubly linked list implementation** of the `List` and `Deque` interfaces.  
> Each element (node) contains **data** and **links to the previous and next nodes**, enabling efficient insertion and
> deletion operations.

---

### 276.How does LinkedList store elements in memory?

> Unlike `ArrayList`, which uses a contiguous array, `LinkedList` stores elements as **individual nodes** in the heap.  
> Each node holds:

- A reference to the **previous** node.
- A reference to the **next** node.
- The **element value** itself.

> Nodes are linked together via these references, forming a bidirectional chain.

---

### 277. What types of LinkedLists are there?

1. **Singly Linked List** – Each node has a reference to the next node only.
2. **Doubly Linked List** – Each node references both previous and next nodes (used by Java’s `LinkedList`).
3. **Circular Linked List** – The last node points back to the first node.

---

### 278.What advantages does LinkedList have over ArrayList?

1. **Fast Insertions and Deletions** (O(1)) at head or tail — no shifting elements.
2. **Efficient for Queues/Stacks** — implements `Deque`, making it ideal for FIFO/LIFO structures.
3. **Predictable Performance** for frequent add/remove operations at ends.
4. **No capacity resizing** — dynamically grows as elements are added.

---

### 279.What are the disadvantages of LinkedList?

1. **Slow Random Access** — Accessing by index requires traversal (O(n)).
2. **Higher Memory Usage** — Each node stores two extra references.
3. **Poor Cache Locality** — Non-contiguous memory allocation reduces CPU cache efficiency.
4. **Slower Traversal** — Pointer chasing adds overhead.
5. **Not Thread-Safe** — Must be synchronized externally.

---

### 280.What are the differences between LinkedList and ArrayList?

| Feature                | ArrayList          | LinkedList               |
|------------------------|--------------------|--------------------------|
| Internal Structure     | Dynamic array      | Doubly linked list       |
| Memory Layout          | Contiguous         | Non-contiguous           |
| Access Time            | O(1) random access | O(n) traversal           |
| Insert/Delete (middle) | O(n)               | O(1) if node known       |
| Insert/Delete (end)    | O(1) amortized     | O(1)                     |
| Memory Overhead        | Low                | High (extra references)  |
| Use Case               | Frequent reads     | Frequent inserts/deletes |
| Implements             | `List`             | `List`, `Deque`, `Queue` |

---

### 281.Why is the initial capacity of LinkedList zero?

> `LinkedList` has **no predefined capacity** because it does not use an internal array.  
> Elements are stored in **independent nodes**, each dynamically allocated in heap memory.  
> Thus, it grows and shrinks **on demand**, and its initial size is effectively **zero** until elements are added.
---

### 282.What is a Node?

> A **Node** is a fundamental unit of the `LinkedList` data structure.  
> Each node contains:

- The **data (element)** itself.
- A **reference to the previous node**.
- A **reference to the next node**.

> Together, these nodes form a **bidirectional chain**, enabling traversal in both directions.

---

### 283. Which data structure does LinkedList use internally?

> Internally, `LinkedList` uses a **doubly linked list** data structure — implemented as a sequence of interconnected
`Node` objects.  
> Each node maintains two references: one to its predecessor and one to its successor.

---

### 284.What is the load factor (growth ratio) of LinkedList?

> Unlike `ArrayList`, `LinkedList` **does not have a load factor or capacity growth ratio** because it does not rely on
> array resizing.  
> Each insertion dynamically creates a new node; therefore, its size increases **node by node**.

---

### 285.What is the superclass of LinkedList?

> `LinkedList` extends the **`AbstractSequentialList`** class, which provides a skeletal implementation of
> sequential-access lists.  
> This superclass ensures consistent list behavior while delegating storage mechanics to subclasses.

---

### 286.Why is retrieving an element from LinkedList slower?

> Accessing an element by index requires **traversing nodes sequentially** from either the head or tail until the target
> index is reached.  
> This traversal is **O(n)** time complexity, unlike `ArrayList`, which offers **O(1)** access using direct indexing in
> a
> contiguous array.  
> Additionally, pointer dereferencing (poor cache locality) further slows down access compared to array-based
> structures.

---

### 287.What is a Vector?

> `Vector` is a **legacy synchronized dynamic array** class in Java that implements the `List` interface.  
> It was introduced before the Collections Framework and provides **thread-safe operations** by synchronizing all public
> methods.

---

### 288.Why has the Vector class been considered deprecated since JDK 5?

> Although not formally marked as `@Deprecated`, `Vector` is considered **obsolete** because:

- It relies on **coarse-grained synchronization**, causing performance bottlenecks.
- It lacks support for **modern concurrency mechanisms** (e.g., `ConcurrentHashMap`, `CopyOnWriteArrayList`).
- The **Collections Framework** provides more efficient and flexible alternatives like `ArrayList` and
  `Collections.synchronizedList()`.

---

### 289.What is the initial capacity of a Vector?

> By default, the **initial capacity** of a `Vector` is **10 elements**.  
> When exceeded, the capacity increases either by **doubling (100%)** or by a **user-defined increment** if specified in
> the constructor.

---

### 290.What are the differences between Vector and ArrayList?

| Feature         | Vector                     | ArrayList                           |
|-----------------|----------------------------|-------------------------------------|
| Synchronization | Synchronized (thread-safe) | Not synchronized (faster)           |
| Growth Factor   | Doubles capacity (2×)      | Increases by 50%                    |
| Introduced      | JDK 1.0                    | JDK 1.2                             |
| Performance     | Slower due to locking      | Faster for single-threaded use      |
| Thread Safety   | Yes                        | No (can wrap with synchronizedList) |
| Legacy          | Yes                        | Modern alternative                  |
| Iterators       | Fail-fast                  | Fail-fast                           |

---

### 291.Why is Vector slower than ArrayList?

> Every public method in `Vector` is **synchronized**, meaning only one thread can access it at a time.  
> This **lock contention** introduces overhead even in single-threaded contexts.  
> In contrast, `ArrayList` operates without synchronization, offering faster access and iteration.

---

### 292. Is Vector thread-safe? If yes, why?

> `Vector` is thread-safe because **all its methods are synchronized**.  
> However, this synchronization occurs at the method level, which reduces throughput under concurrent access due to
> global
> locking.

---

### 293.What happens if we modify a Vector while iterating through it?

- **Iterator / for-each loop:** Throws a **`ConcurrentModificationException`** (fail-fast behavior).
- **Enumeration:** Does **not** throw this exception because it is **not fail-fast**, but it does not detect concurrent
  structural changes, which may cause inconsistent reads.

---

### 294. What is a Set?

> A **Set** is a collection that **does not allow duplicate elements** and **does not guarantee positional access**.  
> It models the mathematical concept of a set — unique, unordered elements.
---

### 295. What are the main characteristics of a Set?

1. **Uniqueness:** No duplicate elements are allowed.
2. **Unordered:** Does not maintain index-based order (depends on implementation).
3. **Null Handling:** Allows at most one `null` element (except in certain implementations).
4. **No positional access:** Elements are accessed via iteration, not by index.
5. **Performance:** Lookup, add, and remove operations typically have **O(1)** time complexity in hash-based
   implementations.

---

### 296.Name the subclasses (implementations) of the Set interface.

1. **`HashSet`** – Unordered, hash-based implementation.
2. **`LinkedHashSet`** – Maintains insertion order using a linked list internally.
3. **`TreeSet`** – Maintains sorted order (based on natural ordering or a `Comparator`).
4. **`CopyOnWriteArraySet`** – Thread-safe version using copy-on-write semantics.
5. **`EnumSet`** – Optimized for enumerated types.

---

### 297.What is a HashSet?

> `HashSet` is a **hash table–based implementation** of the `Set` interface.  
> It stores elements in a **`HashMap`** internally and ensures uniqueness by using **hashing** to detect duplicates.  
`HashSet` provides **constant-time** performance for basic operations (`add`, `remove`, `contains`).

---

### 298.What internal structure does HashSet use to store elements?

Internally, `HashSet` uses a **`HashMap`** instance where:

- Each element of the set is stored as a **key** in the map.
- The corresponding **value** is a constant dummy object (usually `PRESENT`).  
  This allows `HashSet` to reuse the efficient hash-based lookup logic of `HashMap`.

---

### 299. Is HashSet thread-safe?

> **No.**  
`HashSet` is **not synchronized**.  
> If multiple threads modify it concurrently, it must be wrapped using `Collections.synchronizedSet()` or replaced with
> a
> concurrent alternative like `ConcurrentHashMap.newKeySet()`.

---

### 300. Does HashSet maintain insertion order?

> **No.**  
`HashSet` does **not guarantee order** of elements — the iteration order depends on the hash codes and internal bucket
> structure.  
> If insertion order is required, use **`LinkedHashSet`** instead.
---

### 301. Explain how the add() method of HashSet works.

1. When `add(element)` is called, `HashSet` delegates to the **`put()`** method of its internal `HashMap`.
2. The element’s **hash code** is computed to determine the storage bucket.
3. If no existing key with the same hash and `equals()` result exists, the element is stored as a new key.
4. If an equivalent element already exists, it is **not added** (ensuring uniqueness).
5. The method returns `true` if the element was added, or `false` if it already existed.

---

### 302. Why can’t HashSet store duplicate elements?

> Because `HashSet` uses a **hash-based comparison mechanism** —  
> when inserting an element, it checks:
> If another element with the **same hash code** and **equal content** already exists in the set.  
> If yes, the new element is **rejected**.  
> This behavior relies on the **`hashCode()`** and **`equals()`** contract to enforce uniqueness.

---

### 303. What is a LinkedHashSet?

> `LinkedHashSet` is an **ordered implementation** of the `Set` interface that maintains **insertion order**.  
> It extends `HashSet` and internally uses a **combination of a hash table and a doubly linked list** to store
> elements.  
> This allows it to preserve the order in which elements were inserted while still preventing duplicates.

---

### 304.What is the difference between LinkedHashSet and HashSet?

| Feature            | HashSet                          | LinkedHashSet                                |
|--------------------|----------------------------------|----------------------------------------------|
| Order              | Unordered                        | Maintains insertion order                    |
| Internal Structure | Hash table (`HashMap`)           | Hash table + Doubly linked list              |
| Performance        | Slightly faster for pure hashing | Slightly slower due to link maintenance      |
| Memory Usage       | Lower                            | Higher (extra pointers for links)            |
| Use Case           | When order is irrelevant         | When predictable iteration order is required |

---

### 305. Is LinkedHashSet thread-safe?

> **No.**  
> `LinkedHashSet` is **not synchronized**.  
> If multiple threads access it concurrently and at least one modifies it, synchronization is required.  
> Use `Collections.synchronizedSet(new LinkedHashSet<>())` or a concurrent set alternative for thread safety.

---

### 306.For which operations is LinkedHashSet efficient?

> `LinkedHashSet` offers **O(1)** time complexity for:

- **Insertion** (`add()`),
- **Removal** (`remove()`), and
- **Lookup** (`contains()`),

> while maintaining **predictable iteration order**.  
> It’s especially efficient when both **fast access** and **ordered traversal** are required, such as caching (e.g., LRU
> cache implementations).

---

### 307.What is a Comparator?

> `Comparator` is a **functional interface** in `java.util` used to define **custom comparison logic** for sorting
> objects.  
> It allows sorting objects that do **not implement Comparable**, or sorting them in **multiple different ways**.

- Package: `java.util`
- Key method: `int compare(T o1, T o2)`
- Since: **Java 1.2**
- It can also use **lambda expressions** or **method references** (Java 8+).

---

### 308.What is a Comparable?

> Comparable is an interface in java.lang that defines the natural ordering of objects.
> Classes implementing it define a single comparison logic used by default when sorting.
---

### 309.What is the difference between Comparator and Comparable interfaces?

| Feature               | Comparable                                                   | Comparator                                                    |
|-----------------------|--------------------------------------------------------------|---------------------------------------------------------------|
| Package               | `java.lang`                                                  | `java.util`                                                   |
| Purpose               | Defines the **natural ordering** of objects.                 | Defines a **custom ordering** of objects.                     |
| Method                | `int compareTo(T o)`                                         | `int compare(T o1, T o2)`                                     |
| Affects Class         | Implemented **inside the class** whose objects are compared. | Implemented **outside the class** (separate class or lambda). |
| Modifies Source Code  | Requires modifying the class.                                | Does not require modifying the class.                         |
| Number of Sort Orders | Only **one** natural order.                                  | Can define **multiple** custom orders.                        |
| Example Use Case      | Sorting by `id` in the entity itself.                        | Sorting by `name`, `date`, or other attributes externally.    |

---

### 310.When should we use each of these two interfaces?

> **Use `Comparable`**  
> When the class has a **default or natural ordering** that makes sense in all contexts.  
> Example: sorting integers, strings, or domain objects by their unique identifier.

> **Use `Comparator`**  
> When you need **custom or multiple sorting strategies** without altering the class definition.  
> Example: sorting employees by `salary`, `name`, or `hireDate` dynamically in different contexts.

---

### 311.What is a TreeSet?

> `TreeSet` is a class in `java.util` that implements the `NavigableSet` interface.  
> It stores elements in **sorted (ascending) order** according to their **natural order** or a **custom Comparator**.  
> It does **not allow duplicate elements** and ensures **logarithmic-time performance** for basic operations.

---

### 312.Does TreeSet allow duplicate elements?

> No.  
> `TreeSet` does **not allow duplicate elements**.  
> If an element that compares as *equal* (using `compareTo()` or `compare()`) is added, it is ignored.

---

### 313.Is TreeSet thread-safe?

> No.  
> `TreeSet` is **not synchronized**.  
> If multiple threads access it concurrently and at least one modifies it, external synchronization (e.g., via
`Collections.synchronizedSortedSet()`) is required.

---

### 314.What is the difference between TreeSet and HashSet?

| Feature                             | TreeSet                          | HashSet                |
|-------------------------------------|----------------------------------|------------------------|
| Ordering                            | Sorted (natural or custom order) | Unordered              |
| Internal Structure                  | Balanced Tree (`TreeMap`)        | Hash Table (`HashMap`) |
| Performance (add, remove, contains) | O(log n)                         | O(1) average           |
| Null Elements                       | Not allowed                      | One `null` allowed     |
| Comparator Support                  | Yes                              | No                     |
| Thread Safety                       | Not thread-safe                  | Not thread-safe        |

---

### 315.What internal data structure does TreeSet use to store elements?

> `TreeSet` internally uses a **`TreeMap`** (specifically a **Red-Black Tree**) to store its elements.  
> The elements are stored as **keys** in the `TreeMap`, with dummy values.
---

### 316.What happens if we modify a TreeSet while iterating through it?

If the `TreeSet` is **structurally modified** (add/remove) during iteration (except via the iterator’s own
`remove()`),  
a **`ConcurrentModificationException`** is thrown.  
This behavior ensures **fail-fast** iteration.
---

### 317. What is a Queue?

> A `Queue` in Java is a linear data structure that orders elements in a **First-In, First-Out (FIFO)** manner.
> The `Queue` interface (in `java.util`) models a collection designed for holding elements before processing.  
> It is commonly used in concurrent processing, task scheduling, and message buffering scenarios.  
> Unlike stacks (LIFO), queues process elements in the order they were inserted.  
`Queue` extends the `Collection` interface and defines operations for insertion, retrieval, and removal consistent with
> FIFO ordering.

---

### 318. What is FIFO?

> FIFO stands for **First In, First Out** — the element inserted first is removed first.
> In a FIFO structure, insertion happens at the **rear (tail)** and removal at the **front (head)**.  
> This model ensures processing order fairness, typical in producer-consumer systems, task queues, and network buffers.

---

### 319. What are the methods of the Queue interface?

| Method      | Behavior       | Throws Exception on Failure    | Returns Special Value |
|-------------|----------------|--------------------------------|-----------------------|
| `add(e)`    | Insert element | Yes (`IllegalStateException`)  | —                     |
| `offer(e)`  | Insert element | No                             | `false` if full       |
| `remove()`  | Remove head    | Yes (`NoSuchElementException`) | —                     |
| `poll()`    | Remove head    | No                             | `null` if empty       |
| `element()` | Inspect head   | Yes (`NoSuchElementException`) | —                     |
| `peek()`    | Inspect head   | No                             | `null` if empty       |

---

### 320. How many types of Queues are there?

1. **Non-blocking queues** — e.g., `PriorityQueue`, `ConcurrentLinkedQueue`.
2. **Blocking queues** — e.g., `ArrayBlockingQueue`, `LinkedBlockingQueue`, `PriorityBlockingQueue`, `DelayQueue`.
3. **Double-ended queues (Deque)** — e.g., `ArrayDeque`, `LinkedList`.

---

### 321. What are the main characteristics of a Queue?

> - FIFO ordering

- No random access
- Supports safe insertion/removal from ends
- Often used for producer-consumer workflows

> Queues ensure fair ordering and controlled access.  
> Depending on implementation, they can:

- Be **bounded** or **unbounded**
- Support **thread-safety** (`BlockingQueue`, `ConcurrentLinkedQueue`)
- Be **priority-based** (using comparators)
- Reject `null` elements (modern implementations)

---

### 322. Can we add null elements to a Queue?

> No, most modern `Queue` implementations **do not permit null elements**.

Allowing `null` breaks the API contract where `poll()` and `peek()` use `null` to signal “empty”.  
Hence, adding `null` leads to ambiguity.  
All `BlockingQueue` and concurrent queue implementations explicitly forbid `null`.
---

### 323.: Can we add duplicate elements to a Queue?

> Yes, duplicates are generally allowed unless explicitly restricted (e.g., by `Set` semantics).
> The `Queue` interface does not enforce uniqueness.  
> So, `PriorityQueue` and most `BlockingQueue` types allow duplicates, maintaining them in insertion or priority order.

---

### 324.

>
---

### 325.

>
---

### 326.

>
---

### 327.

>
---

### 328.

>
---

### 329.

>
---

### 330.

>
---

### 331.

>
---

### 332.

>
---

### 333.

>
---

### 334.

>
---

### 335.

>
---

### 336.

>
---

### 337.

>
---

### 338.

>
---

### 339.

>
---

### 340.

>
---

### 341.

>
---

### 342.

>
---

### 343.

>
---

### 344.

>
---

### 345.

>
---

### 346.

>
---

### 347.

>
---

### 348.

>
---

### 349.

>
---

### 350.

>
---

### 351.

>
---

### 352.

>
---

### 353.

>
---

### 354.

>
---

### 355.

>
---

### 356.

>
---

### 357.

>
---

### 358.

>
---

### 359.

>
---

### 360.

>
---

### 361.

>
---

### 362.

>
---

### 363.

>
---

### 364.

>
---

### 365.

>
---

### 366.

>
---

### 367.

>
---

### 368.

>
---

### 369.

>
---

### 370.

>
---

### 371.

>
---

### 372.

>
---

### 373.

>
---

### 374.

>
---

### 375.

>
---

### 376.

>
---

### 377.

>
---

### 378.

>
---

### 379.

>
---

### 380.

>
---

### 381.

>
---

### 382.

>
---

### 383.

>
---

### 384.

>
---

### 385.

>
---

### 386.

>
---

### 387.

>
---

### 388.

>
---

### 389.

>
---

### 390.

>
---

### 391.

>
---

### 392.

>
---

### 393.

>
---

### 394.

>
---

### 395.

>
---

### 396.

>
---

### 397.

>
---

### 398.

>
---

### 399.

>
---

### 400.

>
---

### 401.

>
---

### 402.

>
---

### 403.

>
---

### 404.

>
---

### 405.

>
---

### 406.

>
---

### 407.

>
---

### 408.

>
---

### 409.

>
---

### 410.

>
---

### 411.

>
---

### 412.

>
---

### 413.

>
---

### 414.

>
---

### 415.

>
---

### 416.

>
---

### 417.

>
---

### 418.

>
---

### 419.

>
---

### 420.

>
---

### 421.

>
---

### 422.

>
---

### 423.

>
---

### 424.

>
---

### 425.

>
---

### 426.

>
---

### 427.

>
---

### 428.

>
---

### 429.

>
---

### 430.

>
---

### 431.

>
---

### 432.

>
---

### 433.

>
---

### 434.

>
---

### 435.

>
---

### 436.

>
---

### 437.

>
---

### 438.

>
---

### 439.

>
---

### 440.

>
---

### 441.

>
---

### 442.

>
---

### 443.

>
---

### 444.

>
---

### 445.

>
---

### 446.

>
---

### 447.

>
---

### 448.

>
---

### 449.

>
---

### 450.

>
---

### 451.

>
---

### 452.

>
---

### 453.

>
---

### 454.

>
---

### 455.

>
---

### 456.

>
---

### 457.

>
---

### 458.

>
---

### 459.

>
---

### 460.

>
---

### 461.

>
---

### 462.

>
---

### 463.

>
---

### 464.

>
---

### 465.

>
---

### 466.

>
---

### 467.

>
---

### 468.

>
---

### 469.

>
---

### 470.

>
---

### 471.

>
---

### 472.

>
---

### 473.

>
---

### 474.

>
---

### 475.

>
---

### 476.

>
---

### 477.

>
---

### 478.

>
---

### 479.

>
---

### 480.

>
---

### 481.

>
---

### 482.

>
---

### 483.

>
---

### 484.

>
---

### 485.

>
---

### 486.

>
---

### 487.

>
---

### 488.

>
---

### 489.

>
---

### 490.

>
---

### 491.

>
---

### 492.

>
---

### 493.

>
---

### 494.

>
---

### 495.

>
---

### 496.

>
---

### 497.

>
---

### 498.

>
---

### 499.

>
---

### 500.

>
---

### 501.

>
---

### 502.

>
---

### 503.

>
---

### 504.

>
---

### 505.

>
---

### 506.

>
---

### 507.

>
---

### 508.

>
---

### 509.

>
---

### 510.

>
---

### 511.

>
---

### 512.

>
---

### 513.

>
---

### 514.

>
---

### 515.

>
---

### 516.

>
---

### 517.

>
---

### 518.

>
---

### 519.

>
---

### 520.

>
---

### 521.

>
---

### 522.

>
---

### 523.

>
---

### 524.

>
---

### 525.

>
---

### 526.

>
---

### 527.

>
---

### 528.

>
---

### 529.

>
---

### 530.

>
---

### 531.

>
---

### 532.

>
---

### 533.

>
---

### 534.

>
---

### 535.

>
---

### 536.

>
---

### 537.

>
---

### 538.

>
---

### 539.

>
---

### 540.

>
---

### 541.

>
---

### 542.

>
---

### 543.

>
---

### 544.

>
---

### 545.

>
---

### 546.

>
---

### 547.

>
---

### 548.

>
---

### 549.

>
---

### 550.

>
---

### 551.

>
---

### 552.

>
---

### 553.

>
---

### 554.

>
---

### 555.

>
---

### 556.

>
---

### 557.

>
---

### 558.

>
---

### 559.

>
---

### 560.

>
---

### 561.

>
---

### 562.

>
---

### 563.

>
---

### 564.

>
---

### 565.

>
---

### 566.

>
---

### 567.

>
---

### 568.

>
---

### 569.

>
---

### 570.

>
---

### 571.

>
---

### 572.

>
---

### 573.

>
---

### 574.

>
---

### 575.

>
---

### 576.

>
---

### 577.

>
---

### 578.

>
---

### 579.

>
---

### 580.

>
---

### 581.

>
---

### 582.

>
---

### 583.

>
---

### 584.

>
---

### 585.

>
---

### 586.

>
---

### 587.

>
---

### 588.

>
---

### 589.

>
---

### 590.

>
---

### 591.

>
---

### 592.

>
---

### 593.

>
---

### 594.

>
---

### 595.

>
---

### 596.

>
---

### 597.

>
---

### 598.

>
---

### 599.

>
---

### 600.

>
---
