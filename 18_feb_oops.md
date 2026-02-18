# Creating a Student class with attributes: name, roll number, and marks and performing certain operations.

```cpp
#include <iostream>
#include <string>

class Student {
private:
    std::string name;
    int roll_number;
    float marks;

public:
    // Function to input student details
    void input() {
        std::cout << "Enter name: ";
        std::getline(std::cin, name);
        std::cout << "Enter roll number: ";
        std::cin >> roll_number;
        std::cout << "Enter marks: ";
        std::cin >> marks;
        std::cin.ignore(); // To handle newline after cin
    }

    // Function to display student details
    void display() const {
        std::cout << "Name: " << name << std::endl;
        std::cout << "Roll Number: " << roll_number << std::endl;
        std::cout << "Marks: " << marks << std::endl;
        std::cout << "-------------------" << std::endl;
    }
};

int main() {
    Student s1, s2, s3;

    std::cout << "Enter details for Student 1:" << std::endl;
    s1.input();

    std::cout << "Enter details for Student 2:" << std::endl;
    s2.input();

    std::cout << "Enter details for Student 3:" << std::endl;
    s3.input();

    std::cout << "\nDisplaying student details:" << std::endl;
    s1.display();
    s2.display();
    s3.display();

    return 0;
}
```


# Creating a BankAccount Class with Constructor and Destructor.

```cpp
#include <iostream>

class BankAccount {
private:
    int account_number;
    double balance;

public:
    // Constructor to initialize account number and balance
    BankAccount(int acc_num, double bal) : account_number(acc_num), balance(bal) {
        std::cout << "Account " << account_number << " created with balance $" << balance << std::endl;
    }

    // Destructor to display a message
    ~BankAccount() {
        std::cout << "Destructor called for account " << account_number << std::endl;
    }
};

// Function to create objects and observe destructor behavior
void createAccounts() {
    BankAccount acc1(12345, 1000.0);
    BankAccount acc2(67890, 2500.0);
    std::cout << "Inside createAccounts function." << std::endl;
    // Objects go out of scope here, destructors will be called
}

int main() {
    std::cout << "Calling createAccounts function:" << std::endl;
    createAccounts();
    std::cout << "Back in main. Program ending." << std::endl;
    return 0;
}
```


# Creating an Employee class with private specifier and validation

```cpp
#include <iostream>
#include <string>

class Employee {
private:
    std::string name;
    double salary;  // Private member

public:
    // Constructor to initialize name and salary
    Employee(std::string emp_name, double emp_salary) : name(emp_name) {
        setSalary(emp_salary);  // Use setter for validation
    }

    // Setter for salary with validation
    void setSalary(double s) {
        if (s >= 0) {
            salary = s;
        } else {
            std::cout << "Error: Salary cannot be negative. Setting to 0." << std::endl;
            salary = 0;
        }
    }

    // Getter for salary
    double getSalary() const {
        return salary;
    }

    // Function to display employee details
    void display() const {
        std::cout << "Name: " << name << std::endl;
        std::cout << "Salary: $" << salary << std::endl;
    }
};

int main() {
    Employee emp1("Alice", 50000.0);
    Employee emp2("Bob", -1000.0);  // Invalid salary, will be set to 0

    std::cout << "Employee 1:" << std::endl;
    emp1.display();

    std::cout << "\nEmployee 2:" << std::endl;
    emp2.display();

    // Demonstrate setter
    emp2.setSalary(45000.0);
    std::cout << "\nAfter updating Employee 2's salary:" << std::endl;
    emp2.display();

    return 0;
}
```


# Creating a class Calculator and using method overloading.

