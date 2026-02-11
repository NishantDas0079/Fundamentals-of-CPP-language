# Implementing a singly linked list, using new and delete for nodes and performing certain operations.

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
};

class LinkedList {
private:
    Node* head;

public:
    LinkedList() {
        head = nullptr;
    }

    ~LinkedList() {
        Node* current = head;
        while (current != nullptr) {
            Node* next = current->next;
            delete current;
            current = next;
        }
    }

    // 1) Insertion at the beginning
    void insertAtBeginning(int val) {
        Node* newNode = new Node();
        newNode->data = val;
        newNode->next = head;
        head = newNode;
    }

    // 2) Insertion at the end
    void insertAtEnd(int val) {
        Node* newNode = new Node();
        newNode->data = val;
        newNode->next = nullptr;

        if (head == nullptr) {
            head = newNode;
            return;
        }

        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }

    // 3) Deletion of a node (by value, deletes the first occurrence)
    void deleteNode(int val) {
        if (head == nullptr) {
            std::cout << "List is empty. Cannot delete." << std::endl;
            return;
        }

        // If the node to be deleted is the head
        if (head->data == val) {
            Node* temp = head;
            head = head->next;
            delete temp;
            return;
        }

        Node* current = head;
        Node* prev = nullptr;

        while (current != nullptr && current->data != val) {
            prev = current;
            current = current->next;
        }

        if (current == nullptr) {
            std::cout << "Value not found in the list." << std::endl;
            return;
        }

        prev->next = current->next;
        delete current;
    }

    // 4) Displaying the entire list
    void display() {
        if (head == nullptr) {
            std::cout << "List is empty." << std::endl;
            return;
        }

        Node* temp = head;
        while (temp != nullptr) {
            std::cout << temp->data << " -> ";
            temp = temp->next;
        }
        std::cout << "nullptr" << std::endl;
    }
};

int main() {
    LinkedList list;

    // Demonstrate operations
    list.insertAtBeginning(10);
    list.insertAtBeginning(20);
    list.insertAtEnd(30);
    list.insertAtEnd(40);

    std::cout << "List after insertions: ";
    list.display();

    list.deleteNode(20);
    std::cout << "List after deleting 20: ";
    list.display();

    list.deleteNode(50); // Trying to delete a non-existent value
    std::cout << "List after attempting to delete 50: ";
    list.display();

    return 0;
}
```

EXPLANATION :-
```cpp
struct Node {
    int data;
    Node* next;
};
```
Functionality: This defines a simple structure for each node in the linked list.

int data: Stores the value (an integer) held by the node.

Node* next: A pointer to the next node in the list. For the last node, this is nullptr.

LinkedList Class
The LinkedList class manages the list. It has a private member Node* head (initially nullptr for an empty list) and public methods for operations.

Constructor and Destructor

```cpp
LinkedList() {
    head = nullptr;
}

