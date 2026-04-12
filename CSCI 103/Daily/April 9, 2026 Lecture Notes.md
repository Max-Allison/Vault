---
tags:
  - CSCI103
  - Daily
---
# Runtime Table

|            | SLL  | Vector                                       | SLL + tail | DLL  | DLL + tail | Circular Array                       |
| ---------- | ---- | -------------------------------------------- | ---------- | ---- | ---------- | ------------------------------------ |
| print()    | O(n) | O(n)                                         | O(n)       | O(n) | O(n)       | O(n)                                 |
| Push_back  | O(n) | O(n) (usually 1 but might need to copy over) | O(1)       | O(n) | O(1)       | O(n) (usually 1 but worst case is n) |
| Pop_back   | O(n) | O(1)                                         | O(n)       | O(n) | O(1)       | O(1)                                 |
| Push_Front | O(1) | O(n)                                         | O(1)       | O(1) | O(1)       | O(n) (usually 1 but worst case is n) |
| Pop_Front  | O(1) | O(n)                                         | O(1)       | O(1) | O(1)       | O(1)                                 |
| Put        | O(n) | O(n)                                         | O(n)       | O(n) | O(n)       | O(n)                                 |
| Get        | O(n) | O(1)                                         | O(n)       | O(n) | O(n)       | O(1)                                 |
# Practice Code 1
~~~cpp
void crunch(char* c, float f, vector<int>& v, int** i);
//How to call this function given the following variables?
char st[3];
vector<int> arr;
float* f;
int m[10];
//Answer
crunch(st, *f, arr, &m);
~~~
# Practice Code 2
~~~cpp
class Object {
	Object();
	Object(ai&)i
	Object& operator=(const obj c)
	~Obj();
}
~~~
# Practice Code 3
~~~cpp
Obj dupe(Obj o) {
	return o;
}
int main() {
	Obj a;
	Obj b;
	Obj c = a; //2
	b = c; //3
	Obj d = dupe(c); //2
}
~~~
# Practice Code 4 (inheritance)
~~~cpp
class Animal {
	virtual void make_noise() {
		cout << "";
	}
	virtual void eat() = 0;
};

class Dog : public Animal {
	void make_noise() {
		cout << "Woof";
	}
	void eat() {
		cout << "treats";
	}
};

class Newt : public Animal {
	void eat() {
		cout << "bugs";
	}
};

class Tree : public Animal {
	void make_noise() {
		cout << "trees don't make noise...";
	}
};


int main() {
	Animal a; //Does not compile as it is an abstract base class
	Animal * ap = new Animal[2]; //Works because it poitns at an animal but you didn't actually make one
	Dog d; //Cannot make objects with pure virtual functions, this works because dog implements the pure virtual functions from animal
	Newt n; //Compiles because make noise is just virtual not pure virtual so its chill
	Tree t; //Does not compile because no overwriting of the pure virtual eat
	n.make_noise();
	
	ap[0] = &d;
	ap[1] = &n;
	
	Newt * n1 = d; //not allowed, points can't go across the hierarchy
	
	ap[0]->make_noise(); //gives "woof"
	ap[1]->make_noise(); //gives ""
	
	//All of this only works with the derived classes having public animal
	
	return 0;
}

~~~
# Practice Code 5 (Fileio)
~~~cpp
/* 
width height
0, 0 1, 0 2, 0 ... width, 0
0,1
0,2
.
.
.
0,height ... width,height

2 3
0 1 28
223 17 5
Read all this in
*/
#include <string>
#include <fstream>
void read_image(string file_name) {
	ifstream f(file_name);
	
	if (f.fail()) {
		return;
	}
	
	int width;
	int height;
	
	f >> width;
	f >> height;
	
	int image[width][height]; //Doesn't work since you don't know how big width and height are when you compile
	
	width = stoi(ws);
	height = stoi(hs);
	
	int ** image = new int*[height];
	for (int i = 0; i < height; i++) {
		image[i] = new int[width];
		for (int j = 0; j < width; j++) {
			string i_s;
			f >> i_s;
			image[i][j] = stoi(i_s);
		}
	}
	
	delete [] image;
	
	f.close();
	return;
}

~~~


[[April 7, 2026 Lecture Notes|Previous Lecture]] | [[April 9, 2026 Lecture Notes|Next Lecture]]