```cpp
#include <iostream>

class Calculator {
public:
    // Overloaded add function for two integers
    int add(int a, int b) {
        return a + b;
    }

    // Overloaded add function for two doubles
    double add(double a, double b) {
        return a + b;
    }

    // Overloaded add function for three integers
    int add(int a, int b, int c) {
        return a + b + c;
    }

    // Overloaded add function for three doubles (for completeness)
    double add(double a, double b, double c) {
        return a + b + c;
    }
};

int main() {
    Calculator calc;

    // Demonstrate add for two integers
    std::cout << "add(5, 3) = " << calc.add(5, 3) << std::endl;

    // Demonstrate add for two doubles
    std::cout << "add(5.5, 3.2) = " << calc.add(5.5, 3.2) << std::endl;

    // Demonstrate add for three integers
    std::cout << "add(1, 2, 3) = " << calc.add(1, 2, 3) << std::endl;

    // Demonstrate add for three doubles
    std::cout << "add(1.1, 2.2, 3.3) = " << calc.add(1.1, 2.2, 3.3) << std::endl;

    return 0;
}
```


# Student Class with Dynamic Subjects Array using Struct.

```cpp
#include <iostream>
#include <string>

struct Subject {
    std::string name;
    int marks;
};

class Student {
private:
    int roll;
    std::string name;
    Subject* subjects;
    int n;

public:
    // Constructor: Allocates dynamic memory for n subjects
    Student(int r, std::string nm, int num_subjects) : roll(r), name(nm), n(num_subjects) {
        subjects = new Subject[n];
    }

    // Destructor: Frees dynamic memory for subjects
    ~Student() {
        delete[] subjects;
    }

    // Input function: Inputs details for each subject
    void input() {
        for (int i = 0; i < n; ++i) {
            std::cout << "Enter subject " << (i + 1) << " name: ";
            std::cin >> subjects[i].name;
            std::cout << "Enter marks for " << subjects[i].name << ": ";
            std::cin >> subjects[i].marks;
        }
    }

    // Display function: Shows student and subject details
    void display() const {
        std::cout << "Roll: " << roll << std::endl;
        std::cout << "Name: " << name << std::endl;
        std::cout << "Subjects:" << std::endl;
        for (int i = 0; i < n; ++i) {
            std::cout << "  " << subjects[i].name << ": " << subjects[i].marks << std::endl;
        }
        std::cout << "Total Marks: " << total() << std::endl;
        std::cout << "Grade: " << grade() << std::endl;
        std::cout << "-------------------" << std::endl;
    }

    // Total function: Sums up marks
    int total() const {
        int sum = 0;
        for (int i = 0; i < n; ++i) {
            sum += subjects[i].marks;
        }
        return sum;
    }

    // Grade function: Assigns grade based on total (assuming max marks per subject is 100, total max is 100*n)
    char grade() const {
        int t = total();
        int max_possible = 100 * n;
        double percentage = (static_cast<double>(t) / max_possible) * 100;
        if (percentage >= 90) return 'A';
        else if (percentage >= 80) return 'B';
        else if (percentage >= 70) return 'C';
        else if (percentage >= 60) return 'D';
        else return 'F';
    }

    // Getter for name (used for finding topper)
    std::string getName() const { return name; }
};

int main() {
    int N;
    std::cout << "Enter number of students: ";
    std::cin >> N;

    // Dynamic array of student pointers
    Student** students = new Student*[N];

    for (int i = 0; i < N; ++i) {
        int roll, n_subjects;
        std::string name;
        std::cout << "\nEnter details for Student " << (i + 1) << ":" << std::endl;
        std::cout << "Roll: ";
        std::cin >> roll;
        std::cout << "Name: ";
        std::cin >> name;
        std::cout << "Number of subjects: ";
        std::cin >> n_subjects;

        students[i] = new Student(roll, name, n_subjects);
        students[i]->input();
    }

    // Display all students
    std::cout << "\nDisplaying all students:" << std::endl;
    for (int i = 0; i < N; ++i) {
        students[i]->display();
    }

    // Find topper (student with highest total marks)
    int topper_index = 0;
    int max_total = students[0]->total();
    for (int i = 1; i < N; ++i) {
        if (students[i]->total() > max_total) {
            max_total = students[i]->total();
            topper_index = i;
        }
    }
    std::cout << "Topper: " << students[topper_index]->getName() << " with total marks " << max_total << std::endl;

    // Free memory: Delete each student (destructor handles subjects), then the array
    for (int i = 0; i < N; ++i) {
        delete students[i];
    }
    delete[] students;

    return 0;
}
```