~LinkedList() {
    Node* current = head;
    while (current != nullptr) {
        Node* next = current->next;
        delete current;
        current = next;
    }
}
```
Constructor (LinkedList()): Initializes an empty list by setting head to nullptr.
Destructor (~LinkedList()): Automatically called when the LinkedList object is destroyed (e.g., at the end of main). It traverses the list, deleting each node to free memory and prevent leaks. This is crucial for dynamic allocation.

```cpp
void insertAtBeginning(int val) {
    Node* newNode = new Node();
    newNode->data = val;
    newNode->next = head;
    head = newNode;
}
```
Functionality: Adds a new node with the given value (val) at the start of the list.

Allocates a new Node on the heap using new.

Sets its data to val and next to the current head (so it points to the old first node).

Updates head to point to the new node.


```cpp
void insertAtEnd(int val) {
    Node* newNode = new Node();
    newNode->data = val;
    newNode->next = nullptr;

    if (head == nullptr) {
        head = newNode;
        return;
    }

    Node* temp = head;
    while (temp->next != nullptr) {
        temp = temp->next;
    }
    temp->next = newNode;
}
```
Functionality: Adds a new node with the given value (val) at the end of the list.

Allocates a new Node and sets its data to val and next to nullptr.

If the list is empty (head == nullptr), sets head to the new node.

Otherwise, traverses the list using a temporary pointer (temp) to find the last node (where next is nullptr), then links the new node to it.


```cpp
void deleteNode(int val) {
    if (head == nullptr) {
        std::cout << "List is empty. Cannot delete." << std::endl;
        return;
    }

    // If the node to be deleted is the head
    if (head->data == val) {
        Node* temp = head;
        head = head->next;
        delete temp;
        return;
    }

    Node* current = head;
    Node* prev = nullptr;

    while (current != nullptr && current->data != val) {
        prev = current;
        current = current->next;
    }

    if (current == nullptr) {
        std::cout << "Value not found in the list." << std::endl;
        return;
    }

    prev->next = current->next;
    delete current;
}
```
Functionality: Removes the first node containing the specified value (val).
Checks if the list is empty and prints a message if so.
Special case: If the head node matches val, updates head to the next node and deletes the old head.
Otherwise, uses two pointers (current and prev) to traverse the list until finding the node with val.
If found, links the previous node to the next one (skipping the current node) and deletes it.
If not found, prints a message.
Time Complexity: O(n) – May traverse the entire list.
Edge Cases: Handles empty list, deletion of head, and non-existent values. Note: This deletes only the first occurrence; for multiple same values, it wouldn't remove all.

```cpp
void display() {
    if (head == nullptr) {
        std::cout << "List is empty." << std::endl;
        return;
    }

    Node* temp = head;
    while (temp != nullptr) {
        std::cout << temp->data << " -> ";
        temp = temp->next;
    }
    std::cout << "nullptr" << std::endl;
}
```
Functionality: Prints the contents of the list to the console.
If empty, prints a message.

Otherwise, starts from head and traverses the list, printing each node's data followed by " -> ", ending with "nullptr" to indicate the end.

Output Format: E.g., "10 -> 20 -> 30 -> nullptr" for a list with values 10, 20, 30.

Main Function

```cpp
int main() {
    LinkedList list;

    // Demonstrate operations
    list.insertAtBeginning(10);
    list.insertAtBeginning(20);
    list.insertAtEnd(30);
    list.insertAtEnd(40);

    std::cout << "List after insertions: ";
    list.display();

    list.deleteNode(20);
    std::cout << "List after deleting 20: ";
    list.display();

    list.deleteNode(50); // Trying to delete a non-existent value
    std::cout << "List after attempting to delete 50: ";
    list.display();

    return 0;
}
```

# Dynamically allocating memory for an array of integers using new and delete and performing certain operations.

```cpp
#include <iostream>

int main() {
    int size;

    // 1) Allow the user to enter the size of the array
    std::cout << "Enter the size of the array: ";
    std::cin >> size;

    // Basic validation: Ensure size is positive
    if (size <= 0) {
        std::cout << "Invalid size. Size must be a positive integer." << std::endl;
        return 1; // Exit with error code
    }

    // Dynamically allocate memory for the array using new
    int* arr = new int[size];

    // 2) Allow the user to enter the values for the array
    std::cout << "Enter " << size << " integer values for the array:" << std::endl;
    for (int i = 0; i < size; ++i) {
        std::cout << "Element " << i + 1 << ": ";
        std::cin >> arr[i];
    }

    // Optional: Display the array to confirm input
    std::cout << "The array elements are: ";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    // 3) Free the allocated memory using delete
    delete[] arr;
    arr = nullptr; // Good practice to set pointer to nullptr after deletion

    std::cout << "Memory has been freed." << std::endl;

    return 0;
}
```

EXPLANATION :-
Allow the User to Enter the Size of the Array

```cpp
std::cout << "Enter the size of the array: ";
std::cin >> size;

if (size <= 0) {
    std::cout << "Invalid size. Size must be a positive integer." << std::endl;
    return 1;
}
```
Functionality: Prompts the user to input an integer for the array size. Reads it using std::cin.

Includes basic validation: If the size is not positive (e.g., 0 or negative), it prints an error message and exits the program with a non-zero code (indicating failure). This prevents invalid allocations.

Dynamically Allocate Memory for the Array

```cpp
int* arr = new int[size];
```
Functionality: Allocates memory on the heap for an array of size integers using new[]. The pointer arr now points to the start of this array.

new int[size] creates contiguous memory for size integers. If allocation fails (e.g., due to insufficient memory), new throws a std::bad_alloc exception (though not explicitly caught here for simplicity).

Allow the User to Enter the Values for the Array

```cpp
std::cout << "Enter " << size << " integer values for the array:" << std::endl;
for (int i = 0; i < size; ++i) {
    std::cout << "Element " << i + 1 << ": ";
    std::cin >> arr[i];
}

