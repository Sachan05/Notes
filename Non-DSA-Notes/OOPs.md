# OOPs :

====================================================
### Module 1: Class/Objects 
====================================================  

✔ What is OOP?   
✔ Class vs Object  
✔ Attributes  
✔ Methods  
✔ self  
✔ Constructors   

----

* **OBJECT :** An object in Python is a fundamental data structure in memory that contains data (called attributes) and code that can manipulate that data (called methods). In Python, "everything is an object".
Core Properties of a Python Object :
- **Identity (id):** The object's unique address in computer memory. You can check it using id(object)
- **Type (type):** Determines what kind of values the object can hold and what operations it supports.
- **Value:** The actual data stored inside the object. If the value can change over time, the object is mutable (like a list); if it cannot change, it is immutable (like an integer or string).


* **CLASS :** To build your own objects, you use a Class. A class is simply the blueprint, while the object is the actual physical instance created from that blueprint.

* **1. Defining the blueprint (Class) :**
    ```class Dog:
        def __init__(self, name, breed):
            self.name = name    # Attribute (Data)
            self.breed = breed  # Attribute (Data)
    
        def bark(self):         # Method (Behavior)
            return f"{self.name} says Woof!"
    
        # 2. Creating the Object (Instantiation)
        my_dog = Dog("Buddy", "Golden Retriever")
        
        # 3. Accessing attributes and methods
        print(my_dog.name)   # Output: Buddy
        print(my_dog.bark()) # Output: Buddy says Woof!
  ```

* **Self :** self is a reference variable that **points directly to the current object/instance of a class. It allows individual objects to access and modify their own unique data and methods.** Contrary to popular belief, self is not a reserved keyword in Python, but rather a strictly followed naming convention.
  - In this ex :
    ```
        class Employee:                    e1 = Employee(), e2 = Employee()
            def greet(self):
                print("Hello")
    ```
    
  - **when we write e1.greet(), python secretly converts it into Employee.greet(e1)**
  - **So, self = current object. It tells Python, "Operate on THIS object."**
  - Can we name self something else?
    - Yes. def display(this): also works, but self is a convention in python



* **Constructors :** In Python, a constructor is a special method used to initialize an object's state and allocate its initial attributes when a class instance is created. **While people typically refer to the __init__() method as the constructor, Python splits the instantiation process into two distinct parts: object creation (__new__()) and object initialization (__init__()).**

  **Core Components :**
  - __new__(cls, ...): The actual instance creator. It runs first, allocates memory, and returns the newly created empty object instance.
  - __init__(self, ...): The instance initializer. It runs immediately after __new__() and sets up the starting values (attributes) for your object.
  - self: A mandatory first parameter in __init__() that represents the specific object instance being configured


* **Questions :**
Q1. Difference between Class and Object?  
Q2. What is self?  
Q3. Why do we use init?  
Q4. Difference between attribute and method?
- an attribute represents data or state associated with an object, whereas a method represents an action or behavior that the object can perform  
Q5. Can a class exist without an object?
- Yes, a class can completely exist without you creating an instance (object) of it.When you define a class in Python, the class definition is immediately executed, and Python creates a class object in memory. This allows you to use the class as a standalone container for variables and functions without ever instantiating it.      
Q6. Can an object exist without a class?
- In normal Python code, no. Every object is an instance of some class (even built-in types like int or list).  


**Q7 : Assignment (=) vs Mutation (append, extend, pop, etc.)**
**"Assignment changes the reference for one object; mutation changes the object itself."**  

        ```
        1. Assignment (=)
        -----------------
        e1.company = "Google"
        
        • Creates/updates an INSTANCE variable.
        • Does NOT modify the class variable.
        • A new attribute is created for that object only.
        
        Example:
        Employee.company = "Wipro"
        
        e1.company = "Google"
        
        e1.company        -> Google
        e2.company        -> Wipro
        Employee.company  -> Wipro
        
        -------------------------------------------------------
        2. Mutation (append, extend, pop, remove, update, etc.)
        --------------------------------------------------------
        
        e1.company.append("Google")
        
        • Python first looks up company.
        • If it's a class variable, it mutates the SAME shared object.
        • All instances referencing that object see the change.
        
        Example:
        class Employee:
            company = []
        
        e1.company.append("Google")
        
        e1.company -> ['Google']
        e2.company -> ['Google']
        ```