# PatientQueue Class with Priority Enqueue

```cpp
#include <iostream>
#include <string>

struct Node {
    int id;
    std::string name;
    int severity;
    Node* next;
};

class PatientQueue {
private:
    Node* front;  // Points to the front of the queue (highest priority)

public:
    // Constructor
    PatientQueue() : front(nullptr) {}

    // Destructor: Frees all nodes
    ~PatientQueue() {
        while (front) {
            dequeue();  // Dequeue will handle deletion
        }
    }

    // Enqueue: Inserts based on severity (higher severity first)
    void enqueue(int id, std::string name, int severity) {
        Node* newNode = new Node{id, name, severity, nullptr};

        if (!front || severity > front->severity) {
            // Insert at front if higher severity or empty queue
            newNode->next = front;
            front = newNode;
        } else {
            // Find position to insert (after nodes with higher or equal severity)
            Node* current = front;
            while (current->next && current->next->severity >= severity) {
                current = current->next;
            }
            newNode->next = current->next;
            current->next = newNode;
        }
        std::cout << "Enqueued: " << name << " (ID: " << id << ", Severity: " << severity << ")" << std::endl;
    }

    // Dequeue: Removes and deletes the front node
    void dequeue() {
        if (!front) {
            std::cout << "Queue is empty. Cannot dequeue." << std::endl;
            return;
        }
        Node* temp = front;
        front = front->next;
        std::cout << "Dequeued: " << temp->name << " (ID: " << temp->id << ", Severity: " << temp->severity << ")" << std::endl;
        delete temp;
    }

    // Display: Shows all patients in the queue
    void display() const {
        if (!front) {
            std::cout << "Queue is empty." << std::endl;
            return;
        }
        Node* current = front;
        std::cout << "Patient Queue (from highest to lowest priority):" << std::endl;
        while (current) {
            std::cout << "ID: " << current->id << ", Name: " << current->name << ", Severity: " << current->severity << std::endl;
            current = current->next;
        }
    }
};

int main() {
    PatientQueue queue;

    // Demonstrate enqueue
    queue.enqueue(1, "Alice", 5);
    queue.enqueue(2, "Bob", 3);
    queue.enqueue(3, "Charlie", 7);  // Higher severity, should go to front
    queue.enqueue(4, "Diana", 4);

    std::cout << "\nAfter enqueues:" << std::endl;
    queue.display();

    // Demonstrate dequeue
    std::cout << "\nDequeue operations:" << std::endl;
    queue.dequeue();
    queue.display();

    queue.dequeue();
    queue.display();

    // Add more and dequeue
    queue.enqueue(5, "Eve", 6);
    std::cout << "\nAfter adding Eve:" << std::endl;
    queue.display();

    queue.dequeue();
    queue.display();

    // Destructor will clean up remaining nodes when queue goes out of scope
    return 0;
}
```


# Library Class with BookNode Linked List