std::cout << "The array elements are: ";
for (int i = 0; i < size; ++i) {
    std::cout << arr[i] << " ";
}
std::cout << std::endl;
```
Functionality: Loops through the array, prompting the user to enter a value for each element (1-based indexing in prompts for user-friendliness). Stores each input in arr[i].

After input, it displays the entire array to confirm what was entered.

Edge Cases: If the user enters non-integer values, std::cin may fail (e.g., entering "abc" could leave invalid data). In production code, you'd add error checking for input streams.

Free the Allocated Memory Using delete

```cpp
delete[] arr;
arr = nullptr;
std::cout << "Memory has been freed." << std::endl;
```

Functionality: Deallocates the memory allocated by new[] using delete[]. This is crucial to prevent memory leaks.

delete[] must be used for arrays (not just delete), as it properly handles deallocating multiple elements.

Sets arr to nullptr afterward to avoid accidental use of a dangling pointer (a pointer to freed memory).

# Swapping two numbers using pointers

```cpp
#include <iostream>

void swap(int* ptr1, int* ptr2) {
    int temp = *ptr1;
    *ptr1 = *ptr2;
    *ptr2 = temp;
}

int main() {
    int a, b;

    // User inputs values for the two integers
    std::cout << "Enter the first number: ";
    std::cin >> a;
    std::cout << "Enter the second number: ";
    std::cin >> b;

    // Declare pointers pointing to the variables
    int* ptrA = &a;
    int* ptrB = &b;

    // Display original values
    std::cout << "Before swapping: a = " << a << ", b = " << b << std::endl;

    // Swap using pointers
    swap(ptrA, ptrB);

    // Display swapped values
    std::cout << "After swapping: a = " << a << ", b = " << b << std::endl;

    return 0;
}
```

EXPLANATION :-

Variable Declaration: int a, b; declares two integer variables to hold the user-input values.
User Input:
Prompts the user to enter values for a and b using std::cout.

Reads the inputs into a and b using std::cin.

Pointer Declaration and Assignment:

int* ptrA = &a;: Declares a pointer ptrA of type int* and initializes it with the address of a (using the address-of operator &).
int* ptrB = &b;: Similarly, declares ptrB pointing to b.

Now, ptrA holds the memory address of a, and ptrB holds the address of b.

Displaying Original Values: Prints the values of a and b before swapping to show the initial state.

Swapping: Calls swap(ptrA, ptrB);, passing the pointers. The function modifies the values at these addresses, effectively swapping a and b.

Displaying Swapped Values: Prints the values after swapping to confirm the change.

Return Statement: return 0; indicates successful program execution.

# Dynamically allocating memory for an array of strings (an array of pointers) and performing certain operations.

```cpp
#include <iostream>
#include <string>
#include <cstring>  // For strcpy

int main() {
    int n;

    // 1) Allow the user to input the number of strings
    std::cout << "Enter the number of strings: ";
    std::cin >> n;
    std::cin.ignore();  // Ignore the newline character left in the input buffer after std::cin >> n

    // Dynamically allocate an array of pointers (char**) for the strings
    char** strings = new char*[n];

    // Input each string
    for (int i = 0; i < n; ++i) {
        std::string input;
        std::cout << "Enter string " << i + 1 << ": ";
        std::getline(std::cin, input);  // Use getline to read the entire line, including spaces

        // Dynamically allocate memory for the string and copy it
        strings[i] = new char[input.length() + 1];
        strcpy(strings[i], input.c_str());
    }

    // 2) Print all the strings using the array of pointers
    std::cout << "\nThe strings are:" << std::endl;
    for (int i = 0; i < n; ++i) {
        std::cout << strings[i] << std::endl;
    }

    // 3) Free the allocated memory for each string and the array of pointers using delete
    for (int i = 0; i < n; ++i) {
        delete[] strings[i];  // Free memory for each individual string
    }
    delete[] strings;  // Free the array of pointers
    strings = nullptr;  // Set to nullptr to avoid dangling pointer

    std::cout << "\nMemory has been freed." << std::endl;

    return 0;
}
```

EXPLANATION :-
Allow the User to Input Multiple Strings

```cpp
std::cout << "Enter the number of strings: ";
std::cin >> n;
std::cin.ignore();  // Ignore the newline character left in the input buffer after std::cin >> n

