## SOLID : Design Principles
- S : Single Responsibility Principle
- O : Open Closed Principle
- L : Liskov's Substitution Principle
- I : Interface Segregation Principle
- D : Dependency Inversion Principle

* Design Principles : Set of rules or guidelines to help us write good code.
  - Extensible (easy to add new features in code), Maintainable (easy debugging), Readable, Modular, Reusable


* SRP(Single Responsibility Principle) : Every code unit(class/function/interface) should have a single responsibility (there should be only one reason to change).

  * how to identify violation of SRP :
    - too many if-else conditions : If if-else conditions are part of some algorithm/logic then its not a violation of SRP.
    - Monster method : If a method is doing a lot more than its name suggests, then its a violation of SRP.
    - Ex : A utility file containing all sorts of unrelated helper methods violates SRP. Instead, separating methods into specific utility files such as StringUtils.java, DateUtils.java, etc., each holding only relevant methods, embodies SRP

 
* OCP(Open Closed Principle) : Our codebase should be open for extension and closed for modification. rather than modifying the exisitng codebase, we should add new code units (class/interface/functions). Adding new features should require very less  if NO code changes in the existing codebase.
  - Violation: Modifying existing code when adding new functionality violates this principle. Instead, you should be able to extend a class or module to introduce new functionality
  - Adding new bird types shouldn't require changes to existing bird classes; instead, introduce new classes that extend from existing base classes
    

* LSP(Liskov's Substitution Principle): Objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. Ensure subclasses can stand in for parent classes without unexpected behavior. This might involve ensuring that methods in subclasses maintain the same behavioral contracts as in superclasses

* ISP(Interface Segregation Principle) : Ideally every interface should have a single method. Interfaces should be as light as possible. Clients should not be forced to implement interfaces they don't use; a single class should not be burdened with implementing large interfaces. Create smaller, more specific interfaces. For birds, separate interfaces for fly and dance allow implementing classes to have only the necessary capabilities

* DIP(Dependency Inversion Principle): No 2 concrete classes should depend on each other directly, they should depend on each other via interface. Depend upon abstractions, not concretions. High-level modules should not depend on low-level modules; both should depend on abstractions.  Use interface-based architectures where classes rely on abstractions rather than concrete implementations. This approach reduces tight coupling and allows for more flexible, interchangeable implementations


####################
####################
####################