**Golden Rule:**  
• "=" creates/overrides an instance attribute.  
• Mutation changes the existing object.  
• Avoid mutable class variables unless shared state is intentional.  


----------
====================================================
### Module 2: Encapsulation  
====================================================

✔ Encapsulation  
✔ Access modifiers  
✔ Getters/Setters  
✔ @property decorator  

----

**Encapsulation :**
Encapsulation means hiding an object's internal data and allowing controlled access through methods or properties. Bundling data and methods together while restricting direct access to internal data.

Why?
- Protect object state.
- Validate data before modification.
- Hide implementation details.

* **Access Modifiers in Python :**  
--------------------------  
Public    : variable      -> Accessible everywhere.  
Protected : _variable     -> Convention only (not enforced).  
Private   : __variable    -> Name mangling (_ClassName__variable).  

Name Mangling :
-------------
__x  -> _ClassName__x

Purpose:
- Reduce accidental access.
- Avoid name clashes in inheritance. Without name mangling, the child could accidentally overwrite the parent's internal variable.
- Not true privacy.

---- 
* **Examples :**  
  ```class Employee:  
    def __init__(self):  
        self.name = "Alice"```
  
**1) Public Members : everything works**

     ```emp = Employee()
        print(emp.name)
        emp.name = "Bob"```

**2) Protected Members (_):**
     ```- self._salary = 50000  
     - You can still access it: print(emp._salary).    
     - Nothing stops you. Why? Because _ is just a convention. it means, "This is an internal implementation detail. Please don't access it from outside unless necessary."  
     ```
    
**3) Private Members (__) :**  
     ```- self.__salary = 50000  
     - now try, print(emp.__salary)  --->  output : AttributeError:'Employee' object has no attribute '__salary'  
     - Python performs name mangling here, Internally, it changes: self.__salary ---> self._Employee__salary   (it adds the class name.)  
     - so you can still access it using : print(emp._Employee__salary) ----> 50000  
     - **So __ is not true privacy. It is name mangling to reduce accidental access and name clashes.**  
     ```
    
**Q: Does Python support private variables?**
     - Python doesn't have true private variables. Using __variable triggers name mangling, making accidental access harder by renaming it to _ClassName__variable.
 
**Q: "If __salary can still be accessed using _Employee__salary, what's the point of making it private?"**
      - __salary isn't meant to provide absolute security. It prevents accidental access and accidental overriding, especially in inheritance. Python follows the philosophy of 'we're all consenting adults here' rather than enforcing strict access control.


-----


* **Getters/Setters :**  
getters and setters are methods used to restrict and control access to an object's internal data, ensuring data validation and integrity. While you can write traditional getter and setter methods like in Java or C++, the standard, clean way to handle this in Python is by using the @property decorator

* **@property Decorators :**
The @property decorator transforms a method into a read-only property (getter). You can then define a corresponding .setter to safely update the attribute with input validation. This approach allows you to use standard dot notation (obj.variable = value) while keeping your internal validation rules hidden.

* **Q : Why do Python developers prefer @property over get_salary() and set_salary()?**  
  - Python prefers @property because it provides attribute-like access while still allowing validation and encapsulation. The user of the class can write emp.salary instead of emp.get_salary(), making the API cleaner. Internally, the implementation can later change to add validation or computed values without changing the external interface.

* **Ex :**
    ```
     class Employee:
          def __init__(self, name, salary):
              self.name = name
              # Using a single leading underscore indicates a 'protected' attribute by convention
              self._salary = salary 
      
          # Getter method
          @property
          def salary(self):
              return self._salary
      
          # Setter method with validation logic
          @salary.setter
          def salary(self, value):
              if value < 0:
                  raise ValueError("Salary cannot be negative.")
              self._salary = value
      
      # --- Usage ---
      emp = Employee("Alice", 50000)
      
      # Accessing like a normal public attribute (triggers the getter)
      print(emp.salary)  # Output: 50000
      
      # Modifying like a normal public attribute (triggers the setter)
      emp.salary = 55000 
      print(emp.salary)  # Output: 55000
  ```


-----------
====================================================
### Module 3: Inheritance
====================================================