char** strings = new char*[n];

for (int i = 0; i < n; ++i) {
    std::string input;
    std::cout << "Enter string " << i + 1 << ": ";
    std::getline(std::cin, input);

    strings[i] = new char[input.length() + 1];
    strcpy(strings[i], input.c_str());
}
```
Functionality: First, prompts the user for the number of strings (n) and reads it with std::cin. The std::cin.ignore() call is crucial—it discards the newline character left in the input buffer after reading n, preventing issues with subsequent std::getline calls (which would otherwise read an empty line).

Allocates an array of n pointers (char** strings = new char*[n];). Each element in this array is a char* that will point to a string.

In the loop, for each string:

Uses std::getline(std::cin, input) to read the entire line (including spaces) into a temporary std::string called input. This is better than std::cin >> input for handling multi-word strings.

Allocates memory for a C-style string: new char[input.length() + 1] (adds 1 for the null terminator \0).

Copies the content from input to the allocated memory using strcpy(strings[i], input.c_str()), where c_str() returns a C-style string pointer.

Stores the pointer to the allocated string in strings[i].

```cpp
std::cout << "\nThe strings are:" << std::endl;
for (int i = 0; i < n; ++i) {
    std::cout << strings[i] << std::endl;
}
```
Functionality: Iterates through the array of pointers (strings), dereferencing each char* to print the string it points to. std::cout << strings[i] treats strings[i] as a C-string and outputs it until the null terminator.

Adds a newline after each string for readability.

```cpp
for (int i = 0; i < n; ++i) {
    delete[] strings[i];  // Free memory for each individual string
}
delete[] strings;  // Free the array of pointers
strings = nullptr;  // Set to nullptr to avoid dangling pointer

std::cout << "\nMemory has been freed." << std::endl;
```
Functionality: Properly deallocates all dynamically allocated memory to prevent memory leaks.

First loop: For each string, uses delete[] strings[i] to free the memory allocated for that C-string (since new char[] was used).

Then, delete[] strings frees the array of pointers itself.

Sets strings = nullptr to prevent accidental access to freed memory (a dangling pointer).

# Demonstrating the use of a pointer to a constant variable and performing certain operations.

```cpp
#include <iostream>

int main() {
    // 1) Declare a constant variable and a pointer to it
    const int constantVar = 42;  // Declare a constant integer variable
    const int* ptr = &constantVar;  // Declare a pointer to a constant integer, pointing to constantVar

    // 2) Show how you can read the value pointed to by the pointer, but not modify it
    // Reading the value through the pointer
    std::cout << "Value of constantVar through pointer: " << *ptr << std::endl;

    // Attempting to modify the value through the pointer would cause a compile error
    // Uncommenting the line below will result in a compilation error:
    // *ptr = 50;  // Error: assignment of read-only location '*ptr'

    // Note: The pointer itself can be reassigned to point to another constant or non-constant variable,
    // but it cannot be used to modify the value it points to.
    // For example:
    int anotherVar = 100;
    ptr = &anotherVar;  // Valid: Reassigning the pointer
    std::cout << "Value of anotherVar through pointer: " << *ptr << std::endl;

    // But still cannot modify through ptr:
    // *ptr = 200;  // This would also cause a compile error

    return 0;
}
```

EXPLANATION :-

Declaration of Constant Variable:

const int constantVar = 42;: Creates an integer constant initialized to 42. Its value cannot be changed directly (e.g., constantVar = 50; would be invalid).

Declaration of Pointer to Constant:

const int* ptr = &constantVar;: Declares ptr as a pointer to a constant integer. It points to constantVar. The const applies to the type being pointed to, meaning you can't modify what ptr points to.

Reading the Value:

std::cout << "Value of constantVar through pointer: " << *ptr << std::endl;: Dereferences ptr to access and print the value (42). This is allowed because reading doesn't modify the constant.

Attempted Modification (Commented Out):
// *ptr = 50;: This line is commented to prevent a compile error. If uncommented, the compiler would reject it with an error like "assignment of read-only location '*ptr'" because ptr points to a constant.

This demonstrates the restriction: You can read but not write through a pointer to a constant.

Reassigning the Pointer:

int anotherVar = 100;: Declares a non-constant integer.

ptr = &anotherVar;: Reassigns ptr to point to anotherVar. This is valid because the pointer itself is not constant (only what it points to is constant).
std::cout << "Value of anotherVar through pointer: " << *ptr << std::endl;: Prints 100, showing the pointer now points to a different variable.

Return Statement: return 0; indicates successful execution.

# Writing a C++ program where a function returns a reference to a local variable.

```cpp
#include <iostream>

