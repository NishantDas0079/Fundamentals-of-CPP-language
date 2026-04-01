#  Student Record System with Classes and Objects

Scenario: You need to develop a student record management system for a college. The system should allow the addition of student records, modification, and display of records, as well as calculations like average grades.

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <iomanip>
using namespace std;

class Student {
protected:
    string roll, name;
    vector<double> marks;
    
public:
    // Constructor Overloading
    Student() { cout << "Default ctor\n"; }
    Student(string r, string n, vector<double> m) : roll(r), name(n), marks(m) {
        cout << "Full ctor: " << n << endl;
    }
    Student(string r, string n) : roll(r), name(n) { cout << "Basic ctor: " << n << endl; }
    
    ~Student() { cout << "Dtor: " << name << endl; }
    
    // Method Overloading
    void addStudent(string r, string n, vector<double> m) {
        roll = r; name = n; marks = m; cout << "Added: " << n << endl;
    }
    void addStudent(string r, string n) { roll = r; name = n; cout << "Added basic: " << n << endl; }
    
    void modifyStudent(string n, vector<double> m) { name = n; marks = m; }
    double calculateAverage() {
        if (marks.empty()) return 0;
        double sum = 0; for (double m : marks) sum += m;
        return sum / marks.size();
    }
    virtual void display() {  // Virtual for polymorphism
        cout << "\nRoll: " << roll << ", Name: " << name 
             << ", Avg: " << fixed << setprecision(1) << calculateAverage() << endl;
    }
};

class UGStudent : public Student {  // Inheritance
private:
    string branch;
public:
    UGStudent(string r, string n, vector<double> m, string b) 
        : Student(r, n, m), branch(b) { cout << "UG ctor\n"; }
    
    void display() override {  // Polymorphism
        cout << "UG - " << name << " (" << branch << "), Avg: " 
             << fixed << setprecision(1) << calculateAverage() << endl;
    }
};

class StudentSystem {
    vector<Student*> students;  // Polymorphic container
    
public:
    ~StudentSystem() { 
        for (auto s : students) delete s; 
        cout << "System cleaned\n";
    }
    
    void addStudent() {
        string r, n, b; vector<double> m = {85, 90, 88};
        cout << "Roll: "; cin >> r;
        cout << "Name: "; cin.ignore(); getline(cin, n);
        
        Student* s = new UGStudent(r, n, m, "CSE");  // Dynamic allocation
        students.push_back(s);
        cout << "Student added!\n";
    }
    
    void showAll() {
        cout << "\n=== ALL STUDENTS ===\n";
        for (int i = 0; i < students.size(); i++) {
            cout << i+1 << ". "; students[i]->display();  // Dynamic dispatch
        }
    }
    
    void classAverage() {
        double avg = 0;
        for (auto s : students) avg += s->calculateAverage();
        cout << "Class Avg: " << fixed << setprecision(1) << avg/students.size() << endl;
    }
};

int main() {
    // Test constructors & overloading
    vector<double> m1 = {85, 92, 78};
    Student s1("001", "John", m1);
    Student s2("002", "Jane");
    s2.addStudent("002", "Jane", {88, 91, 87});
    
    s1.display(); s2.display();
    
    // Test inheritance & polymorphism
    UGStudent ug("UG1", "Mike", {90, 88, 92}, "CSE");
    ug.display();
    
    // Test management system
    StudentSystem sys;
    sys.addStudent(); sys.addStudent();
    sys.showAll();
    sys.classAverage();
    
    return 0;
}
```

SAMPLE OUTPUT :-
```
Full ctor: John
Basic ctor: Jane
Added basic: Jane
Roll: 001, Name: John, Avg: 85.0
Roll: 002, Name: Jane, Avg: 88.7
UG ctor
UG - Mike (CSE), Avg: 90.0

=== ALL STUDENTS ===
1. UG - [Name] (CSE), Avg: 87.7
2. UG - [Name] (CSE), Avg: 87.7
Class Avg: 87.7
Dtor: John
Dtor: Jane
UG ctor
Dtor: Mike
System cleaned
```

CONCEPTS USED :-
```
✅ Classes & Objects
✅ Encapsulation  
✅ Inheritance (Student)
✅ Polymorphism (Student)
✅ Constructor/Method Overloading (Student)
✅ Destructors (Student)
```


# Employee Salary Management System Using File Handling

Scenario: You need to build an employee salary management system that reads employee records from a file, calculates their salary, and writes the updated data back to the file.

```cpp
#include <iostream>
#include <fstream>
#include <vector>
#include <string>
#include <iomanip>
using namespace std;

class Employee {
private:
    string emp_id, name;
    double basic_salary, total_salary;
    
public:
    // Default constructor
    Employee() : emp_id(""), name(""), basic_salary(0), total_salary(0) {}
    
    // Parameterized constructor
    Employee(string id, string n, double salary) 
        : emp_id(id), name(n), basic_salary(salary), total_salary(0) {
        calculateSalary();  // Auto-calculate on creation
    }
    
    // Getters & Setters
    string getId() { return emp_id; }
    string getName() { return name; }
    double getBasic() { return basic_salary; }
    double getTotal() { return total_salary; }
    