```cpp
#include <iostream>
#include <string>

struct BookNode {
    int id;
    std::string title;
    std::string author;
    bool issued;
    BookNode* next;
};

class Library {
private:
    BookNode* head;

public:
    // Constructor
    Library() : head(nullptr) {}

    // Destructor: Frees all nodes in the linked list
    ~Library() {
        BookNode* current = head;
        while (current) {
            BookNode* temp = current;
            current = current->next;
            delete temp;
        }
    }

    // Add a new book to the end of the list
    void addBook(int id, std::string title, std::string author) {
        BookNode* newNode = new BookNode{id, title, author, false, nullptr};
        if (!head) {
            head = newNode;
        } else {
            BookNode* current = head;
            while (current->next) {
                current = current->next;
            }
            current->next = newNode;
        }
        std::cout << "Book added: " << title << std::endl;
    }

    // Issue a book by ID
    void issueBook(int id) {
        BookNode* current = head;
        while (current) {
            if (current->id == id) {
                if (!current->issued) {
                    current->issued = true;
                    std::cout << "Book issued: " << current->title << std::endl;
                } else {
                    std::cout << "Book already issued: " << current->title << std::endl;
                }
                return;
            }
            current = current->next;
        }
        std::cout << "Book with ID " << id << " not found." << std::endl;
    }

    // Return a book by ID
    void returnBook(int id) {
        BookNode* current = head;
        while (current) {
            if (current->id == id) {
                if (current->issued) {
                    current->issued = false;
                    std::cout << "Book returned: " << current->title << std::endl;
                } else {
                    std::cout << "Book was not issued: " << current->title << std::endl;
                }
                return;
            }
            current = current->next;
        }
        std::cout << "Book with ID " << id << " not found." << std::endl;
    }

    // Search for a book by title
    void searchBook(std::string title) {
        BookNode* current = head;
        while (current) {
            if (current->title == title) {
                std::cout << "Book found - ID: " << current->id << ", Title: " << current->title
                          << ", Author: " << current->author << ", Issued: " << (current->issued ? "Yes" : "No") << std::endl;
                return;
            }
            current = current->next;
        }
        std::cout << "Book with title '" << title << "' not found." << std::endl;
    }

    // Display all books
    void displayAll() {
        if (!head) {
            std::cout << "No books in the library." << std::endl;
            return;
        }
        BookNode* current = head;
        std::cout << "Library Books:" << std::endl;
        while (current) {
            std::cout << "ID: " << current->id << ", Title: " << current->title
                      << ", Author: " << current->author << ", Issued: " << (current->issued ? "Yes" : "No") << std::endl;
            current = current->next;
        }
    }
};

int main() {
    Library lib;

    // Add books
    lib.addBook(1, "1984", "George Orwell");
    lib.addBook(2, "To Kill a Mockingbird", "Harper Lee");
    lib.addBook(3, "The Great Gatsby", "F. Scott Fitzgerald");

    // Display all
    lib.displayAll();

    // Issue and return books
    lib.issueBook(1);
    lib.issueBook(1);  // Try issuing again
    lib.returnBook(1);
    lib.returnBook(1);  // Try returning again

    // Search
    lib.searchBook("1984");
    lib.searchBook("Nonexistent Book");

    // Display again
    lib.displayAll();

    // Destructor will clean up memory
    return 0;
}
```


# BankAccount Class with Transaction Linked List

