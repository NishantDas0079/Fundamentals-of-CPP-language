# 1. Basic Structure & Syntax
# Hello World Program

```
#include <iostream>
using namespace std;

int main() {
    cout << "Hello World!" << endl;
    return 0;
}
```

# Program 1: Simple Input/Output
```
#include <iostream>
using namespace std;

int main() {
    string name;
    int age;
    
    cout << "Enter your name: ";
    cin >> name;
    
    cout << "Enter your age: ";
    cin >> age;
    
    cout << "Hello " << name << "! You are " << age << " years old." << endl;
    
    return 0;
}
```

# 2. Variables & Data Types

```
#include <iostream>
using namespace std;

int main() {
    // Basic data types
    int number = 10;           // Whole numbers
    float decimal = 3.14f;     // Decimal numbers (small)
    double price = 99.99;      // Decimal numbers (large)
    char letter = 'A';         // Single character
    bool answer = true;        // true or false
    
    cout << "Number: " << number << endl;
    cout << "Decimal: " << decimal << endl;
    cout << "Letter: " << letter << endl;
    cout << "Answer: " << answer << endl;
    
    return 0;
}
```

# Program 2: Simple Calculator
```
#include <iostream>
using namespace std;

int main() {
    float num1, num2;
    
    cout << "Enter first number: ";
    cin >> num1;
    
    cout << "Enter second number: ";
    cin >> num2;
    
    cout << "Addition: " << num1 + num2 << endl;
    cout << "Subtraction: " << num1 - num2 << endl;
    cout << "Multiplication: " << num1 * num2 << endl;
    
    if(num2 != 0) {
        cout << "Division: " << num1 / num2 << endl;
    } else {
        cout << "Cannot divide by zero!" << endl;
    }
    
    return 0;
}
```

# 3. Conditional Statements

```
#include <iostream>
using namespace std;

int main() {
    int marks;
    
    cout << "Enter your marks: ";
    cin >> marks;
    
    if(marks >= 90) {
        cout << "Grade A" << endl;
    }
    else if(marks >= 70) {
        cout << "Grade B" << endl;
    }
    else if(marks >= 50) {
        cout << "Grade C" << endl;
    }
    else {
        cout << "Grade F" << endl;
    }
    
    return 0;
}
```

# Program 3: Even or Odd Checker
```
#include <iostream>
using namespace std;

int main() {
    int number;
    
    cout << "Enter a number: ";
    cin >> number;
    
    if(number % 2 == 0) {
        cout << number << " is Even" << endl;
    } else {
        cout << number << " is Odd" << endl;
    }
    
    return 0;
}
```

# 4. Loops

```
#include <iostream>
using namespace std;

int main() {
    // For loop
    cout << "Counting 1 to 5: ";
    for(int i = 1; i <= 5; i++) {
        cout << i << " ";
    }
    cout << endl;
    
    // While loop
    int count = 1;
    cout << "Counting 1 to 3: ";
    while(count <= 3) {
        cout << count << " ";
        count++;
    }
    cout << endl;
    
    return 0;
}
```

# Program 4: Multiplication Table
```
#include <iostream>
using namespace std;

int main() {
    int num;
    
    cout << "Enter a number for multiplication table: ";
    cin >> num;
    
    for(int i = 1; i <= 10; i++) {
        cout << num << " x " << i << " = " << num * i << endl;
    }
    
    return 0;
}
```

# 5. Pointers

```
#include <iostream>
using namespace std;

int main() {
    int num = 10;
    int *ptr;  // Pointer declaration
    
    ptr = &num;  // Store address of num
    
    cout << "Value of num: " << num << endl;
    cout << "Address of num: " << &num << endl;
    cout << "Value of ptr: " << ptr << endl;
    cout << "Value at ptr: " << *ptr << endl;  // Dereferencing
    
    // Change value using pointer
    *ptr = 20;
    cout << "New value of num: " << num << endl;
    
    return 0;
}
```

# Reference Variables

```
#include <iostream>
using namespace std;

int main() {
    int num = 10;
    int &ref = num;  // Reference variable
    
    cout << "num: " << num << endl;
    cout << "ref: " << ref << endl;
    
    ref = 20;  // Change through reference
    
    cout << "After change:" << endl;
    cout << "num: " << num << endl;
    cout << "ref: " << ref << endl;
    
    return 0;
}
```

# 6. new and delete Operators

```
#include <iostream>
using namespace std;

int main() {
    // Single variable
    int *p = new int;  // Allocate memory
    *p = 25;           // Store value
    
    cout << "Value: " << *p << endl;
    
    delete p;  // Free memory
    
    // Array
    int *arr = new int[3];  // Allocate array
    
    arr[0] = 10;
    arr[1] = 20;
    arr[2] = 30;
    
    cout << "Array elements: ";
    for(int i = 0; i < 3; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
    
    delete[] arr;  // Free array memory
    
    return 0;
}
```

# Program 5: Dynamic Array
```
#include <iostream>
using namespace std;

int main() {
    int size;
    
    cout << "How many numbers? ";
    cin >> size;
    
    int *numbers = new int[size];  // Create dynamic array
    
    cout << "Enter " << size << " numbers:" << endl;
    for(int i = 0; i < size; i++) {
        cin >> numbers[i];
    }
    
    cout << "You entered: ";
    for(int i = 0; i < size; i++) {
        cout << numbers[i] << " ";
    }
    cout << endl;
    
    delete[] numbers;  // Clean up
    
    return 0;
}
```

# 7. Classes and Objects (Encapsulation)

