---
tags:
  - FinalNote
  - CSCI103
---
# Basics
Classes are one of the two ways of creating [[Objects]] in C++, the other being [[Structs]]. They are functionally identical with the only difference being that the data members and functions of structs default to public while classes default to private meaning that by default third party code (such as main) cannot access said functions and data members. 
# Steps to Making and Using a Class
When using a class you must first define the class' data members and function/method prototypes. Then you write the function/method implementations. Finally you must instantiate/declare object variables and use them by calling their methods. Below is some code that showcases making and using a class:
~~~cpp
#incude <iostream>
using namespace std;
//Defining
class Deck {
	public:
	void shuffle();
	void cut(int where);
	int get_top_card();
	
	private:
	int cards[52];
	int top_index;
};
// member function implementation
void Deck::shuffle() {
	for (int i = 51; i > 0; i--) {
		int r = rand() % i;
		swap(cards[i], cards[r]);
	}
}
int Deck::get_top_card() {
	return cards[top_index++];
}

// Main application
int main(int argc, char* argv[]) {
	Deck d;
	int hand[5];
	d.shuffle();
	d.cut();
	for(int i = 0; i < 5; i++) {
		hand[i] = d.get_top_card();
	}
}
~~~
# Common Class Structure - Split Files
It's a common practice to separate classes into separate source code files so it can easily be reused by different applications. Typically a class would be split among 3 different files, the header file (.h), which defines the class along with its data members and prototypes for any of its functions, a corresponding .cpp file, which has the implementation of the member functions, and an application file (usually separate .cpp file) which instantiates and declares object variables and uses them. Here is an example of splitting a class across 3 separate files:
~~~cpp
//Header File (.h)
class Deck {
	public:
	void shuffle();
	void cut(int where);
	int get_top_card();
	private:
	int cards[52];
	int top_index;
}; // note the ; here
~~~

~~~cpp
//.cpp file for functions
#include <iostream
#include "deck.h"

//Code for each prototype method
~~~

~~~cpp
//Application File
#include <iostream>
#include "deck.h"

int main(int argc, char* argv[]) {
	Deck d;
	int hand[5];
	d.shuffle();
	d.cut();
	for (int =0; i < 5; i++) {
		hand[i] = d.get_top_card();
	}
}
~~~
# Access Specifiers
Each function or data member can be classified as public, private, or protected. These classifications support encapsulation by ensuring that no other programmer writes code that uses or modifies your object in an unintended way. They make private data/method members to be inaccessible to non-member functions of the class, forcing non-members to only utilize the PUBLIC interface. They are fairly self explanatory, private means it can only be called or access by members/functions that are part of that class, and public means any other code can call or access it. Protected will be explained more in a different section. By default everything is private, so you must use public: to make things visible. Generally you want to make the inteface public and the guts/inner workings private. Here is some example code:
~~~cpp
//Header File
class Deck {
	public:
	Deck(); //Constructor
	~Deck(); //Destructor
	void shuffle();
	void cut(int where);
	int get_top_card();
	private:
	int cards[52];
	int top_index;
};

~~~

~~~cpp
//.cpp file implementing methods
#include <iostream>
#include "deck.h"

//Code for each prototyped method
~~~

~~~cpp
//.cpp file using Deck
#include <iostream>
#include "deck.h"

int main(int argc, char* argv[]) {
	Deck d;
	int hand[5];
	
	d.shuffle();
	d.cut();
	
	d.cards[0] = ACE; //won't compile
	d.top_index = 5; //won't compile
}
~~~
# Constructors / Destructors
When an object comes alive, we need to have appropriate initial values in our data members so that future calls to member functions will work appropriately. Likewise, when an object dies (goes out of scope or is deleted) we may need to perform some cleanup operators. To help us with those tasks C++ provides Constructor (ctor) and Destructor (dtor) functions. 
## Constructor
A constructor (ctor for short) is a function of the same name as the class itself (e.g. Deck()). It is called automatically when the object is created (either when declared or when allocated view new), and it is used to initialize your object's data members to some desired or known initial state. It returns nothing.
## Destructor
A destructor (dtor for short) is a function of the same name as the class itself with a ~ in front (e.g. ~Deck()). This gets called automatically when object goes out of scope (i.e. when it is deallocated by "delete" or when scope completes), and it is used to free/delete any memory allocated by the object or close any open file streams, etc. It, like a constructor, returns nothing. It is not always needed though, more on this later.

Here is some code showcasing use of constructors and destructors:
~~~cpp
//deck.h
class Deck {
	public:
	Deck(); // Constructor
	~Deck(); // Destructor
	...
};
~~~

~~~cpp
//deck.cpp
#include <iostream>
#include "deck.h"

Deck::Deck() {
	top_index = 0;
	for (int i = 0; i < 52; i++) {
		cards[i] = i;
	}
}

Deck::~Deck() {
	//Not needed for this class
}
~~~

~~~cpp
//cardgame.cpp
#include "deck.h"