```cpp

#include <iostream>
#include <string>

struct Transaction {
    std::string type;  // "Deposit" or "Withdraw"
    double amount;
    std::string date;
    Transaction* next;
};

class BankAccount {
private:
    int accountNo;
    std::string holderName;
    double balance;
    Transaction* historyHead;

public:
    // Constructor
    BankAccount(int accNo, std::string name, double initialBalance = 0.0)
        : accountNo(accNo), holderName(name), balance(initialBalance), historyHead(nullptr) {}

    // Destructor: Frees all transaction nodes
    ~BankAccount() {
        Transaction* current = historyHead;
        while (current) {
            Transaction* temp = current;
            current = current->next;
            delete temp;
        }
    }

    // Deposit money and add to history
    void deposit(double amount, std::string date) {
        balance += amount;
        addTransaction("Deposit", amount, date);
        std::cout << "Deposited $" << amount << " on " << date << ". New balance: $" << balance << std::endl;
    }

    // Withdraw money (if sufficient balance) and add to history
    void withdraw(double amount, std::string date) {
        if (amount > balance) {
            std::cout << "Insufficient balance. Cannot withdraw $" << amount << "." << std::endl;
            return;
        }
        balance -= amount;
        addTransaction("Withdraw", amount, date);
        std::cout << "Withdrew $" << amount << " on " << date << ". New balance: $" << balance << std::endl;
    }

    // Show transaction history
    void showHistory() const {
        if (!historyHead) {
            std::cout << "No transactions for account " << accountNo << "." << std::endl;
            return;
        }
        Transaction* current = historyHead;
        std::cout << "Transaction History for " << holderName << " (Account " << accountNo << "):" << std::endl;
        while (current) {
            std::cout << current->type << " $" << current->amount << " on " << current->date << std::endl;
            current = current->next;
        }
    }

    // Show current balance
    void showBalance() const {
        std::cout << "Account " << accountNo << " (" << holderName << ") Balance: $" << balance << std::endl;
    }

    // Getters for searching
    int getAccountNo() const { return accountNo; }
    std::string getHolderName() const { return holderName; }

private:
    // Helper to add a transaction to the history list
    void addTransaction(std::string type, double amount, std::string date) {
        Transaction* newTrans = new Transaction{type, amount, date, nullptr};
        if (!historyHead) {
            historyHead = newTrans;
        } else {
            Transaction* current = historyHead;
            while (current->next) {
                current = current->next;
            }
            current->next = newTrans;
        }
    }
};

int main() {
    const int NUM_ACCOUNTS = 3;
    BankAccount** accounts = new BankAccount*[NUM_ACCOUNTS];

    // Create accounts
    accounts[0] = new BankAccount(1001, "Alice", 1000.0);
    accounts[1] = new BankAccount(1002, "Bob", 500.0);
    accounts[2] = new BankAccount(1003, "Charlie", 2000.0);

    // Perform operations on accounts
    accounts[0]->deposit(500.0, "2023-10-01");
    accounts[0]->withdraw(200.0, "2023-10-02");
    accounts[1]->withdraw(600.0, "2023-10-03");  // Insufficient balance
    accounts[2]->deposit(1000.0, "2023-10-04");

    // Show balances
    for (int i = 0; i < NUM_ACCOUNTS; ++i) {
        accounts[i]->showBalance();
    }

    // Show history for one account
    accounts[0]->showHistory();

    // Search for an account by number
    int searchAcc = 1002;
    bool found = false;
    for (int i = 0; i < NUM_ACCOUNTS; ++i) {
        if (accounts[i]->getAccountNo() == searchAcc) {
            std::cout << "Found account: " << accounts[i]->getHolderName() << std::endl;
            accounts[i]->showHistory();
            found = true;
            break;
        }
    }
    if (!found) {
        std::cout << "Account " << searchAcc << " not found." << std::endl;
    }

    // Free memory: Delete each account (destructor handles transactions), then the array
    for (int i = 0; i < NUM_ACCOUNTS; ++i) {
        delete accounts[i];
    }
    delete[] accounts;

    return 0;
}
```


# Student Class with Dynamic Course Registration

