# Practice Codes for C++

# Q1. Referencing and Dereferencing
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

# Q2. Scoping of a variable
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

# Q3. Writing a square(int) function
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

# Q4. Printing Value and address of the variable and value stored in pointer
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

# Q5. Program where a pointer stores the address of another variable and copies its value in third variable
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

# Q6. Swapping two numbers using pointers
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

# Q7. Simple dynamic integer variable using new and delete
```cpp
#include <iostream>
using namespace std;

int main()
{
	int a;
	int *ptr;
	cout << "enter number:" << " " ;
	cin >> a;
	ptr = new int(a);
	(*ptr)++;
	cout << "what is a now?" << ptr << endl;
	cout << *ptr << endl;
	delete ptr;	
	return 0;
	
}
```

# Output Questions

```cpp
int x = 5;
int *p = &x;
*p = 10;
cout << x;
```

OUTPUT 
```
10
```

LOGIC
```
Step by step

int x = 5;
→ x starts as 5

int *p = &x;
→ p stores the address of x

*p = 10;
→ You change the value at that address
→ That value is x

cout << x;
→ Prints the updated value
```

```cpp
int a = 1, b = 2;
int *p = &a;

p = &b;   // now p points to b
*p = 5;   // change b

cout << a << " " << b;
```

OUTPUT
```
1 5
```

LOGIC
```
Step by step

a = 1, b = 2

p = &a → p points to a

p = &b → p now points to b

*p = 5 → modifies b, not a
```

```cpp
int x = 10;
int *p = &x;

cout << (*p)++ << "";
cout << *p << "";
cout << ++*p << "";
```

OUTPUT
```
cout << (*p)++ << " ";  // 10, x becomes 11
cout << *p << " ";     // 11
cout << ++(*p) << " "; // 12
```

```cpp
int a[] = {10, 20, 30, 40, 50};
int *p = a + 1;
cout << *(p + 2) << "" << "\n";
```

OUTPUT
```
20 30
```

LOGIC
```
Index:   0   1   2   3   4
Value:  10  20  30  40  50
Address: &a[0] &a[1] &a[2] &a[3] &a[4]

int *p = a + 1;

a decays to &a[0]

a + 1 → &a[1]

So p points to 20

*(p + 2)

p + 2 → &a[3]

*(p + 2) → value at index 3 → 40
```