int main() {
	Deck d; // Deck() is called
	...
	
	return 0;
	//~Deck() is called
}
~~~
## Multiple Constructors
We can have multiple constructors with different arguments lists to provide options to client software for how they'd like to initialize the object. The constructor that has no arguments is known as the default constructor. Take a look at this code for an example:
~~~cpp
//student.h
class Student {
	public:
	Student(); // Default ctor
	Student(std::string name, int id, double gpa); // "Initializing" ctor
	~Student(); // Destructor
	std::string get_name();
	int get_id();
	double get_gpa();
	
	void set_name(std::string name);
	void set_id(int id);
	void set_gpa(double gpa);
	private:
	std::stirng name_;
	int id_; //Often name data members with special decorator (id_ or gpa_)
	double gpa_;// to make it obvious to other programmers that this variable
				// Is a data member
};
~~~

~~~cpp
//student.cpp
Student::Student() {
	name_ = "Jane Doe"; id_ = 0; gpa_ = 2.0;
}
Student::Student(string name, int id, double gpa) {
	name_ = name; id_ = id; gpa_ = gpa;
}
~~~

~~~cpp
#include <iostream>
#indluce "student.h"

int main() {
	Student s1; //calls default ctor
	string myname;
	cin >> myname;
	s1.set_name(myname);
	s1.set_id(214952);
	s1.set_gpa(3.67);
	Student s2(myname, 32421, 4.0); // calls "initializing" ctor
}
~~~
# Accessor / Mutator Methods
Generally it is good practice to define "get" (accessor) and "set" (mutator) functions to let other code access desired private data members. It is also good practice to use "const" after argument list for functions that DONT modify data members. This ensures data members are not altered by this function. 
~~~cpp
//student.h
class Student { 
	public: 
	Student(); // Constructor 1 
	Student(string name, int id, double gpa); // Constructor 2 
	~Student(); // Destructor 
	std::string get_name() const; 
	int get_id() const; 
	double get_gpa() const; 
	
	void set_name(string s); 
	void set_gpa(double g); 
	private: 
	std::string name_; 
	int id_; 
	double gpa_; 
};
~~~

~~~cpp
#include "student.h"
using namespace std;
std::string Student::get_name() const {
	return name_;
}
int Student::get_id() const {
	return id_;
}
void Student::set_name(string s) {
	name_ = s;
}
void Student::set_gpa(double g) {
	gpa_ = g;
}
~~~

~~~cpp
#include <iostream>
#include "student.h"
using namespace std;
int main() {
	Student s1;
	string myname;
	cin >> myname;
	s1.set_name (myname);
	string name_copy;
	name_copy = s1.get_name();
	...
}
~~~
# Member Functions
## Writing Member Functions
When writing member functions we need to let the compiler know that a function is a member of a class. This is done by including the name of the class followed by "::" just before the name of the function. This allows the compiler to check access to private/public variables. Without the class:: part the compiler would read the function as an outside piece of code and would bar it access to private variables.
## Calling Member Functions
When calling member functions outside the class scope (i.e. in main() or some outside function) you must precede the member function call with the object name of the specific object that it should operate on along with the dot operator (e.g. d1.shuffle()). The "objname." part of it indicates that the following function should be operating based on that specific objects data and not any other objects that belong to the same class. Here is some code showing this idea:
~~~cpp
#include <iostream>
#include "deck.h"

int main() {
	Deck d1, d2;
	int hand[5];
	
	d1.shuffle();
	//not Deck.shuffle() nor shuffle(d1), etc.
	
	for (int i =0; i < 5; i++) {
		hand[i] = d1.get_top_card();
	}
}
~~~
When calling member functions inside the class scope no preceding object is necessary. Within a member function we can just call other member functions directly, as shown here:
~~~cpp
//poker.cpp
#include <iostream>
#include "deck.h"

int main(int argc, char* argv[]) {
	Deck d1, d2;
	int hand[5];
	
	d1.shuffle();
	...
}
~~~

~~~cpp
deck.cpp
#include <cstdlib>
#include "deck.h"

void Deck::shuffle() {
	cut(); // calls cut() for this object, d1 is implicitly passed to shuffle()
	for (i = 0; i < 52; i++) {
		int r = rand() % (52-i);
		int temp = cards[r];
		cards[r] = cards[i];
		cards[i] = temp;
	}
}
void Deck::cut() { // Since shuffle was implicitly working on d1s data, d1 is again implicitly passed to cut()
	//swap 1st half of deck with 2nd
}
~~~
# Class pointers
We can declare pointers to these new class types. When doing so we use -> operator to access member functions or data, as shown here:
~~~cpp
#include <iostream>
#include "deck.h"

Deck* makeDeck() {
	Deck* d1 = new Deck; //Ctor called
	d1->shuffle();
	d1->cut();
	return d1;
}
int main() {
	int hand[5];
	Deck* myd = makeDeck();
	myd->shuffle();
	for (int i =0; i < 5; i++) {
		hand[i] = myd->get_top_card();
	}
	//More Ccode
	delete myd; // Dtor called
	return 0;
}
~~~