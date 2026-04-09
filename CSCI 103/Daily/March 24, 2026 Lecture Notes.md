---
tags:
  - Daily
  - CSCI103
---
# Midterm 1 Statistics
- Historically the worst 1
- Average on this midterm usually is 74% this midterm average was 70% (you got 76% yippee!)

# C++ References (4e)
### Pass-by-Reference (Using Pointers)
- To allow a function to modify the data of another, we learned we must pass pointers
### A New Way to Pass by Reference
- To declare a C++ reference, use the & symbol after the type in a declaration!
	- Poor choice by C++ because & is already used for the 'address of operator' when used in an expression (i.e. non-declaration)
- Behind the scenes the compiler will essentially access variable with a pointer
- But you get to access it like a normal variable without dereferencing
- Think of a reference variable as an alias

# Operator Overloading (5a)
### Function Overloading
- What makes up a signature (uniqueness) of a function
	- name
	- number and type of arguments
- No two functions are allowed to have the same signature; the following 4 functions are unique and allowable...
	- void f1(int)
	- void f1(double)
	- void f1(double, int)
	- void f1(int, int)
- We say that "f1" is overloaded 4 times
### Operator Overloading
- Same as function overloading
- There are two ways to specify an operator overload function
	- Global level function (not a member of any class)
	- As a member function of the class on which it will operate
- Which should we choose?
	- It depends on left hand side operand
		- String + int
### Ostream Overloading
- Should go on a cheat sheet!


[[March 26, 2026 Lecture Notes|Next Lecture]]