// Problematic version: Function returning a reference to a local variable
int& getLocalReference() {
    int localVar = 42;  // Local variable on the stack
    return localVar;    // Returning a reference to it
}

int main() {
    // This is undefined behavior!
    int& ref = getLocalReference();  // ref now points to a destroyed local variable
    std::cout << "Value through reference: " << ref << std::endl;  // Might print garbage or crash
    // Modifying it could corrupt memory
    // ref = 100;  // Dangerous!

    return 0;
}
```

Potential Problems with Returning a Reference to a Local Variable
Returning a reference to a local variable in C++ is highly problematic and leads to undefined behavior. Here's why and how to avoid it:

Problems:

Lifetime of Local Variables: Local variables (e.g., localVar in getLocalReference()) are allocated on the stack and are destroyed when the function returns. The reference (ref in main()) becomes a "dangling reference" pointing to invalid memory.

Undefined Behavior: Accessing or modifying through such a reference can result in:

Printing garbage values.

In some cases, it might "work" temporarily (e.g., if the stack space isn't overwritten yet), but this is unreliable and not guaranteed.

No Compile-Time Error: C++ compilers often don't catch this, making it a runtime issue that's hard to debug.

Security Risks: In larger programs, this could lead to vulnerabilities if the corrupted memory is accessed elsewhere.

How to Avoid These Problems:

Don't Return References to Locals: Simply avoid this pattern. If you need to return a value, return by value (e.g., int getValue() { int x = 42; return x; }).

Use Static or Global Variables: As shown in the safe version below, declare the variable as static (inside the function) or global (outside). These persist beyond the function's scope.

Return Pointers Carefully: If using pointers, ensure the pointed-to memory outlives the function (e.g., dynamically allocated with new, but remember to delete later).

Use Smart Pointers or References to Globals/Statics: For complex cases, consider std::shared_ptr or references to persistent objects.

Here's a corrected version where the function returns a reference to a static variable (declared inside the function).

```cpp
#include <iostream>

// Safe version: Function returning a reference to a static variable
int& getStaticReference() {
    static int staticVar = 42;  // Static variable persists beyond function calls
    return staticVar;           // Safe to return a reference to it
}

int main() {
    int& ref = getStaticReference();  // ref now safely points to staticVar
    std::cout << "Value through reference: " << ref << std::endl;  // Prints 42

    // Modifying it is safe and affects the static variable
    ref = 100;
    std::cout << "Modified value: " << ref << std::endl;  // Prints 100

    // Calling the function again returns the same reference
    int& ref2 = getStaticReference();
    std::cout << "Value through second reference: " << ref2 << std::endl;  // Prints 100 (same variable)

    return 0;
}
```

Explanation of the Safe Version

Static Variable Declaration: static int staticVar = 42; inside getStaticReference(). This variable is created once when the function is first called and retains its value across multiple calls. It's not destroyed when the function exits.

Returning the Reference: return staticVar; is safe because staticVar outlives the function.

Usage in main():

int& ref = getStaticReference();: Gets a reference to the static variable.

Reading and modifying through ref works correctly, as it directly affects staticVar.

Subsequent calls (e.g., ref2) reference the same variable, demonstrating persistence.

Advantages: No undefined behavior, and it's thread-safe in this simple case (though statics can have concurrency issues in multi-threaded programs).

