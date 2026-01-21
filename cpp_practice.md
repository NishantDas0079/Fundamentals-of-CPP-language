# Practice Codes for C++

```cpp
#include <iostream>
using namespace std;

int main()
{
	int *a; //declaring that a is a pointer to int
	int b;
	int c;
	
	cout << "enter number b:-" << endl;
	cin >> b;
	cout << "enter number c:-" << endl;
	cin >> c;
	
	a = &b; //referencing the value of b
	b = *a; // de referencing the value of c
	cout << a;
	cout << b;
	cout << c;
	return 0;
}
```

```cpp
#include <iostream>
using namespace std;

// Global variable
int a = 10;

void func1(int &b)   // pass by reference
{
    b = a;          // assign global variable to local variable
}

int main()
{
    int c = 20;     // local variable

    cout << "Before changing c: " << c << endl;

    func1(c);       // function modifies c

    cout << "After changing c: " << c << endl;
    cout << "Global variable a: " << a << endl;

    return 0;
}
```

```cpp
#include <iostream>
using namespace std;

int square(int a)
{
	return a*a;
}
int main()
{
	int a;
	cout << "enter a:-";
	cin >> a;
	square(a);
	cout << square(a) << endl;
	return 0;
}
```

```cpp
#include <iostream>
using namespace std;

int main()
{
	int a;
	int *ptr;
	cout << "enter a:-" << endl;
	cin >> a;
	ptr = &a;
	cout << "ptr:-" << ptr << endl;
	cout << "*ptr:-" << *ptr << endl;
	cout << :"value of a:-" << a << endl;
	return 0;
}
```

```cpp
#include <iostream>
using namespace std;

int main()
{
	int *b;
	int a;
	int c;
	
	cout << "enter a" << endl;
	cin >> a;
	b = &a;
	c = *b;
	cout << "value of b" << b << endl;
	cout << "value of c" << c << endl;
	return 0;
}
```

```cpp
#include <iostream>
using namespace std;

int main()
{
    int a;
    int b;
    int *ptr1;
    int *ptr2;
    int temp;
    cout << "a";
    cin >> a;
    cout << "b";
    cin >> b;
    ptr1 = &a;
    ptr2 = &b;
    temp = *ptr1;
    *ptr1 = *ptr2;
    *ptr2 = temp;
    cout << "after swapping a :" << a << endl;
    cout << "after changing b:-" << b << endl;
    return 0;
    
}
```
