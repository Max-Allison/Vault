---
tags:
  - CSCI103
  - FinalNote
---
# Basics
Strings are one of the [[Classes]] that the C++ library provides. They are one of the most basic and useful classes in C++, and are effectively an evolved form of [[C-Strings]]. They [[Abstraction|abstract]] all the annoying details and [[Encapsulation|encapsulate]] the code to actually handle:
- Memory allocation and sizing
- Deep copy
- Concatenation, comparison, size information
- etc.
In C++, the string class provides an easier alternative to working with plain-old character arrays. Some Do's and Don'ts of them are:
- DO \#include \<string> and put using namespace std;
- DO initialize using = or by giving an initial value in parentheses (aka use the "constructor" syntax)
- DO still use it like an array by using \[index] to get individual characters
- DO still use cin/cout with strings
- DONT need to declare the size (i.e. \[7] just assign)
- DONT worrry about how many characters the user types when inputting to a c++ string
Here is some example code showcasing strings:
~~~cpp
#include <iostream>
#include <string>
using namespaces std;

int main() {
	char str1[7] = "CS 103";
	/* Initializes the array to "CS 103" */
	string str2 = "CS 103";
	string str3("Hello");
	/* Initializes str2 to "CS 103" & str3 to "Hello" */
	str2[5] = '4'; // now str2 = "CS 104"
	
	cout << str2 << endl;
	// prints "CS 104"
	
	cin >> str1; // If the user types more than 6 chars.. uh oh!
	cin >> str2; // str2 will ajust to hold whatever the user types
}
~~~
Behind the scenes strings are really just creating and manipulating character arrays, but they give you a simplified set of operators and functions. They abstract character arrays and makes something like concatenation (appending) for example, to be as easy as just writing a + like shown here:
~~~cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
	string str2 = "CS 103";
	// str2 storse 6 chars. = "CS 103"
	
	str2 = "Computer Science";
	// now str2 stores 16 characters
	
	//Can append using "+" or "+=" operator
	str2 = str2 + " is cool";
	//now str2 stores 24 characters
}
~~~
# String Comparison
C++ strings will perform lexicographic (alphabetical) comparison when comparison operators (<, >, \==, etc.) are applied. Remember that these comparison operators do not work with plain old character arrays. Here is some code for an example:
~~~cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
	char str1[4] = "abc";
	string str2 = "abc";
	
	if (str1 == "abc") // doesn't work
	 {...}
	if (str2 == "abc") // works...true
	 {...}
	if (str1 < "aac") // doesn't work
	 {...}
	if (str2 < "aac") // works...false
	 {...}
	
	string str3 = "acb";
	if (str3 > str2) //works...true
	 {...}
}
~~~
# Calling Member Functions (Methods)
As strings are [[Objects]] you use the dot operator to call an operation (function) on them or to access a data value. The string class has a number of different functions but two useful ones are asking for the string size and generating substrings. Asking for the string size can be done with .size() and returns the number of characters store in the string. Generating substrings is done with either .substr(start_index) or .substr(start_index, length) which returns a substring starting from that index and either going until n or just the end of the string. They are both showcased in code below:
~~~cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
	string mystr = "CS 103";
	cout << mystr.size() << endl; // 6
	
	string s = mystr.substr(2); // s = "103"
	
	mystr = "Computer Science";
	cout << mystr.size() << endl; // 16
	
	s = mystr.substr(9,2); // s = "Sc"
}
~~~
# String <--> Number Conversion
Recall that casting does NOT work for string <--> numeric conversions. Instead, use functions defined in \<string>. Conversion from number to string can be done with functions like string to_string(int); string to_string(double); etc. Conversion from string to number can be done with int stoi(string); unsigned int stoul(string); and double stod(string); These are showcased below:
~~~cpp
#include <iostream> 
#include <string>
using namespace std;
int main() {
	double a = 3.6;
	int b = static_cast<int>(a) / 2; // Works! b = 1 (casts 3.6 to 3)
	
	int c = 123;
	string d = static_cast<string>(c); // Error! Doesn't Compile
	string d = to_string(c); // Works! But only since C++11
	
	string e = "42";
	int f = static_cast<int>(e); // Error Doesn't compile
	int f = stoi(e); // string-to-int, Works! but only since C++11
	//use stod() for string-to-double
	return 0;
}
~~~