✔ What is inheritance?  
✔ Why do we use it?  
✔ super()  
✔ Method overriding  
✔ Constructor chaining  
✔ Types of inheritance  
✔ Method Resolution Order (MRO)  
✔ Diamond problem  
✔ Common interview questions  

-----

**Inheritance :** 
Inheritance allows one class (child) to acquire the properties and behavior of another class (parent), promoting code reuse and extensibility. Without inheritance, Lots of duplication. With inheritance, Shared code stays in one place.

**Method Overriding :** 
A child class can provide a specific implementation of a method that is already defined in its parent class. **The child's implementation overrides the parent's.**

  - **Overriding** → Same method name, child provides a different implementation.
  - **Overloading** → Same method name, different parameters (Python doesn't support traditional method overloading like Java).


**super() :** Sometimes we want both the properties of parents and child. super() returns a proxy object that allows you to access methods and constructors of the parent class.

  **Its uses :**  
  **1) Initializing Parent Classes :** The most common use case for super() is inside a child class’s __init__ constructor. It passes parameters up to the parent constructor so you do not have to manually reassign inherited attributes.  

   
    ```class Employee:
          def __init__(self, name, salary):
              self.name = name
              self.salary = salary

        class Developer(Employee):
            def __init__(self, name, salary, programming_language):
                # super() automatically finds Employee and runs its __init__
                super().__init__(name, salary)
                self.programming_language = programming_language
        
        dev = Developer("Alice", 95000, "Python")
        print(dev.name)                 # Output: Alice
        print(dev.programming_language) # Output: Python```
  

**2) Extending Parent Methods (Instead of Replacing)**  
       When you override a method in a child class, Python completely ignores the parent's version. super() allows you to run the parent's logic and add custom child behavior around it.

        ```class TimestampLogger(Logger):
                def log(self, message):
                    # Run the parent's log logic first
                    super().log(message)
                # Add specific child behavior
                print("Timestamp: 2026-07-09") ```
       


**3) The Real Power: Multiple Inheritance and MRO**
       In languages with simple inheritance, super() just points to the immediate parent. In Python, super() does not just look at the parent—it follows the Method Resolution Order (MRO) line.

        
        ``` class Base:
                def __init__(self):
                    print("Base init")
            
            class ChildA(Base):
                def __init__(self):
                    print("ChildA init")
                    super().__init__()
            
            class ChildB(Base):
                def __init__(self):
                    print("ChildB init")
                    super().__init__()
            
            class Grandchild(ChildA, ChildB):
                def __init__(self):
                    print("Grandchild init")
                    super().__init__()
            
            gc = Grandchild()
            # Output order shows how super() winds through ChildA, then ChildB, then Base:
            # Grandchild init
            # ChildA init
            # ChildB init
            # Base init ```

       


* **Constructors :**
  In Python inheritance, constructors (the __init__ method) follow a specific rule: if a child class does not define its own constructor, it automatically inherits the parent's constructor.However, if the child class defines its own __init__ method, it overrides the parent's constructor. To keep the parent's initialization logic, you must call it explicitly.
  
  **1. Automatic Constructor Inheritance :** If your child class only adds new methods (and no new attributes), you do not need to write a new constructor. Python automatically runs the parent's constructor
       
        ``` class Parent:
                def __init__(self, name):
                    self.name = name
                    print("Parent constructor called")
            
            class Child(Parent):
                def greet(self):
                    print(f"Hello, my name is {self.name}")
            
            # This triggers Parent.__init__ automatically
            obj = Child("Alice")  # Output: Parent constructor called
            obj.greet()           # Output: Hello, my name is Alice ```

        
     
  **2. Overriding and Using super() :** If your child class needs its own unique attributes, you must define a new constructor. To avoid breaking the parent class logic, use the super() function to trigger the parent constructor first.
        
         ```class Parent:
                def __init__(self, name):
                    self.name = name
            
            class Child(Parent):
                def __init__(self, name, age):
                    # 1. Initialize parent attributes
                    super().__init__(name)  
                    # 2. Initialize child attributes
                    self.age = age          
            
            obj = Child("Bob", 12)
            print(obj.name)  # Output: Bob
            print(obj.age)   # Output: 12 ```

       



* **Constructor Chaining :**  
  **If the child defines __init__(), the parent's __init__() is NOT called automatically.
