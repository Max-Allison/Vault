---
tags:
  - FinalNote
  - CSCI103
---
# Basics
Objects are the center piece of [[Object Orientation]] and are used to represent high level concepts, actual objects, or just more nebulous things (beyond an integer, character, or double). These could include things like a pixel, a circle, a student, or a file. These "objects" can be represented as a collection of integers, character arrays/strings, etc. A pixel for example could have 3 values of R G and B while a circle may have center_x, center_y, and radius, or a student could be comprised of a name, ID, and major. In general objects allow us to aggregate different type variables together to represent a single larger 'thing' as well as supporting operations on that 'thing.' Objects can for example reference the collection with a single name (myCircle, student1) and can also access individual components (myCircle.radius, student1.id)

# Components
As previously mentioned objects are made up of both data members (data needed to model the object and track its state/operation) as well as methods/functions (code that operates on the object, modifies it, etc.). A good example for this is a deck of cards. The data members would be an array of 52 entries (one for each card) indicating their ordering with their indexes. Some functions of the deck of cards could be shuffle(), cut(), or get_top_card().

# C++ Objects
In C++ objects are made primarily through the use of [[Structs]] (which originate from C) and [[Classes]] (which is a C++ original). Structs are the predecessors of classes however, and so classes more so form the basis rather than structs. Both are fundamentally though just a way of grouping related data together with related operations to model some object

# Types and Instances
In C++ a type indicates how much memory will be required, what the bits mean (i.e. integer, double, pointer), and what operations can be performed. These types are things like int, which is 32-bits representing only integer values and supporting +, -, \*, /, =, \==, <, >, etc, and char*, which is 64-bits representing an address and supporting \* (dereference), &, +, - (but not multiply and divide). Types are effectively like blueprints for what and how to make a particular 'thing.' A 'variable' or 'object' is an actual instantiation (allocation of memory) for one of these types (ex: int x, double z, char *str, etc.)

# Declarations
To use objects in C++ they must first be defined as a struct or a class as mentioned earlier. This declaration is essentially a blueprint that indicates what any instance of the object should look like, and it should identify the overall name of the struct/class and its individual member types and names. It's also important to remember that declaring an object does not actually create a variable as no memory is allocated. Declarations will usually appear outside any function.

Once declared any number of instances can be created/instantiated in the code. These instances are actual objects (memory is allocated for each) created from the definition the declaration gives. These instances are declared like any other variables.

An example of the declaration and instantiating of a pixel struct is shown below:
~~~cpp
#include <iostream>

using namespace std;

//struct definition/declaration
struct pixel {
	unsigned char red;
	unsigned char green;
	unsigned char blue;
}; //note the semicolon here
//'pixel' is now a type
//just like 'int' is a type

int main(int argc, char *argv[]) {
	int i, j;
	//instantiations
	pixel p1;
	pixel image[256][256]
	//make p1 red
	p1.red = 255;
	p1.blue = p1.green = 0;
	//make a green image
	for (i = 0; i < 256; i++) {
		for (j = 0; j < 256; j++) {
			image[i][j].green = 255;
			image[i][j].blue = 0;
			image[i][j].red = 0;
		}
	}
	return 0;
}
~~~

# Membership Operator
Each variable (and function) in an object definition is called a member of the object. When declaring an instance/variable of an object, we give the entire object a name, but the individual members are identified with the member names provided earlier in the object definition. To access these members in an instance of the object we use the . (dot/membership) operator, so it would be instance_name.member)name. Here is an example in code below:
~~~cpp
#include <iostream>
using namespace std;

enum {CSCI = 1, CECS = 2};

struct student {
	char name[80];
	int id;
	int major;
};

int main(int argc, char *argv[]) {
	int i, j;
	//instantiations
	student my_student;
	
	my_student.id = 1682942;
	my_student.major = CSCI;
	...
	return 0;
}
~~~

# Memory View of  Objects
Each instantiation allocates memory for all the members/components of the object. For example this code:
~~~cpp
#include <iostream>

using namespace std;
//declaration (blueprint)
struct pixel {
	unsigned char red;
	unsigned char green;
	unsigned char blue;
};
int main (int argc, char *argv[]) {
	int i, j;
	//instantiations (object allocation)
	pixel p1;
	pixel image[256][256];
	...
	return 0;
}
~~~
Allocates this memory:

| Address | Memory Data | Variable | Object      |
| ------- | ----------- | -------- | ----------- |
| 0x7400  | 00          | red      | p1          |
| 0x7401  | FF          | green    | p1          |
| 0x7402  | 00          | blue     | p1          |
| 0x7403  | FF          | red      | image[0][0] |
| 0x7404  | 00          | green    | image[0][0] |
| 0x7405  | 00          | blue     | image[0][0] |
| 0x7406  | 48          | red      | image[0][1] |
| 0x7407  | C9          | green    | image[0][1] |
| 0x7408  | 17          | blue     | image[0][1] |
| ...     | ...         | ...      | ...         |
# Other Notes about Objects
Here are a couple of other important things to know about objects.
## Object Assignment
Assigning one object to another will perform a member-by-member copy of the entire source object to the destination object. Here is an example in code with a corresponding memory table:
~~~cpp
#include <iostream>
using namespace std;

enum {CSCI = 1, CECS = 2};

struct student {
	char name[80];
	int id;
	int major;
};

