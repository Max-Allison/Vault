---
tags:
  - CSCI103
  - FinalNote
---
# Basics
In C, strings are character arrays (such as char mystring\[80];) which are terminated with a NULL character '\0'. They are passed by reference/pointer (char*) to functions and require some care when making copies. They are processed using the \<cstring> library. 
# Functions
The following is a of cstring functions that are included with the library.
- Int strlen(char* dest);
	- Which returns the length of the string
- Int strcmp(char* str1, char* str2);
	- Compares two strings together based on alphanumerics
	- Return 0 if equal, >0 if first non-equal char in str1 is alphanumerically larger, <0 otherwise
- char \*strcpy(char \*dest, char \*src);
	- Copies src to dest
	- strncpy(char \*dest, char \*src, int n); 
	- Maximum of n characters copied
- char \*strchr (char* str, char c );
	- Finds first occurrence of character ‘c’ in str returning a pointer to that character or NULL if the character is not found
# Shallow Vs. Deep Copy
When copying c strings you cannot just use the basic assignment operator, you need to allocate new storage. Here is a code example of how to do this:
~~~cpp
#include <iostream>
#include <cstring>
using namespace std;

int main() {
	//store 10 user names
	// names type is still char **
	char* names[10];
	
	char temp_buf[40];
	for (int i=0; i < 10; i++) {
		cin >> temp_buf;
		//Find length of strings
		int len = strlen(temp_buf);
		names[i] = new char[len+1];
		strcpy(names[i], temp_buf);
	}
	// Do stuff with names
	
	for (int i=0; i < 10; i++) {
		delete [] names[i];
	}
	
	return 0;
}
~~~