Use super().__init__() to initialize the parent.**


* **Q : Does Python automatically call the parent constructor?**
  - No. If the child defines its own __init__(), the parent constructor is not called automatically. You must explicitly call it using super().__init__().

-----

* **Types of Inheritance :**
  
  **1. Single Inheritance :**
  A single child class inherits properties and behaviors from exactly one parent class. This is the simplest form of inheritance. ex : class Child(Parent)

  **2. Multiple Inheritance :**
  A single child class inherits attributes and methods from more than one parent class simultaneously. ex : class Child(Father, Mother):
 
  **3. Multilevel Inheritance :**
  A child class inherits from a parent class, which in turn inherits from another grandparent class. It forms a linear chain of ancestry.
 
  **4. Hierarchical Inheritance :**
  Multiple child classes inherit properties from a single parent class. The children share the parent's logic but remain completely independent of each other.
 
  **5. Hybrid Inheritance :**
  Hybrid inheritance is a combination of two or more types of inheritance explained above. It often creates complex relationships, such as the famous "Diamond Problem" where a child inherits from two parents that share a common grandparent.(Hierarchical + Multiple)


* **MRO (Method Resolution Order):**  
  Multiple inheritance allows a class to inherit features from more than one parent class.
  Suppose both parents have the same method. Which one should Python call?
  Python follows a fixed order called the Method Resolution Order (MRO). It defines the search hierarchy when a class utilizes multiple or multilevel inheritance. Every time you call a method or use super(), Python uses this precalculated list to determine which class should execute the code.

  * **The C3 Linearization Algorithm :** Python uses the C3 Linearization algorithm to build the MRO list. It guarantees that the lookup order is always predictable by enforcing three strict rules:  
    **1) Children Before Parents:** A subclass is always searched before its base/parent classes.  
    **2) Left-to-Right Order:** Leftmost classes defined in the inheritance tuple take priority over rightmost classes (e.g., in class X(A, B), A is searched before B).  
    **3) Monotonicity:** The relative order of parent classes must be preserved across the entire hierarchy. If Class A comes before Class B anywhere in the chain, it cannot flip-flop elsewhere.  
    * **to check MRO of a class :**  
      - The **__mro__ attribute:** Returns the order as a tuple.
      - The **mro() method:** Returns the order as a list.




* **Diamond Problem : Both B and C inherit from A. D inherits from both B and C.**

    
         ```class A:
                def hello(self):
                    print("A")        
            class B(A):
                def hello(self):
                    print("B")
                    super().hello()         
            class C(A):
                def hello(self):
                    print("C")
                    super().hello()
                   
            class D(B, C):
                pass```
    
      
* **Q : what order does D().hello() follow ? How many times should A.show() execute?**
  - Python solves this using the **C3 Linearization Algorithm. Every class appears only once in the MRO.**
  - **print(D.mro()) :  D -> B -> C -> A -> object**
  - **Execution:**
    - D doesn't have hello().
    - Goes to B.hello().
    - Prints B.
    - super() means "next class in the MRO", not necessarily "my parent class".
    - So it goes to C.hello().
    - Prints C.
    - super() again goes to A.hello().
    - Prints A.
    - Final output: B -> C -> A
  - **In Python, super() follows the MRO, not simply the direct parent. "super() returns a proxy that delegates method calls to the next class in the Method Resolution Order (MRO). In single inheritance, this is usually the parent. In multiple inheritance, it follows the MRO."**
 



-----------
====================================================
### Module 4: Polymorphism
====================================================

✔ What is polymorphism?  
✔ Compile-time vs Runtime polymorphism  
✔ Method overriding  
✔ Duck typing (Python-specific ⭐⭐⭐⭐⭐)  
✔ Why Python doesn't support traditional method overloading  
✔ *args, default arguments as alternatives  
✔ Interview questions  

---


* **Polymorphism :**
allows the same interface (method/function) to behave differently depending on the object that invokes it. Same method. Different behavior.
Python achieves polymorphism through three main mechanisms: Duck Typing, Method Overriding, Method Overloading, and Function/Operator Polymorphism

**1) Method Overriding :** 
In object-oriented programming, method overriding happens when a child class provides a specific implementation for a method that is already defined in its parent class