int main(int argc, char *argv[]) {
	student s1, s2;
	strncpy(s1.name, "Jill", 80);
	s1.id = 5;
	s1.major = CECS;
	s2 = s1; //This performs a member by member copy of s1 onto s2
	return 0;
}
~~~

| Address | Memory Data | Object   |
| ------- | ----------- | -------- |
| 7300    | J i l l     | s1.name  |
| 7304    | \0 ? ? ?    | s1.name  |
| ...     | ...         | s1.name  |
| 7376    | ? ? ? ?     | s1.name  |
| 7380    | 1682942     | s1.id    |
| 7384    | 2           | s1.major |
| 7388    | J i l l     | s2.name  |
| 7392    | \0 ? ? ?    | s2.name  |
| 7396    | ...         | s2.name  |
| 7400    | ? ? ? ?     | s2.name  |
| 7408    | 1682942     | s2.id    |
| 7412    | 2           | s2.major |
|         |             |          |
## Pointers & Objects
We can declare pointers to objects just as any other variable, and the address of a struct/class is just its starting address. Here is a code and memory table example:
~~~cpp
#include <iostream>
using namespace std;

enum {CSCI = 1, CECS = 2};

struct student {
	char name[80];
	int id;
	int major;
};

int main(int argc, char *argv[]) {
	student s1;
	student *stu_ptr;
	strncpy(s1.name, "Jill", 80);
	s1.id = 5; s1.major = CECS;
	stu_ptr = &s1; //gives stu_ptr s1's address
	return 0;
}
~~~

| Address    | Memory Data   | Object   |
| ---------- | ------------- | -------- |
| 7300 (&s1) | J i l l       | s1.name  |
| 7304       | \0 ? ? ?      | s1.name  |
| ...        | ...           | s1.name  |
| 7376       | ? ? ? ?       | s1.name  |
| 7380       | 5             | s1.id    |
| 7384       | 2             | s1.major |
| 7388       | 0 0 0 0       | stu_ptr  |
| 7392       | 7 3 0 0 (&s1) | stu_ptr  |
When accessing members from a pointer you can dereference the pointer first then use the dot operator, but remember that the dot operator has a higher precedence than * requiring the use of parentheses. Here is another code example:
~~~cpp
#include <iostream>
using namespace std;

enum {CSCI = 1, CECS = 2};

struct student {
	char name[80];
	int id;
	int major;
};

int main(int argc, char *argv[]) {
	student s1;
	student *stu_ptr;
	strncpy(s1.name, "Jill", 80);
	s1.id = 5; s1.major = CECS;
	stu_ptr = &s1; //gives stu_ptr s1's address
	*stu_ptr.id = 4; //This is incorrect, derefs id not the pointer
	(*stu_ptr).id = 4; //This is correct, derefs pointer then gets id
	strncpy((*str_ptr).name, "Tom", 80);
	return 0;
}
~~~
This looks a bit ugly though and you can save keystrokes and make your code look prettier by using the Arrow (->) operator. If you have a pointer pointing at an object (class or struct) then instead of using the dot operator you could write ptr_to_struct->member instead. Here is the final lines of the previous code block rewritten to show this:
~~~cpp
str_ptr->id = 4; //same as (*stu_ptr).id = 4;
strncpy(stu_ptr->name, "Tom", 80);
~~~
When it comes to actually using pointers to objects, you mainly want to use them when objects are either passed by reference or dynamically allocated. Below is some example code showing a situation where an object pointer comes in handy:
~~~cpp
#include <iostream>
using namespace std;

enum {CSCI = 1, CECS = 2};

struct student {
	char name[80];
	int id;
	int major;
};

student* makeStudent(const char* n, int i, int m) {
	student* stuptr = new student;
	
	strncpy(stuptr->name, n, 80);
	stuptr->id = i; stuptr->major = m;
	return stuptr;
}

int main(int argc, char *argv[]) {
	student* stuptr = makeStudent("Jane Doe", 5, CECS);
	...
	cout << stuptr->name << endl; //prints "Jane Doe"
	delete stuptr;
	return 0;
}
~~~
## Passing Objects as Arguments
In C, arguments must be a single value (i.e. can't pass an entire array of data, instead pass a pointer), but objects are the exception. You can actually pass an entire struct or class 'by value.' This will make a member-by-member copy of the object (as mentioned above) and pass it to the function. Of course, you can always pass a pointer (especially for big objects since pass by value means making a copy of large objects). Here is some example code showing objects being passed as arguments:
~~~cpp
#include <iostream>

using namespace std;
struct Point {
	int x;
	int y;
};

void print_point(Point myp) {
	cout << "(x,y)=" << myp.x << "," << myp.y;
	cout << endl;
}

int main(int argc, char* argv[]) {
	Point p1;
	p1.x = 2; p1.y = 5;
	print_point(p1);
	return 0;
}
~~~
## Returning Objects
Objects can be turned from a function, but they will return a copy of the struct/class indicated (return-by-value). Here is a code example of how to return an object:
~~~cpp
#include <iostream>
using namespace std;

struct Point {
	int x;
	int y;
};

void print_point(Point *myp) {
	cout << "(x,y)=" << myp->x << "," << myp->y;
	cout << endl;
}

Point make_point() {
	Point temp;
	temp.x = 3; temp.y = -1;
	return temp;
}

int main(int argc, char* argv[]) {
	Point p1;
	p1 = make_point();
	print_point(&p1); //prints (x,y)=3,-1
	return 0;
}
~~~
