# Creating a Structure Student with the folllowing parameters : roll number, name and marks. 

```cpp
#include <iostream>
#include <string>
using namespace std;

struct Student {
    int roll;
    string name;
    float marks;
};

int main() {
    Student s[5];

    // Input details
    for (int i = 0; i < 5; i++) {
        cout << "\nEnter details of student " << i + 1 << endl;
        cout << "Roll Number: ";
        cin >> s[i].roll;

        cout << "Name: ";
        cin >> s[i].name;

        cout << "Marks: ";
        cin >> s[i].marks;
    }

    // Display students with marks > 75
    cout << "\nStudents who scored more than 75 marks:\n";
    for (int i = 0; i < 5; i++) {
        if (s[i].marks > 75) {
            cout << "\nRoll Number: " << s[i].roll;
            cout << "\nName: " << s[i].name;
            cout << "\nMarks: " << s[i].marks << endl;
        }
    }

    return 0;
}
```

INPUT :-

```
Enter details of student 1
Roll Number: 1
Name: Aman
Marks: 82

Enter details of student 2
Roll Number: 2
Name: Riya
Marks: 68

Enter details of student 3
Roll Number: 3
Name: Karan
Marks: 90

Enter details of student 4
Roll Number: 4
Name: Neha
Marks: 74

Enter details of student 5
Roll Number: 5
Name: Rohit
Marks: 78
```

OUTPUT :-

```
Students who scored more than 75 marks:

Roll Number: 1
Name: Aman
Marks: 82

Roll Number: 3
Name: Karan
Marks: 90

Roll Number: 5
Name: Rohit
Marks: 78
```



# Defining a Structure Employee containing : employee ID, name, basic salary.

```cpp
#include <iostream>
#include <string>
using namespace std;

struct Employee {
    int emp_id;
    string name;
    float basic_salary;
};

int main() {
    Employee e;
    float hra, da, gross_salary;

    // Input employee details
    cout << "Enter Employee ID: ";
    cin >> e.emp_id;

    cout << "Enter Employee Name: ";
    cin >> e.name;

    cout << "Enter Basic Salary: ";
    cin >> e.basic_salary;

    // Calculate HRA and DA
    hra = 0.20 * e.basic_salary;   // 20% of basic salary
    da  = 0.10 * e.basic_salary;   // 10% of basic salary

    // Calculate Gross Salary
    gross_salary = e.basic_salary + hra + da;

    // Display details
    cout << "\nEmployee Details";
    cout << "\nEmployee ID: " << e.emp_id;
    cout << "\nName: " << e.name;
    cout << "\nBasic Salary: " << e.basic_salary;
    cout << "\nHRA (20%): " << hra;
    cout << "\nDA (10%): " << da;
    cout << "\nGross Salary: " << gross_salary;

    return 0;
}
```

INPUT :-

```
Enter Employee ID: 101
Enter Employee Name: Ravi
Enter Basic Salary: 20000
```

OUTPUT :-

```
Employee Details
Employee ID: 101
Name: Ravi
Basic Salary: 20000
HRA (20%): 4000
DA (10%): 2000
Gross Salary: 26000
```


# Array Output Questions

```cpp
#include <iostream>
using namespace std;

int main()
{
	int arr[] = {10, 20, 30, 40};
    int* p = arr;

    cout << *p << endl;
    cout << *(p + 1) << endl
	cout << *(p + 3) << endl;
    return 0;
}
```

OUTPUT :-
```
10
20
40
```

Explanation ;-
```
The array name arr represents the base address of the array.

Pointer p now points to the first element of the array (arr[0]).

*p dereferences the pointer.

It gives the value at arr[0], which is 10.

p + 1 moves the pointer to the next integer location.

This points to arr[1].

Value printed is 20.

p + 2 points to arr[2].

Value printed is 30
```


```cpp
#include <iostream>
using namespace std;

int main()
{
   int arr[] = {5, 10, 15, 20};
   int* p = arr + 2;

   cout << *p << endl;
   cout << *(p - 1) << endl;
   return 0;
}
```


OUTPUT :-
```
15
10
```

Explanantion :-
```
Array elements with index:

arr[0] = 5

arr[1] = 10

arr[2] = 15

arr[3] = 20

arr points to arr[0]

arr + 2 points to arr[2]

So pointer p points to the value 15

p - 1 moves the pointer one position backward

Now it points to arr[1]

Value at arr[1] is 10

Second output line → 10

Key Concepts Used

Pointer arithmetic

arr + 2 → points to 3rd element

p - 1 → moves pointer backward

Dereferencing (*) gives the value stored at the address

If you want to try trickier pointer outputs, pre/post increment, or array–pointer confusion questions, send the next one 👌
```


```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {1, 2, 3};
    int* p = arr;

    for (int i = 0; i < 3; i++) {
        cout << *(p++) << " ";
    }

    return 0;
}
```

OUTPUT :-
```
1 2 3
```

Explanantion :-
```
p++ is post-increment, so:

First: dereference p

Then: increment p to point to the next element

So each iteration:

Print the value p points to

Move p forward by one int

| Iteration | `p` points to | Printed | `p` moves to |
| --------- | ------------- | ------- | ------------ |
| 1         | `arr[0]`      | `1`     | `arr[1]`     |
| 2         | `arr[1]`      | `2`     | `arr[2]`     |
| 3         | `arr[2]`      | `3`     | past array   |
```


```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {3, 6, 9, 12};
    int* p = arr;

    while (p <= &arr[3]) {
        cout << *p << " ";
        p++;
    }

    return 0;
}
```

OUTPUT :-
```
3 6 9 12 
```


Explanantion ;


# Structures Output Questions

```cpp
#include <iostream>
using namespace std;

int main()
{
    struct Data {
        int x;
        int y;
    };

    Data arr[] = {{1,2}, {3,4}, {5,6}};
    Data* p = arr;

    cout << p->x << endl;
    cout << (p + 1)->y << endl;

    return 0;
}
```


OUTPUT :-
```
1
4
```

Explanation :-
```
arr[0] = {1, 2}
arr[1] = {3, 4}
arr[2] = {5, 6}

cout << p->x << endl;

p->x means arr[0].x

Value: 1

(p + 1) points to arr[1]

arr[1].y is 4
```


```cpp
#include <iostream>
using namespace std;

int main()
{
    struct Item {
        int price;
    };

    Item arr[] = {{1}, {3}, {5}};
    Item* p = arr;

    cout << p[2].price << endl;       // arr[2].price
    cout << (*(p + 1)).price << endl; // arr[1].price

    return 0;
}
```


OUTPUT :-
```
5
3
```


Explanation :-
```
| Expression         | Value |
| ------------------ | ----- |
| `p[2].price`       | 5     |
| `(*(p + 1)).price` | 3     |
```