**2) Duck Typing :** 
Python is a dynamically typed language, meaning it cares about what an object can do, not what it is. This follows the phrase: "If it walks like a duck and quacks like a duck, it's a duck." If an object has the required methods, it works.
**A Python feature where an object's suitability is determined by the methods/behavior it supports, rather than its declared type.**
Python uses duck typing, meaning it doesn't care whether obj is a Car or a Robot. It only cares that the object implements the required start() method as start() method is there on both the car and robot class.

   ```
    def save(file):
        file.write(data)
   ```
    Python doesn't care whether file is:
       - a local file
       - an in-memory buffer
       - a network stream
       - As long as it implements write(). That's why many Python libraries feel so flexible.


**3) Built-in Function and Operator Polymorphism :** Python's built-in tools inherently exhibit polymorphism. The exact same operation yields entirely different behaviors depending on the data type passed to it. Python internally calls the appropriate implementation.
The + operator behaves differently depending on the object type.  
       ```
    print(5 + 10)
    print("Hello" + "World")
    print([1] + [2])
        ```

**4) Method Overloading :** having multiple methods in the same class with the same name but different arguments).
   - **Python does not support traditional Method Overloading.** If you write two methods with the same name, Python will simply overwrite the first one with the second one.
   - **To achieve overloading behavior**, Python devs use **default arguments** (argument=None) or the ***args** and ****kwargs** syntax. Python classes are dictionaries of names. The second definition overwrites the first.


* **Q : Does Python support method overloading?** 
  - **Python does not support traditional compile-time method overloading like Java or C++. If multiple methods with the same name are defined, the last one overrides the previous definitions. Similar behavior is typically achieved using default arguments, *args, or argument inspection.**

* **Q : Python vs Java :**
  
    | Java                                              | Python                         |
    | ------------------------------------------------- | ------------------------------ |
    | Checks types/interfaces before use (compile-time) | Checks behavior at runtime     |
    | Requires implementing an interface                | No explicit interface required |
    | Statically typed                                  | Dynamically typed              |



-----------
====================================================
### Module 5: Abstraction
====================================================

✔ What is abstraction?  
✔ Difference between abstraction & encapsulation ⭐⭐⭐⭐⭐  
✔ Abstract classes  
✔ Abstract methods  
✔ ABC module  
✔ @abstractmethod  
✔ Interfaces in Python  
✔ Real-world examples  
✔ Interview coding questions  

----

Abstraction means hiding implementation details and exposing only the essential functionality to the user. Hide HOW(complexity), expose WHAT. It acts as a blueprint or a contract, focusing on what an object does rather than how it does it.

    - Ex : .sort() function : we dont the sorting algorithm used
    - Ex : file.write(data) : we dont know how bytes are buffered, OS writes to disk, which system calls are used. The implementation is hidden.


* **Q : Encapsulation vs Abstraction**
  
    | Encapsulation                                          | Abstraction                                  |
    | ------------------------------------------------------ | -------------------------------------------- |
    | Hides data                                             | Hides implementation                         |
    | Protects object state                                  | Reduces complexity                           |
    | Achieved using access control (`_`, `__`, `@property`) | Achieved using abstract classes/interfaces   |
    | Focuses on **how data is accessed**                    | Focuses on **what operations are available** |


* **ABC Module: from abc import ABC, abstractmethod**
  
  - **Abstract Class:** A template class that cannot be instantiated directly. Can contain constructors, attributes, normal methods, and abstract methods.
  - **Abstract Method:** Declares a method that subclasses must implement. subclass cannot be instantiated until all abstract methods are implemented.
  - **Concrete Method:** A fully functional method inside an abstract class that subclasses can inherit and use directly


  - Ex : Imagine you're building a payment system. Every payment gateway should support: process_payment()
  - You don't care how each gateway works. You just know they must implement it. Now your backend can do: gateway.process_payment(1000). without caring which gateway it is. This is abstraction + polymorphism working together.

    ```
    from abc import ABC, abstractmethod

    class PaymentGateway(ABC):
        @abstractmethod
        def process_payment(self, amount):
            pass

    class Razorpay(PaymentGateway):
        def process_payment(self, amount):
            print("Razorpay")
    
    class Stripe(PaymentGateway):
        def process_payment(self, amount):
            print("Stripe")
    ```