```cpp
#include <iostream>
#include <string>

struct Course {
    std::string courseCode;
    std::string courseName;
    int credits;
};

class Student {
private:
    int roll;
    std::string name;
    Course* registeredCourses;
    int numCourses;
    int capacity;  // For dynamic array growth

public:
    // Constructor: Initializes with empty course list
    Student(int r, std::string nm) : roll(r), name(nm), numCourses(0), capacity(2) {
        registeredCourses = new Course[capacity];
    }

    // Destructor: Frees dynamic course array
    ~Student() {
        delete[] registeredCourses;
    }

    // Register courses: Input multiple courses and add to dynamic array
    void registerCourses() {
        int n;
        std::cout << "Enter number of courses to register for " << name << ": ";
        std::cin >> n;
        for (int i = 0; i < n; ++i) {
            if (numCourses == capacity) {
                // Grow array
                capacity *= 2;
                Course* newArray = new Course[capacity];
                for (int j = 0; j < numCourses; ++j) {
                    newArray[j] = registeredCourses[j];
                }
                delete[] registeredCourses;
                registeredCourses = newArray;
            }
            std::cout << "Enter course code: ";
            std::cin >> registeredCourses[numCourses].courseCode;
            std::cout << "Enter course name: ";
            std::cin.ignore();  // Handle newline
            std::getline(std::cin, registeredCourses[numCourses].courseName);
            std::cout << "Enter credits: ";
            std::cin >> registeredCourses[numCourses].credits;
            ++numCourses;
        }
    }

    // Drop a course by code
    void dropCourse(std::string code) {
        for (int i = 0; i < numCourses; ++i) {
            if (registeredCourses[i].courseCode == code) {
                // Shift elements left
                for (int j = i; j < numCourses - 1; ++j) {
                    registeredCourses[j] = registeredCourses[j + 1];
                }
                --numCourses;
                std::cout << "Dropped course: " << code << std::endl;
                return;
            }
        }
        std::cout << "Course " << code << " not found for " << name << std::endl;
    }

    // Show all registered courses
    void showCourses() const {
        std::cout << name << "'s courses:" << std::endl;
        if (numCourses == 0) {
            std::cout << "  No courses registered." << std::endl;
            return;
        }
        for (int i = 0; i < numCourses; ++i) {
            std::cout << "  " << registeredCourses[i].courseCode << " - " << registeredCourses[i].courseName
                      << " (" << registeredCourses[i].credits << " credits)" << std::endl;
        }
    }

    // Total credits
    int totalCredits() const {
        int total = 0;
        for (int i = 0; i < numCourses; ++i) {
            total += registeredCourses[i].credits;
        }
        return total;
    }

    // Check if student is registered in a course
    bool isRegisteredIn(std::string code) const {
        for (int i = 0; i < numCourses; ++i) {
            if (registeredCourses[i].courseCode == code) return true;
        }
        return false;
    }

    // Getters
    int getRoll() const { return roll; }
    std::string getName() const { return name; }
};

int main() {
    int N;
    std::cout << "Enter number of students: ";
    std::cin >> N;

    // Dynamic array of student pointers
    Student** students = new Student*[N];

    for (int i = 0; i < N; ++i) {
        int roll;
        std::string name;
        std::cout << "\nEnter roll and name for Student " << (i + 1) << ": ";
        std::cin >> roll >> name;
        students[i] = new Student(roll, name);
        students[i]->registerCourses();
    }

    // Display all students
    std::cout << "\nAll Students:" << std::endl;
    for (int i = 0; i < N; ++i) {
        students[i]->showCourses();
        std::cout << "Total Credits: " << students[i]->totalCredits() << std::endl;
        std::cout << "-------------------" << std::endl;
    }

    // Print students registered in a given course
    std::string courseCode;
    std::cout << "Enter course code to list registered students: ";
    std::cin >> courseCode;
    std::cout << "Students registered in " << courseCode << ":" << std::endl;
    bool found = false;
    for (int i = 0; i < N; ++i) {
        if (students[i]->isRegisteredIn(courseCode)) {
            std::cout << "  " << students[i]->getName() << " (Roll: " << students[i]->getRoll() << ")" << std::endl;
            found = true;
        }
    }
    if (!found) {
        std::cout << "  No students registered." << std::endl;
    }

    // Free memory
    for (int i = 0; i < N; ++i) {
        delete students[i];
    }
    delete[] students;

    return 0;
}
```


# DirectoryTree Class with DirNode Tree

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <sstream>

struct DirNode {
    std::string name;
    bool isFile;
    DirNode* child;    // First child (subfolder or file)
    DirNode* sibling;  // Next sibling
};

class DirectoryTree {
private:
    DirNode* root;

    // Helper: Split path into tokens (e.g., "/a/b/c" -> ["a", "b", "c"])
    std::vector<std::string> splitPath(const std::string& path) {
        std::vector<std::string> tokens;
        std::stringstream ss(path);
        std::string token;
        while (std::getline(ss, token, '/')) {
            if (!token.empty()) tokens.push_back(token);
        }
        return tokens;
    }

    // Helper: Find or create a node in the tree
    DirNode* findOrCreateNode(DirNode* current, const std::vector<std::string>& path, int index, bool isFile) {
        if (index == path.size()) return current;
        std::string name = path[index];
        DirNode* node = current->child;
        DirNode* prev = nullptr;
        while (node) {
            if (node->name == name) {
                if (index == path.size() - 1 && node->isFile != isFile) {
                    std::cout << "Conflict: " << name << " exists as " << (node->isFile ? "file" : "folder") << std::endl;
                    return nullptr;
                }
                return findOrCreateNode(node, path, index + 1, isFile);
            }
            prev = node;
            node = node->sibling;
        }
        // Create new node
        DirNode* newNode = new DirNode{name, (index == path.size() - 1) ? isFile : false, nullptr, nullptr};
        if (prev) {
            prev->sibling = newNode;
        } else {
            current->child = newNode;
        }
        return findOrCreateNode(newNode, path, index + 1, isFile);
    }

