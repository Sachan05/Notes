## OOPs :

### Module 1: Class/Objects 
✔ What is OOP?
✔ Class vs Object
✔ Attributes
✔ Methods
✔ self
✔ Constructors


* **OBJECT :** An object in Python is a fundamental data structure in memory that contains data (called attributes) and code that can manipulate that data (called methods). In Python, "everything is an object".
Core Properties of a Python Object :
- **Identity (id):** The object's unique address in computer memory. You can check it using id(object)
- **Type (type):** Determines what kind of values the object can hold and what operations it supports.
- **Value:** The actual data stored inside the object. If the value can change over time, the object is mutable (like a list); if it cannot change, it is immutable (like an integer or string).


* **CLASS :** To build your own objects, you use a Class. A class is simply the blueprint, while the object is the actual physical instance created from that blueprint.

    # 1. Defining the blueprint (Class)
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
  - Q1. Difference between Class and Object?
  - Q2. What is self?
  - Q3. Why do we use init?
  - Q4. Difference between attribute and method?
    - an attribute represents data or state associated with an object, whereas a method represents an action or behavior that the object can perform
  - Q5. Can a class exist without an object?
    - NO
  - Q6. Can an object exist without a class?
    - In normal Python code, no. Every object is an instance of some class (even built-in types like int or list).


  - **Q7 : Assignment (=) vs Mutation (append, extend, pop, etc.)**
    **"Assignment changes the reference for one object; mutation changes the object itself."**

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
    
    --------------------------------------------------
    
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
    
    --------------------------------------------------
    
    Golden Rule:
    • "=" creates/overrides an instance attribute.
    • Mutation changes the existing object.
    • Avoid mutable class variables unless shared state is intentional.
    
-----------
###########
-----------
    
### Module 2: Encapsulation
✔ Encapsulation
✔ Access modifiers
✔ Getters/Setters
✔ @property decorator
----


* **Encapsulation :**
-------------
Definition:
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

Name Mangling
-------------
__x  -> _ClassName__x

Purpose:
- Reduce accidental access.
- Avoid name clashes in inheritance. Without name mangling, the child could accidentally overwrite the parent's internal variable.
- Not true privacy.

---- 
* **Examples :**
  class Employee:
    def __init__(self):
        self.name = "Alice"
  
  **1) Public Members : everything works**
     - emp = Employee()
     - print(emp.name)
     - emp.name = "Bob"

  **2) Protected Members (_):**
     - self._salary = 50000
     - You can still access it: print(emp._salary).
     - Nothing stops you. Why? Because _ is just a convention. it means, "This is an internal implementation detail. Please don't access it from outside unless necessary."
    
  **3) Private Members (__) :**
     - self.__salary = 50000
     - now try, print(emp.__salary)  --->  output : AttributeError:'Employee' object has no attribute '__salary'
     - Python performs name mangling here, Internally, it changes: self.__salary ---> self._Employee__salary   (it adds the class name.)
     - so you can still access it using : print(emp._Employee__salary) ----> 50000
     - **So __ is not true privacy. It is name mangling to reduce accidental access and name clashes.**
    
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
###########
-----------

### Module 3: Inheritance

✔ What is inheritance?
✔ Why do we use it?
✔ Types of inheritance
✔ super()
✔ Method overriding
✔ Constructor chaining
✔ Method Resolution Order (MRO)
✔ Diamond problem
✔ Common interview questions
-----

* Inheritance : Inheritance allows one class (child) to acquire the properties and behavior of another class (parent), promoting code reuse and extensibility. Without inheritance, Lots of duplication. With inheritance, Shared code stays in one place.

* Method Overriding : A child class can provide a specific implementation of a method that is already defined in its parent class. **The child's implementation overrides the parent's.**

  - Overriding → Same method name, child provides a different implementation.
  - Overloading → Same method name, different parameters (Python doesn't support traditional method overloading like Java).


* super() : Sometimes we want both the properties of parents and child. super() returns a proxy object that allows you to access methods and constructors of the parent class.
  Its uses :
  1) Initializing Parent Classes : The most common use case for super() is inside a child class’s __init__ constructor. It passes parameters up to the parent constructor so you do not have to manually reassign inherited attributes.

   ``` class Employee:
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
        print(dev.programming_language) # Output: Python
  ```









* Types of Inheritance :
  
  1. Single Inheritance : A single child class inherits properties and behaviors from exactly one parent class. This is the simplest form of inheritance. ex : class Child(Parent)

  2. Multiple Inheritance : A single child class inherits attributes and methods from more than one parent class simultaneously. ex : class Child(Father, Mother):
 
  3. Multilevel Inheritance : A child class inherits from a parent class, which in turn inherits from another grandparent class. It forms a linear chain of ancestry.
 
  4. Hierarchical Inheritance : Multiple child classes inherit properties from a single parent class. The children share the parent's logic but remain completely independent of each other.
 
  5. Hybrid Inheritance : Hybrid inheritance is a combination of two or more types of inheritance explained above. It often creates complex relationships, such as the famous "Diamond Problem" where a child inherits from two parents that share a common grandparent.(Hierarchical + Multiple)