* **Q: Interface vs Abstract Class**  
  Python doesn't have a separate interface keyword like Java. Python uses Abstract Base Classes (ABCs) to define contracts similar to interfaces in Java.
* **Q : Can an abstract class have normal methods?**  
  - Yes, only the abstract method must be implemented by child class. other normal method is inherited as-is.

* **Q : Can an abstract class have a constructor?**  
  - Yes
 
* **Q : (Interview Favorite) Suppose you're building a notification service. You have: 1) Email, 2) SMS, 3) Push Notification.
  Would you use: A normal parent class? Or an abstract class? Why?**  
  
  - we will use an abstract class with the abstract method send_notification(). then each of the child class can implement their own way how to send it, either via email, phone or sms.  
  **- Q : "Why not use a normal parent class?"**  
    - Because I want to enforce that every notification provider implements send_notification(). If a developer creates a new provider (e.g., Slack or WhatsApp) and forgets to implement it, Python will raise an error when they try to instantiate the class. This prevents incomplete implementations.  


* **Q : What's the difference between inheritance, polymorphism, and abstraction?**

    | Concept          | Purpose                                                |
    | ---------------- | ------------------------------------------------------ |
    | **Inheritance**  | Reuse code by creating an IS-A relationship.           |
    | **Polymorphism** | Use the same interface with different implementations. |
    | **Abstraction**  | Hide implementation details and define a contract.     |

    - PaymentGateway → Abstraction
    - Stripe(PaymentGateway) → Inheritance
    - stripe.process_payment() / razorpay.process_payment() → Polymorphism




-----------
====================================================
### Module 6: COMPOSITION vs INHERITANCE
====================================================

Inheritance
-----------
Definition:
A child class acquires properties and behavior from a parent class.

Relationship:
IS-A

Examples:
- Dog IS-A Animal
- Manager IS-A Employee
- SavingsAccount IS-A BankAccount

Syntax:
class Dog(Animal):
    pass

Use inheritance only when there is a TRUE IS-A relationship.

----------------------------------------------------

Composition
-----------
Definition:
A class is built using objects of other classes instead of inheriting from them.

Relationship:
HAS-A

Examples:
- Car HAS-A Engine
- UserService HAS-A Database
- Order HAS-A PaymentGateway
- CrashTriageService HAS-A LLM, VectorDB, Logger
- FastAPI App HAS-A Database, Redis, Kafka

Syntax:

class Car:
    def __init__(self):
        self.engine = Engine()

The object is composed of other objects.

----------------------------------------------------

Golden Rule
-----------

Inheritance  -> IS-A relationship
Composition  -> HAS-A relationship

Whenever you are unsure:

Read the sentence aloud.

Dog IS-A Animal ✔

Car IS-A Engine ✘

Car HAS-A Engine ✔

----------------------------------------------------

Why Composition is Preferred
----------------------------

Composition creates:

✓ Loose Coupling
✓ Better Maintainability
✓ Better Extensibility
✓ Better Testability
✓ Better Reusability
✓ Easier Dependency Injection
✓ Easier Component Replacement

Instead of tightly depending on one implementation,
the class only depends on the required behavior.

----------------------------------------------------

Loose Coupling
--------------

Loose coupling means that one class has minimal knowledge
or dependency on another class's implementation.

Changing one component should require little or no change
in the consuming class.

Example:

Today

UserService
    ↓
PostgresDatabase

Tomorrow

UserService
    ↓
MongoDatabase

UserService code remains unchanged.

----------------------------------------------------

Tight Coupling
--------------

Occurs when a class directly creates or depends on a
specific implementation.

Example:

class UserService:

    def __init__(self):
        self.db = PostgresDatabase()

Now changing the database requires modifying UserService.

----------------------------------------------------

## Dependency Injection (DI)
-------------------------

Definition:

**Instead of creating dependencies inside a class,
provide them from outside.**

Bad:

class UserService:

    def __init__(self):
        self.db = Database()

Good:

class UserService:

    def __init__(self, db):
        self.db = db

Benefits:

- Loose coupling
- Easier testing (Mock DB)
- Easy replacement
- Better maintainability

FastAPI Example:

db = Depends(get_db)

FastAPI's Depends() is Dependency Injection.

----------------------------------------------------

Composition + Abstraction
-------------------------

