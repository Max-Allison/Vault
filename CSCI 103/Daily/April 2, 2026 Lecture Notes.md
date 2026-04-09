---
tags:
  - Daily
  - CSCI103
---
# Inheritance (5d)
### Constructor Initialization
- You can still assign values in the constructor but realize that the default constructors will have been called already
- So generally if you know what value you want to assign a data member it's good practice to do it in the initialization list
### Object Oriented Design Concepts
- Encapsulation and Abstraction
	- Combine data and operations on that data into a single unit and only expose a desired public interface and prevent modification/alteration of the implementation
- Inheritance
	- Creating new objects (classes) from existing ones to specify functional relationships and extend behavior
- Polymorphism
	- Using the same expression to support different types with different behavior for each type
### Coupling
- Refers to how much components depend on each other's implementation details (i.e. how much work it is to remove one component and drop in a new implementation of it)
### Inheritance
- A way of defining interfaces, re-using classes and extending original functionality
- Allows a new class to inherit all the data members and member functions from a previously defined class
- Works from more general objects to more specific objects
	- Defines an "is-a" relationship
	- Square is-a rectangle is-a shape
	- Square inherits from Rectangle which inherits from shape
	- Similar to classification of organisms
		- Animal -> Vertebrate -> Mammals
### Base and Derived Classes
- Derived Classes inherit all data members and functions of base class
- Student class inherits:
- get_name() and get_id()
- name_ and id_ member variables
### Constructors and Inheritance
- How do we initialize base class data members?
- Can't assign base class members if they are private
- Constructors are only called when a variable is created and cannot be called directly from another constructor
	- How to deal with base constructors?
- Also want/need base class or other members to be initialized before we perform this object's constructor code
- Use initializer format instead
### Constructors and Destructors
- Constructors
	- A derived class will automatically call its base class constructor before it's own constructor executes either:
		- Explicitly called a specified base class constructor in the initialization list
		- Implicitly calling the default base class constructor if no base class constructor is called in initialization list
- Destructors
	- The derived class will call the base class destructor automatically after it's own destructor executes
- General Idea
	- Constructors go base -> derived
	- Destructors go derived -> base
## Public, Private, Protected
### Protected Members
- Private members of a base class can not be accessed directly by a derived class member function
- Base class can declare variable with protected storage class which means:
	- Private to any object or code not inheriting from the base
	- public to any derived (child) class
### Public, Protected, & Private Access
- Derived class sees base class members using the base class specification
	- If Base class said it was public or protected, the derived class can access it directly
	- If Base class said it was private, the derived class cannot access it directly
### Public, Protected, & Private Inheritance
- public/protected/private inheritance before base class indicates how the public base class members are viewed by clients (those outside) of the derived class
- Public
	- public and protected base class members are accessible to the child class and grandchild classes
	- Only public base class members are accessible to 3rd party clients
- Protected
	- public and protected base class members are accessible to the child class and grandchild classes
	- No base class members are accessible to 3rd parties
- Private
	- public and protected base class members are accessible to the child class
	- No base class members are accessible to grandchild classes or 3rd party clients
### Inheritance Access
- Derive as public if
	- You want users of your derived class to be able to call base class functions/methods
- Derive as private if
	- You only want your internal workings to call base class functions/methods
- Derive as protected more rarely
	- Same reasons as private inheritance but also allow grandchild classes to use Base class methods
### When to Inherit Privately
- If public: Outside user can call the base list functions and break the queue order 
- If private: hide the base class public function, so users can only call derived class interface
- if protected: hide the base class public and protected functions except to derive and friend classes
- For protected or private inheritance, "(implemented) as-a" relationship
	- Queue "implemented as-a" List
## Odds and Ends of Inheritance
### Overloading Base Functions
- A derived class may want to redefine the behavior of a member function of the base class
- A base member function can be overloaded in the derived class
- When derived objects call that function the derived version will be executed
- When a base object calls that function the base version will be executed
### Scoping Base Functions
- We can still call the base function version by using the scope operator ::
	- base_class_name::function_name()
## Composition Vs. Inheritance
### Composition
- Code reuse is a common need in (object-oriented) programming
	- We could use a pre-written List class to make a Queue class
- An easy and often preferable way is to simply use the existing class as a data member
- Composition defines a "has-a" relationship
	- A queue "has-a" List in its implementation
- But could we inherit?
	- Public inheritance would mean a Queue "is-a" List and a Queue should be able to do anything a List can do, but that's not the case
	- Private inheritance could be used but is not a universal approach supported by other languages
	- Often programmers say "prefer composition rather than inheritance" when the goal is code reuse
## Summary
- Public Inheritance = is-a
- Composition = has-a
- Private/Protected Inheritance =
	- as-a
	- implemented-as
	- implemented-in-terms-of
- Public inheritance mainly when
	- We want to add or specialize behavior
	- a true "is-a" relationship holds for the relationship of base and derived
- Composition or Private Inheritance
	- When reuse is the main desire
### Warning: Multiple Inheritance
- C++ allows multiple inheritance but it is not usually recommended
- Anti Loose Coupling
# Extra Code
~~~cpp
#include <iostream>
#include <string>

using namespace std;

class Food{
	
	string flavor = "";
	size_t calories = 0;
public:
	Food(string taste, size_t cal);
};

Food::Food(string taste, size_t cal){
	flavor = taste;
	calories = cal;
}

class Pizza : public Food{

	string toppings;

public:
	Pizza(string taste, size_t cal, string toppings);

};

Pizza::Pizza(string tase, size_t cal, string toppings) 
		: Food(taste, cal) {
		this->toppings = toppings;
}

int main() {
	
	Pizza p("Savory", 100000000000, "Olives);
	p.flavor; //Doesn't work as it is private
	
	return 0;
}
~~~



[[March 31, 2026 Lecture Notes|Previous Lecture]] | [[April 7, 2026 Lecture Notes|Next lecture]]