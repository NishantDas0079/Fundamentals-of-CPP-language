```mermaid
flowchart TB
    A[🏗️ STRUCTURES OVERVIEW]:::main
    
    A --> B1["📐 1. BASICS<br/>struct Point {int x,y;};<br/>Point p={10,20};<br/>p.x → 8 bytes"]:::basics
    A --> B2["📦 2. ARRAYS<br/>Student s[3]={{1,A},{2,B}}<br/>sizeof(s)/sizeof(s[0])=3<br/>72 bytes total"]:::arrays
    A --> B3["🔗 3. POINTERS<br/>Node* p=malloc(sizeof)<br/>p→data=10<br/>Always free(p)"]:::pointers
    A --> B4["📂 4. NESTED<br/>struct Date {d,m,y};<br/>struct Emp {Date join;}<br/>emp.join.d access"]:::nested
    A --> B5["⚖️ 5. C vs C++<br/>Methods: No/Yes<br/>Constructor: No/Yes<br/>Padding: Both"]:::compare
    
    B1 --> X1["Memory: 8 bytes<br/>(4+4 int)"]
    B2 --> X2["Memory: 72 bytes<br/>(3×24 bytes)"]
    B3 --> X3["Dynamic Alloc<br/>16 bytes"]
    B4 --> X4["44 bytes total<br/>w/ padding"]
    B5 --> X5["Key Differences<br/>Table Summary"]
    
    classDef main fill:#2196f3,stroke:#1976d2,stroke-width:4px,color:#fff,font-weight:bold,font-size:16px
    classDef basics fill:#9c27b0,stroke:#7b1fa2,stroke-width:3px,color:#fff,font-size:14px
    classDef arrays fill:#4caf50,stroke:#388e3c,stroke-width:3px,color:#fff,font-size:14px
    classDef pointers fill:#ff9800,stroke:#f57c00,stroke-width:3px,color:#fff,font-size:14px
    classDef nested fill:#00bcd4,stroke:#0097a7,stroke-width:3px,color:#fff,font-size:14px
    classDef compare fill:#f44336,stroke:#d32f2f,stroke-width:3px,color:#fff,font-size:14px

```


# Basics
# 1. Simple Structure Declaration and Access (C/C++)

```cpp
#include <stdio.h>

struct Point {
    int x;
    int y;
};

int main() {
    struct Point p1 = {10, 20};
    printf("Point coordinates: (%d, %d)\n", p1.x, p1.y);
    return 0;
}
```

OUTPUT :-
```
Point coordinates: (10, 20)
```

LOGIC :-
```
struct Point defines a custom data type with two int members

p1 = {10, 20} uses designated initialization to set x=10, y=20

Dot operator . accesses structure members directly

Memory layout: 8 bytes total (4 bytes for x + 4 bytes for y)
```

# 2. Structure with Functions (C++)

```cpp
#include <iostream>
using namespace std;

struct Rectangle {
    int width, height;
    
    int area() {
        return width * height;
    }
};

int main() {
    Rectangle r = {5, 10};
    cout << "Area: " << r.area() << endl;
    return 0;
}
```

OUTPUT :-
```
Area: 50
```

LOGIC :-
```
C++ allows member functions inside struct (unlike C)

area() function has direct access to width and height

Called as r.area() - function belongs to the structure instance

Inline function for better performance on simple calculations
```

# 3. Array of Structures (C/C++)

```cpp
#include <stdio.h>

struct Student {
    int roll_no;
    char name[20];
};

int main() {
    struct Student class[3] = {
        {101, "Alice"},
        {102, "Bob"},
        {103, "Charlie"}
    };
    
    for(int i = 0; i < 3; i++) {
        printf("Roll: %d, Name: %s\n", class[i].roll_no, class[i].name);
    }
    return 0;
}
```

OUTPUT :-
```
Roll: 101, Name: Alice
Roll: 102, Name: Bob
Roll: 103, Name: Charlie
```

LOGIC :-
```
Array of structures: each element is a complete Student (24 bytes each)

Aggregate initialization fills array in declaration order

class[i].roll_no accesses member of ith structure

Total memory: 72 bytes (3 × 24 bytes)
```