The best software design often combines both.

Example:

class PaymentGateway(ABC):

    @abstractmethod
    def pay(self):
        pass

class Razorpay(PaymentGateway):
    ...

class Stripe(PaymentGateway):
    ...

class PaymentService:

    def __init__(self, gateway):
        self.gateway = gateway

PaymentService HAS-A PaymentGateway.

This combines:

✓ Abstraction
✓ Composition
✓ Dependency Injection
✓ Polymorphism

----------------------------------------------------

Real Backend Examples
---------------------

Authentication Service

HAS-A

- Database
- Logger
- Cache
- JWT Provider

- Need Logger, Database, Cache. Should we write : class AuthService(Database, Logger, Cache): NOPE
- Instead :
      ```
        class AuthService:
  
            def __init__(self):
        
                self.db = Database()
                self.logger = Logger()
                self.cache = Cache()
      ```

----------------------------------------------------

Crash Triage Tool

HAS-A

- LLM
- Embedding Model
- Vector DB
- Logger

Changing OpenAI → Gemini should only change
the injected dependency, not CrashTriageService.

----------------------------------------------------

Text Analyzer

HAS-A

- ChromaDB
- Embedding Model
- LLM
- Prompt Builder

----------------------------------------------------

Aggregation vs Composition
--------------------------

Both are HAS-A relationships.

Difference lies in ownership and lifecycle.

----------------------------------------------------

Composition

Strong HAS-A relationship.

Parent OWNS child.

Child cannot meaningfully exist independently.

Parent controls lifecycle.

Examples:

House → Room
Document → Pages
Car → Engine (interview example)

----------------------------------------------------

Aggregation

Weak HAS-A relationship.

Parent only references child.

Child has an independent lifecycle.

Examples:

Company → Employee
School → Student
Team → Player

----------------------------------------------------

Comparison

Composition

- Strong ownership
- Same lifecycle
- Parent creates/owns child

Aggregation

- Weak ownership
- Independent lifecycle
- Parent only references child

----------------------------------------------------

When to Use Inheritance

✓ True IS-A relationship
✓ Shared behavior
✓ Polymorphism
✓ Method overriding makes sense

Examples:

Animal
   ↑
Dog

Employee
   ↑
Manager

----------------------------------------------------

When to Use Composition

✓ Combining independent components
✓ Services
✓ Databases
✓ Loggers
✓ APIs
✓ Cache
✓ LLMs
✓ Storage Providers
✓ Notification Providers

Generally preferred in backend systems.

----------------------------------------------------

Interview Question

Why is Composition preferred over Inheritance?

Answer:

Composition creates loose coupling, making the code
more flexible, maintainable, testable, and extensible.

Components can be replaced independently without
modifying the consuming class.

It also avoids deep inheritance hierarchies and
works well with Dependency Injection.

----------------------------------------------------

Open/Closed Principle (SOLID)

Classes should be

OPEN for Extension

CLOSED for Modification

Example:

PaymentService receives PaymentGateway.

Adding Razorpay, Stripe or PayPal requires creating
a new implementation without modifying PaymentService.

----------------------------------------------------

Interview Keywords
------------------

IS-A
HAS-A
Loose Coupling
Tight Coupling
Composition
Inheritance
Dependency Injection
Maintainability
Extensibility
Testability
Reusability
Open/Closed Principle
Abstraction
Polymorphism

----------------------------------------------------

Most Important Interview Takeaways
----------------------------------

1. Inheritance models IS-A relationships.

2. Composition models HAS-A relationships.

3. Prefer Composition over Inheritance.

4. Use Dependency Injection instead of creating
   dependencies inside the class.

5. Combine Abstraction + Composition + DI for
   scalable backend systems.

6. Modern backend frameworks (FastAPI, Django,
   Spring Boot, .NET) rely heavily on composition.

7. Deep inheritance hierarchies are usually a
   design smell unless the IS-A relationship is
   very strong.



**I use inheritance when there's a genuine IS-A relationship and shared behavior. For most service dependencies and infrastructure components, I prefer composition with dependency injection because it results in loose coupling, easier testing, and better maintainability.
In modern backend applications, abstraction defines the contract, composition assembles the components, dependency injection provides them, and polymorphism allows interchangeable implementations.**

----