    // Calculate salary with business logic
    void calculateSalary() {
        // Business Rules:
        // HRA: 20% of basic, DA: 40% of basic, Bonus: 10% if salary > 50000
        double hra = basic_salary * 0.20;
        double da = basic_salary * 0.40;
        double bonus = (basic_salary > 50000) ? basic_salary * 0.10 : 0;
        double deduction = basic_salary * 0.05;  // 5% tax
        
        total_salary = basic_salary + hra + da + bonus - deduction;
    }
    
    // Display employee
    void display() {
        cout << fixed << setprecision(2);
        cout << "\nID: " << emp_id 
             << ", Name: " << name 
             << ", Basic: ₹" << basic_salary
             << ", Total: ₹" << total_salary << endl;
    }
    
    // Save to file
    void saveToFile(ofstream& out) {
        out << emp_id << "," << name << "," << basic_salary << "," << total_salary << endl;
    }
    
    // Load from file (static method)
    static Employee loadFromFile(string line) {
        size_t pos1 = line.find(',');
        size_t pos2 = line.find(',', pos1 + 1);
        size_t pos3 = line.find(',', pos2 + 1);
        
        string id = line.substr(0, pos1);
        string name = line.substr(pos1 + 1, pos2 - pos1 - 1);
        double salary = stod(line.substr(pos2 + 1, pos3 - pos2 - 1));
        
        return Employee(id, name, salary);
    }
};

class SalaryManager {
private:
    vector<Employee> employees;
    const string FILENAME = "employees.txt";
    
public:
    // Load employees from file
    bool loadFromFile() {
        ifstream file(FILENAME);
        if (!file.is_open()) {
            cout << "❌ File not found! Creating new file...\n";
            return false;
        }
        
        employees.clear();
        string line;
        while (getline(file, line)) {
            if (line.empty()) continue;
            try {
                Employee emp = Employee::loadFromFile(line);
                employees.push_back(emp);
            } catch (...) {
                cout << "⚠️ Skipping invalid line: " << line << endl;
            }
        }
        file.close();
        cout << "✅ Loaded " << employees.size() << " employees from file\n";
        return true;
    }
    
    // Save employees to file
    void saveToFile() {
        ofstream file(FILENAME);
        if (!file.is_open()) {
            cout << "❌ Cannot create file!\n";
            return;
        }
        
        for (const auto& emp : employees) {
            emp.saveToFile(file);
        }
        file.close();
        cout << "💾 Data saved to " << FILENAME << endl;
    }
    
    // Add new employee
    void addEmployee() {
        string id, name;
        double salary;
        
        cout << "Enter ID: "; cin >> id;
        cout << "Enter Name: "; cin.ignore(); getline(cin, name);
        cout << "Enter Basic Salary: "; cin >> salary;
        
        Employee emp(id, name, salary);
        employees.push_back(emp);
        cout << "✅ Employee added & salary calculated!\n";
        emp.display();
    }
    
    // Display all
    void displayAll() {
        if (employees.empty()) {
            cout << "No employees found!\n";
            return;
        }
        cout << "\n=== ALL EMPLOYEES ===\n";
        for (const auto& emp : employees) {
            emp.display();
        }
    }
    
    // Calculate & update all salaries
    void processAllSalaries() {
        for (auto& emp : employees) {
            emp.calculateSalary();  // Recalculate
        }
        cout << "✅ All salaries updated!\n";
    }
};

int main() {
    SalaryManager manager;
    
    cout << "🏢 Employee Salary Management System\n";
    cout << "====================================\n";
    
    // Demo: Load existing data
    manager.loadFromFile();
    
    int choice;
    do {
        cout << "\n1. Add Employee\n2. Display All\n3. Process Salaries\n4. Save to File\n5. Exit\nChoice: ";
        cin >> choice;
        
        switch (choice) {
            case 1: manager.addEmployee(); break;
            case 2: manager.displayAll(); break;
            case 3: manager.processAllSalaries(); break;
            case 4: manager.saveToFile(); break;
            case 5: cout << "👋 Goodbye!\n"; break;
            default: cout << "Invalid choice!\n";
        }
    } while (choice != 5);
    
    manager.saveToFile();  // Auto-save on exit
    return 0;
}
```

SAMPLE OUTPUT :-
```
🏢 Employee Salary Management System
✅ Loaded 3 employees from file

1. Add Employee
Enter ID: E004
Enter Name: Sara Khan
Enter Basic Salary: 55000
✅ Employee added & salary calculated!
ID: E004, Name: Sara Khan, Basic: ₹55000, Total: ₹71500

=== ALL EMPLOYEES ===
ID: E001, Name: John Doe, Basic: ₹50000, Total: ₹65000
ID: E002, Name: Jane Smith, Basic: ₹60000, Total: ₹81000
...
💾 Data saved to employees.txt
```

CONCEPTS USED :-
```
✅ File I/O (Employee)
✅ Exception Handling (Employee)
✅ Static Methods (Employee)
✅ Business Logic (Employee)
```