# Intermediate Level
# 1. Nested Structures (C/C++)

```cpp
#include <stdio.h>

struct Date {
    int day, month, year;
};

struct Employee {
    int id;
    char name[30];
    struct Date joining_date;  // Nested structure
};

int main() {
    struct Employee emp = {1001, "John Doe", {15, 6, 2025}};
    printf("Employee: %s, Joined: %d/%d/%d\n", 
           emp.name, emp.joining_date.day, 
           emp.joining_date.month, emp.joining_date.year);
    return 0;
}
```

OUTPUT :-
```
Employee: John Doe, Joined: 15/6/2025
```

LOGIC :-
```
joining_date is a nested structure (12 bytes inside 44-byte Employee)

Access nested members: emp.joining_date.day

Initializer nesting: {15, 6, 2025} fills Date structure fields sequentially

Memory layout: Employee = id(4) + name(30) + Date(12) = 46 bytes (with padding)
```

# 2. Structure Pointers (C)

```cpp
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

int main() {
    struct Node* head = malloc(sizeof(struct Node));
    head->data = 42;
    head->next = NULL;
    
    printf("Node data: %d\n", head->data);
    free(head);
    return 0;
}
```

OUTPUT :-
```
Node data: 42
```

LOGIC :-

```
malloc(sizeof(struct Node)) allocates 8 bytes dynamically

-> operator dereferences pointer to access members: (*head).data

head->next = NULL marks end of linked list

Always free() allocated memory to prevent leaks
```

# 3. Self-Referential Structures (C++)

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    
    void display() {
        cout << "Data: " << data << endl;
    }
};

int main() {
    Node n1;
    n1.data = 100;
    n1.next = nullptr;
    n1.display();
    return 0;
}
```

OUTPUT :-
```
Data: 100
```

LOGIC :-

```
Node* next creates self-referential structure for linked lists

Forward declaration implicit in C++ (unlike C requiring pointer typedef)

nullptr is modern C++ null pointer (safer than NULL)

Member function display() shows C++ struct capabilities
```



```mermaid

flowchart TD
    A[Structures in C/C++] --> B[Basics]
    A --> C[Intermediate]
    
    B --> B1[Simple Declaration<br/>. operator<br/>Output: 10,20]
    B --> B2[C++ Member Functions<br/>Inline area calc<br/>Output: Area 50]
    B --> B3[Array of Structures<br/>3 Students<br/>Output: Roll+Name]
    
    C --> C1[Nested Structures<br/>Employee+Date<br/>Output: 15/6/2025]
    C --> C2[Structure Pointers<br/>malloc+free<br/>Output: Node 42]
    C --> C3[Self-Referential<br/>Linked List Node<br/>Output: Data 100]
    
    B1 --> D[Memory 8 bytes]
    B2 --> D
    B3 --> E[Memory 72 bytes<br/>3x24 bytes]
    
    C1 --> F[Memory 44 bytes<br/>w padding]
    C2 --> G[Dynamic 16 bytes]
    C3 --> H[Self-reference<br/>Node* next]
    
    D --> I[C vs C++ Table]
    E --> I
    F --> I
    G --> I
    H --> I
    
    I --> J[Methods: C=No C++=Yes<br/>Constructors: No/Yes<br/>Pointers: . / ->]
    
    classDef main fill:#e1f5fe,stroke:#01579b
    classDef basics fill:#f3e5f5,stroke:#4a148c
    classDef inter fill:#e8f5e8,stroke:#1b5e20
    classDef ex fill:#fff3e0,stroke:#e65100
    classDef mem fill:#e0f2f1,stroke:#00695c
    
    class A main
    class B,C basics
    class B1,B2,B3,C1,C2,C3 ex
    class D,E,F,G,H mem
    class I,J main

```



```
| Feature           | C Structures       | C++ Structures |
| ----------------- | ------------------ | -------------- |
| Methods           | ❌ Not allowed      | ✅ Allowed      |
| Constructors      | ❌ Manual init      | ✅ Automatic    |
| Pointer syntax    | (*ptr).member      | ptr->member    |
| Memory management | Manual malloc/free | RAII preferred |
```