```
#include <iostream>
using namespace std;

class Student {
private:  // Hidden data
    string name;
    int roll;
    
public:  // Public functions to access data
    void setData(string n, int r) {
        name = n;
        roll = r;
    }
    
    void display() {
        cout << "Name: " << name << endl;
        cout << "Roll: " << roll << endl;
    }
};

int main() {
    Student s1;
    s1.setData("John", 101);
    s1.display();
    
    return 0;
}
```

# 8. Friend Function
```
#include <iostream>
using namespace std;

class Box {
private:
    int length;
    
public:
    Box(int l) {
        length = l;
    }
    
    friend void showLength(Box b);  // Friend function
};

// Friend function can access private members
void showLength(Box b) {
    cout << "Box length: " << b.length << endl;
}

int main() {
    Box myBox(10);
    showLength(myBox);
    
    return 0;
}
```

# 9. Inheritance

```
#include <iostream>
using namespace std;

// Base class
class Animal {
public:
    void eat() {
        cout << "I can eat!" << endl;
    }
};

// Derived class
class Dog : public Animal {
public:
    void bark() {
        cout << "I can bark! Woof woof!" << endl;
    }
};

int main() {
    Dog myDog;
    
    myDog.eat();   // From Animal class
    myDog.bark();  // From Dog class
    
    return 0;
}
```

# 10. Polymorphism

```
#include <iostream>
using namespace std;

class Animal {
public:
    virtual void sound() {  // Virtual function
        cout << "Animal makes a sound" << endl;
    }
};

class Dog : public Animal {
public:
    void sound() override {  // Override
        cout << "Dog barks" << endl;
    }
};

class Cat : public Animal {
public:
    void sound() override {
        cout << "Cat meows" << endl;
    }
};

int main() {
    Animal* animal1 = new Dog();
    Animal* animal2 = new Cat();
    
    animal1->sound();  // Calls Dog's sound
    animal2->sound();  // Calls Cat's sound
    
    delete animal1;
    delete animal2;
    
    return 0;
}
```

# 11. Abstraction

```
#include <iostream>
using namespace std;

// Abstract class
class Shape {
public:
    virtual void draw() = 0;  // Pure virtual function
};

class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing Circle" << endl;
    }
};

class Square : public Shape {
public:
    void draw() override {
        cout << "Drawing Square" << endl;
    }
};

int main() {
    Shape* shape1 = new Circle();
    Shape* shape2 = new Square();
    
    shape1->draw();
    shape2->draw();
    
    delete shape1;
    delete shape2;
    
    return 0;
}
```

# 12. File Handling

```
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    // Writing to file
    ofstream myFile("example.txt");
    
    if(myFile.is_open()) {
        myFile << "Hello from C++!" << endl;
        myFile << "This is line 2" << endl;
        myFile.close();
        cout << "File written successfully!" << endl;
    }
    
    // Reading from file
    string line;
    ifstream readFile("example.txt");
    
    cout << "\nReading file:" << endl;
    if(readFile.is_open()) {
        while(getline(readFile, line)) {
            cout << line << endl;
        }
        readFile.close();
    }
    
    return 0;
}
```

# Program 8: Simple File Reader
```
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    string filename;
    
    cout << "Enter filename to read: ";
    cin >> filename;
    
    ifstream file(filename);
    
    if(file.is_open()) {
        string line;
        cout << "\nFile contents:" << endl;
        while(getline(file, line)) {
            cout << line << endl;
        }
        file.close();
    } else {
        cout << "Cannot open file!" << endl;
    }
    
    return 0;
}
```

# 13. Exception Handling

```
#include <iostream>
using namespace std;

int main() {
    int num1, num2;
    
    cout << "Enter two numbers: ";
    cin >> num1 >> num2;
    
    try {
        if(num2 == 0) {
            throw "Cannot divide by zero!";  // Throw exception
        }
        
        int result = num1 / num2;
        cout << "Result: " << result << endl;
    }
    catch(const char* error) {  // Catch exception
        cout << "Error: " << error << endl;
    }
    
    cout << "Program continues..." << endl;
    
    return 0;
}
```

# Program 9: Simple Age Checker with Exception
```
#include <iostream>
using namespace std;

int main() {
    int age;
    
    cout << "Enter your age: ";
    cin >> age;
    
    try {
        if(age < 0) {
            throw "Age cannot be negative!";
        }
        if(age > 150) {
            throw "Age seems unrealistic!";
        }
        
        cout << "Your age is: " << age << endl;
    }
    catch(const char* message) {
        cout << "Invalid age: " << message << endl;
    }
    
    return 0;
}
```

# Quick Reference Summary
# 1. Pointers & References

```
int num = 10;
int *ptr = &num;    // Pointer stores address
int &ref = num;     // Reference is alias

cout << *ptr;       // Dereference pointer
cout << ref;        // Use reference
```

# 2. Memory Operators
```
// Allocate single variable
int *p = new int;   
*p = 100;
delete p;

// Allocate array
int *arr = new int[5];
delete[] arr;
```


# 3. OOP Concepts

Encapsulation: Hide data, show functions

Inheritance: Reuse parent class features

Polymorphism: Same function, different behavior

Abstraction: Show only essential features


# 4. Key Differences

Pointer: Can be NULL, can change, uses *

Reference: Must be initialized, cannot change, uses &

new: Allocates heap memory

delete: Frees heap memory

# 5. Simple Rules

Use . for objects: obj.function()

Use -> for pointers: ptr->function()

Always delete what you new

Catch exceptions with try-catch

Use virtual functions for polymorphism
