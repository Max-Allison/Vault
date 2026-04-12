---
tags:
  - Daily
  - CSCI103
---
# Polymorphism (5e)
### Base and Derived Type Compatibility
- Are base and derived objects type compatible? Put another way, can we assign a derived object into a base object?
- Can we assign a base object into a derived?
- Think hierarchy & animal classification? 
	-  Can any dog be (assigned as) a mammal 
	- Can any mammal be (assigned as) a dog
- We can only assign a derived into a base (since the derived has EVERYTHING the base does)
### Pointer & Reference Compatibility
- A pointer or reference to a derived class object is type compatible witch (can be assigned to) a base-class type pointer/reference
	- A base class pointer or reference can point to or reference a derived object
	- Derived d; Base* b = &d
- But not vice versa
	- A derived class pointer or reference cannot point to or reference a base object
	- base b; derived* d = &b; does not work
- And clearly a derived pointer or reference is NOT type compatible with a different derived type pointer/reference
### Which Function Gets Called?
- Person pointer or reference can also point to Student or Faculty Object (i.e. a student is a person)
	- All methods known to Person are supported by a Student object because it was derived from Person
- What happens if we use the base pointer/reference to call a member function that both base and derive implement? which version will get invoked?
- Will apply the function from the class corresponding to the type of the pointer used
### Non-Virtual Functions; Base Pointer -> Base Functions
- For second and third call to print_info() we might like to have Student::print_info() and Faculty::print_info() executed since the actual object pointed to is a Student/Faculty 
-  BUT…it will call Person::print_info()
- This is called 'static binding' (i.e. the version of the function called is based on the static type of the pointer being used)
### Virtual Functions: Base Ptr -> Derived Functions
- Member functions can be declared virtual
- virtual declaration allows derived classes to redefine the function and which version is called is determined by the type of object pointed to/referenced rather than the type of pointer/reference
- This is called Dynamic Binding (i.e. which version is called is based on the type of object being pointed to)
### Polymorphism
- Ability to take many different kinds of data and treat it the same way
- Can we have an array that can story multiple types? No!
- But we can use base pointers to point at different types and have their individual behavior invoked via virtual functions
- Polymorphism via virtual functions allows one set of code to operate appropriately on all derived types of objects
- One data structure can now reference mant types and the code can perform appropriate behavior on each as you iterate over the structure
### Pointers, Objects, and References
- To allow dynamic binding and polymorphism the base class must specify the function as virtual and
- Then use a base class to the derived objects
	- pointer
	- reference
- Copying a derived object to a base object makes a copy and so no polymorphic behavior is possible
### Summary
- No virtual declaration
	- Member function that is called is based on the pointer type
	- static binding
- With virtual declaration
	- Member function that is called is based on the type of object pointed at (referenced)
	- dynamic binding
- This is a good thing to put on a cheat sheet!
### Abstract Classes & Pure Virtuals
- In software development we may want to create a base class that servers only as a requirement/interface that derived classes must implement and adhere to
	- For Example:
		- Suppose we want to create a CollegeStudent class and ensure all derived objects implement behavior for the student to take a test and play sports
		- But depending on which college you go to you may do these activities differently. Until we know the university we don't know how to implement take_test() and play_sports()
		- We can decide to not implement them in this class known as "pure" virtual functions (indicated by setting their prototype =0;)
- A class with pure virtuals is called an abstract base class (i.e. interface for future derived classes)
- An abstract base class is one that defines at least 1 or more pure virtual functions
	- Prototype only
	- Make function body "= 0;"
	- Functions that are not implemented by the base class but must be implemented by the derived class to be able to create an instance of the derived object
- Objects of the abstract class type may not be declared/instantiated
	- Doing so would not be safe since some functions are not implemented
### How Long is a Class Abstract?
- Objects of the abstract class type may not be declared/instantiated
	- Doing so would not be safe since some functions are not implemented
- Until each pure virtual function has a definition, the class stays abstract
### When to use Inheritance
- Main use of inheritance is to setup interfaces (abstract classes) that allow for new, derived classes to be written in the future that provide additional functionality but still work seamlessly with original code
### Abstract Classes
- An abstract base class can still define common functions, have data members, etc. that all derived classes can use via inheritance
### General OO Design goal
- Loose Coupling: A relationship between objects where changes in one component do not require (or reduced the need for) changes in others
- To achieve loose coupling we have principles that we often try to follow in our software design
### OO Design Principles
- Single-Responsibility
	- A class (or even a function) should generally have only one responsibility
- Open/close rule
	- A class should be open to extension but closed to modification. A class should be designed so that its behavior can be changed through inheritance/polymorphism, not modification.
- These are a few principles from what some developers refer to as the 5 SOLID principles
	- feel free to search online for more readings. There's not one agreed upon set of principles and even how various principels are applied may be a subject of a debate
- For C++ OO implementation guidelines:
	- https://isocpp.org/faq
		- Scroll to Classes and Inheritance Section
### Polymorphism & Private Inheritance
- Warning: if private or protected inheritance is used, the derived class is no longer type-compatible with base class
	- Can't have a base class pointer reference a derived object
- Example
	- Given: Class Queue : private LinkedList
	- Can not do the following
		- LinkedList * p = new Queue();
## VTables and BPTRS
### VTables
- Compiler creates a table for each class with an entry for each virtual function (aka vtable)
- Each entry points to the appropriate function code to call
- Each object has an extra data member (vptr) that points to the vtable for its class
- Calling a non-virtual function, always goes to the same code (known at compile time/statically)
- Calling a virtual function, requires following the vtable ptr at runtime (dynamically) to find the correct function to call


[[April 2, 2026 Lecture Notes|Previous Lecture]] | [[April 9, 2026 Lecture Notes|Next Lecture]]