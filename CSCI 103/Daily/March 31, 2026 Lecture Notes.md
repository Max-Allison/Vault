---
tags:
  - Daily
  - CSCI103
---
# Preamble
- Big things on Midterm 2:
	- Linked lists
	- Classes
	- Vectors
* Spring 2023 MT2 will be best practice test
* Coding now will be mostly for fill out or spot the bug, not full code writing

# Classes Revisited (5c)
### Before C++, There was C
- C introduced idea of a struct but diff from now
	- C
		- No class, only struct
		- structs only allowed data members and everything was public
		- some declaration nuances
	- C++
		- Introduced classes (data + functions)
		- structs become equivalent to a class
		- Default access of struct is public, class is private
### Classes & OO Ideals
- Encapsulation
	- Keep data and code that works on that data together
- Abstraction
	- Mostly for organization
	- Don't want to think about every line of code forever, puts code together into abstract trunks
- Polymorphism & Inheritance
	- Later
### Coupling
- Should be able to make changes to some code without needing to change everything else
	- Think placing new battery in car vs engine, one takes a whole lot of other stuff to be removed

## Constructor Initialization Lists

### Composite Objects
- Before the constructor of an object executes, all of its data members must be constructed
- Constructors for objects get called at the time of creation (and are only ever called here)
	- Once the object's constructor starts executing, it is too late to call data members' constructors. The data members have already been constructed
### Summary
- You can still assign values in the constructor but realize that the default constructors will have been called already
- So, if you know what value you want to assign a data member it's good practice to do it in the initialization list

## Destructors
- Destructors are called when an object goes out of scope or is freed from the heap
- Destructors
	- Can have one or none (if no destructor defined by the programmer, compiler will generate an empty destructor)
	- Have no return value
	- Have the name ~ClassName()
	- Data members of an object have their destructor's called automatically upon completion of destructor
- Why use a destructor?
	- Clean up resources that wont go away automatically (e.g. when data members are pointing to dynamically allocated memory that should be deallocated when the object goes out of scope)
	- Destructors are only needed if there are external resources (beyond your immediate data members) that must be cleaned up or free (e.g. release resources, close files, deallocate what pointers are pointing to, etc.)
	- Not necessary in simple cases
## Other Notes
- class.h contains interface description
	- don't put using namespace in header files
		- Makes all files using the header use namespace
- class.cpp contains implementation details

## Conditional Compilation
### Header Guards
- Many headers may include the same file
	- Wont compile if you try to include multiple times (Second def error)
		- Compiler doesn't know which include to use
- This may lead to multiple inclusions and definitions
### Conditional Compiler Directives
- Compiler directives start with "#"
	- "#define" XXX
		- Sets a flag named XXX in the compiler
	- "#ifdef", "#ifndef" XXX ... "#endif"
		- Continue compiling code below until "#endif", if XXX is (is not) defined
- Nest header declarations inside a
	- "#ifndef" XXX
	- "#define" XXX
	- ...
	- "#endif"
### Conditional Compilation
- Often used to compile additional DEBUG code
	- Place code that is only needed for debugging and that you would not want to execute in a release version
- Place code in a "#ifdef" NAME..."#endif" bracket
- Compiler will only compile if a "#define" NAME is found
- Can specific "#define" in:
	- source code
	- At compiler command line with (-DNAME) flag
		- g++ -o stuff -DDEGUG stuff.cpp

## Other Class Details
### Default Arguments
- Can be provided
	- User can provide a different value or not provide any, in which case the default is taken
- Only list the default argument in the prototype but not both the prototype and definition

## Nested Types
### Duplicate Types
- Recall linked lists use a helper struct to model each item in the list
	- Stores a value (of a certain type) and a pointer to the next
- If we want to use a different type list, we would need a different item struct, but would need to name it differently
- Solution:
	- Different names: intitem vs Doubleitem
	- Templates
	- Nested Types
### Nested Types
- A struct or class can be defined inside another and is known as a nested type
- Good practice to nest "helper" types (i.e. structs/classes that exist solely in support of the outer class)
- Nested types can share the same name but have different implementations when defined inside of different objects
- Examples
	- Linked list item struct
### Declaring and Using Nested Types
- Non-members must scope the type name:
	- classname::typename
- Member function code do not have to scope the type once inside the member function scope
## Static Members
### One For All
- How to construct similar objects with different data?
	- i.e. Students with different Ids
~~~cpp
#include <iostream>
#include <string>

struct Circle {

	Circle(){position_x = 0; position_y = 0; radious = 1.0; circle_count++;}

	double get_area(){return pi*radius*radius;}
	double position_x;
	double position_y;
	double radies;
	static double pi;
	static size_t circle_count; //Can't initialize here
};

size_t Circle::circle_count = 0;
double Circle::pi = 3.14159;

int main() {

	Circle c1;
	Circle c2;
	
	std::cout << c2.circle_count;

	return 0;
}
~~~
- Sometimes there are functions or data members that make sense to be part of a class but are shared (only 1 exists) amongst all instances
	- The variable or function doesn't depend on the instance of the object, but just the general class (family of objects)
	- We can make these "static" members which means one definition shared by all instances
### Static Data Members
- A static data member is a single variable that all instances of the class share
- Can think of it as belonging to the class and not each instance
- Declare with keyword static
- Initialize outside the class in a .cpp (cant be header)
	- Must be scoped with class name
### Class Constants
- Sometimes there are constants that are useful to define for a class but the same value for all instances
- std::string::npos is such a constant
	- Used as an input value for a length parameter that means "until the end of the string"
	- Returned by call to
		- string::find() or string::rfind() to indicate "no match"
### Singleton
- In addition, to static data members, static member functions are also allowed
- does NOT take a "this" pointer (not executing on an instance)
	- Called by scoping with the class name
- Can access private members of the class
### Extra Coding
~~~cpp
#include <iostream>
#include <string>

const double pi = 3.14159; //Pi always the same so rare situation where global variable for it is totally fine

struct Circle {

	Circle(){position_x = 0; position_y = 0; radious = 1.0; circle_count++;}

	double get_area(){return pi*radius*radius;}
	double position_x;
	double position_y;
	double radies;
	static size_t circle_count; //Can't initialize here
};

size_t Circle::circle_count = 0; //Initalize outside of the struct as it is seperate from any instance

int main() {

	Circle c1;
	Circle c2;
	
	std::cout << c2.circle_count;

	return 0;
}
~~~



[[March 26, 2026 Lecture Notes|Previous Lecture]] | [[April 2, 2026 Lecture Notes|Next Lecture]]
