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
