---
tags:
  - FinalNote
  - CSCI103
---
Enumeration is a technique in C++ that associates a number (integer) with a symbolic name, pictured below:
~~~cpp
enum [optional_collection_name] {Item1, Item2, ... ItemN}
//Item1=0
//Item2=1
//...
//ItemN=N-1
~~~
By using these symbolic names in code, the compiler will be able to replace those symbolic names with the numbers they correspond too. This can provide an easy way to categorize more nebulous values as specific values without having to remember what they are.
### Example Code
~~~cpp
//Example 1
const int BLACK=0;
const int BROWN=1;
const int RED=2;

const int WHITE=7;

int pixela=RED;
int pixelb=BROWN;
...
//Example 2
//First enum item is associated with 0
enum Colors {Black, Brown, Red, ..., WHITE};

int pixela = RED; // pixela = 2;
int pixelb = BROWN; // pixelb = 1;
//Example 3
enum {CSCI, CSBA, CECS, CSGM, AMCM, QBIO};
int major = AMCM; //major = 4;
int minor = CSCI; //minor = 0;
~~~