    // Helper: Find a node
    DirNode* findNode(DirNode* current, const std::vector<std::string>& path, int index) {
        if (index == path.size()) return current;
        DirNode* node = current->child;
        while (node) {
            if (node->name == path[index]) {
                return findNode(node, path, index + 1);
            }
            node = node->sibling;
        }
        return nullptr;
    }

    // Helper: Delete a subtree
    void deleteSubtree(DirNode* node) {
        if (!node) return;
        deleteSubtree(node->child);
        deleteSubtree(node->sibling);
        delete node;
    }

    // Helper: Recursive destructor helper
    void destroyTree(DirNode* node) {
        if (!node) return;
        destroyTree(node->child);
        destroyTree(node->sibling);
        delete node;
    }

public:
    // Constructor: Root is a dummy node
    DirectoryTree() {
        root = new DirNode{"root", false, nullptr, nullptr};
    }

    // Destructor: Frees the entire tree
    ~DirectoryTree() {
        destroyTree(root);
    }

    // Create folder
    void createFolder(const std::string& path) {
        std::vector<std::string> tokens = splitPath(path);
        if (tokens.empty()) return;
        findOrCreateNode(root, tokens, 0, false);
        std::cout << "Folder created: " << path << std::endl;
    }

    // Create file
    void createFile(const std::string& path) {
        std::vector<std::string> tokens = splitPath(path);
        if (tokens.empty()) return;
        findOrCreateNode(root, tokens, 0, true);
        std::cout << "File created: " << path << std::endl;
    }

    // List contents of a path
    void list(const std::string& path) {
        std::vector<std::string> tokens = splitPath(path);
        DirNode* dir = findNode(root, tokens, 0);
        if (!dir || dir->isFile) {
            std::cout << "Directory not found: " << path << std::endl;
            return;
        }
        std::cout << "Contents of " << path << ":" << std::endl;
        DirNode* child = dir->child;
        if (!child) {
            std::cout << "  (empty)" << std::endl;
            return;
        }
        while (child) {
            std::cout << "  " << (child->isFile ? "File: " : "Folder: ") << child->name << std::endl;
            child = child->sibling;
        }
    }

    // Delete a node and its subtree
    void deleteNode(const std::string& path) {
        std::vector<std::string> tokens = splitPath(path);
        if (tokens.empty()) return;
        DirNode* parent = root;
        int index = 0;
        while (index < tokens.size() - 1) {
            DirNode* node = parent->child;
            DirNode* prev = nullptr;
            while (node) {
                if (node->name == tokens[index]) {
                    parent = node;
                    break;
                }
                prev = node;
                node = node->sibling;
            }
            if (!node) {
                std::cout << "Path not found: " << path << std::endl;
                return;
            }
            ++index;
        }
        // Now delete the target node
        DirNode* target = parent->child;
        DirNode* prev = nullptr;
        while (target) {
            if (target->name == tokens.back()) {
                if (prev) {
                    prev->sibling = target->sibling;
                } else {
                    parent->child = target->sibling;
                }
                deleteSubtree(target);
                std::cout << "Deleted: " << path << std::endl;
                return;
            }
            prev = target;
            target = target->sibling;
        }
        std::cout << "Node not found: " << path << std::endl;
    }
};

int main() {
    DirectoryTree tree;

    // Create folders and files
    tree.createFolder("/docs");
    tree.createFolder("/docs/reports");
    tree.createFile("/docs/notes.txt");
    tree.createFile("/docs/reports/annual.pdf");

    // List
    tree.list("/");
    tree.list("/docs");
    tree.list("/docs/reports");

    // Delete
    tree.deleteNode("/docs/notes.txt");
    tree.list("/docs");

    // Destructor cleans up
    return 0;
}
```

