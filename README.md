# College-work-C++

//Declares one global variable,declares one local variable inside main(),dynamically allocates one integer using new print the addresses
//of all three and identify which memory region each belongs to


#include <iostream>
using namespace std;

int globalVar = 10;   // Global variable (Global/Static memory)

int main() {
    int localVar = 20;        // Local variable (Stack memory)
    int* dynVar = new int;    // Dynamic variable (Heap memory)
    *dynVar = 30;

    cout << "Address of globalVar: " << &globalVar << endl;
    cout << "Address of localVar : " << &localVar << endl;
    cout << "Address of dynVar   : " << dynVar << endl;

    delete dynVar;  // free heap memory
    return 0;
}
//write a funciton square(int) and call it: Normally using a function pointer//
#include <iostream>
using namespace std;

int square(int x) {
    return x * x;
}

int main() {
    int num = 6;

    // Declare a function pointer
    int (*funcPtr)(int);

    // Assign the address of 'square' to the pointer
    funcPtr = square;

    // Call the function using the pointer
    int result2 = funcPtr(num);
    cout << "Square (using pointer) of " << num << " is " << result2 << endl;

    return 0;
}

//Write a program to print: Value of a variable address of the variable value stored in the pointer?


#include <iostream>
using namespace std;

int main() {
    int a = 42;       // Normal variable
    int* ptr = &a;    // Pointer storing the address of 'a'

    cout << "Value of a: " << a << endl;             // Value of the variable
    cout << "Address of a: " << &a << endl;          // Address of the variable
    cout << "Value stored in pointer ptr: " << ptr << endl;  // Value stored in the pointer (address of 'a')

    return 0;
}



//Write a C++ program that dynamically allocates memory for an array of integers using new based on the size input by the user. The program should:

Allow the user to enter the size of the array.

Allow the user to enter the values for the array.

Print the array.

Free the dynamically allocated memory using delete[].

make it user friendly


#include <iostream>
#include <iomanip>  // For pretty printing
using namespace std;

int main() {
    int size;
    
    // 🌈 Welcome message
    cout << "🎯 === DYNAMIC ARRAY MAGIC ===\n";
    cout << "I'll create an array EXACTLY the size you want!\n\n";
    
    // 📏 Get array size
    cout << "How many numbers do you want to store? ";
    cin >> size;
    
    // 🛡️ Check if size is valid
    if (size <= 0) {
        cout << "❌ Oops! Size must be 1 or more. Try again!\n";
        return 1;
    }
    
    // 🧩 Create dynamic array (new magic!)
    int* arr = new int[size];
    
    cout << "\n✨ Great! Created array of size " << size << "\n";
    
    // 📝 Fill the array
    cout << "\n📥 Enter " << size << " numbers:\n";
    for (int i = 0; i < size; i++) {
        cout << "Number " << (i+1) << ": ";
        cin >> arr[i];
    }
    
    // 🖼️ Pretty print the array
    cout << "\n🎨 Your array looks like this:\n";
    cout << "[ ";
    for (int i = 0; i < size; i++) {
        cout << arr[i];
        if (i < size - 1) cout << ", ";
    }
    cout << " ]\n";
    
    // 📊 Bonus: Sum and average
    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum += arr[i];
    }
    double average = (double)sum / size;
    
    cout << "\n📈 Quick stats:\n";
    cout << "   Sum: " << sum << "\n";
    cout << "   Average: " << fixed << setprecision(2) << average << "\n";
    
    // 🧹 Clean up memory (very important!)
    delete[] arr;
    cout << "\n🧹 Memory cleaned up! 👋 Goodbye!\n";
    
    return 0;
}


Write a C++ program to implement a singly linked list using struct for the node and dynamic memory allocation with new and delete. Implement the following operations:

Insertion of a node at the beginning

Insertion of a node at the end

Deletion of a node

Display the entire list
Use new to allocate memory for each node, and delete to free memory when deleting nodes.

#include <iostream>
using namespace std;

// Simple Node structure
struct Node {
    int data;
    Node* next;
};

// Function prototypes (what we'll do)
void insertFront(Node*& head, int value);
void insertEnd(Node*& head, int value);
void deleteNode(Node*& head, int value);
void display(Node* head);
void freeList(Node*& head);

int main() {
    Node* head = NULL;  // Empty list starts with NULL
    
    int choice, value;
    
    cout << "=== SIMPLE LINKED LIST MENU ===\n";
    cout << "1. Add at beginning\n";
    cout << "2. Add at end\n";
    cout << "3. Delete node\n";
    cout << "4. Show list\n";
    cout << "5. Exit\n\n";
    
    do {
        cout << "Enter choice (1-5): ";
        cin >> choice;
        
        switch(choice) {
            case 1:
                cout << "Enter value: ";
                cin >> value;
                insertFront(head, value);
                break;
                
            case 2:
                cout << "Enter value: ";
                cin >> value;
                insertEnd(head, value);
                break;
                
            case 3:
                cout << "Enter value to delete: ";
                cin >> value;
                deleteNode(head, value);
                break;
                
            case 4:
                display(head);
                break;
                
            case 5:
                cout << "Goodbye!\n";
                break;
                
            default:
                cout << "Wrong choice! Try 1-5\n";
        }
        cout << "\n";
        
    } while(choice != 5);
    
    freeList(head);  // Clean up memory
    return 0;
}

// Create a Student class with attributes: name, roll number, and marks.

Add member functions to input and display student details.

Create at least 3 objects and display their data.

// 1. Add at beginning (very simple!)
void insertFront(Node*& head, int value) {
    Node* newNode = new Node;     // Create new node
    newNode->data = value;        // Put data
    newNode->next = head;         // Link to old head
    head = newNode;               // New head!
    cout << "✓ Added " << value << " at front\n";
}

// 2. Add at end
void insertEnd(Node*& head, int value) {
    Node* newNode = new Node;
    newNode->data = value;
    newNode->next = NULL;
    
    if (head == NULL) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != NULL) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "✓ Added " << value << " at end\n";
}

// 3. Delete node
void deleteNode(Node*& head, int value) {
    if (head == NULL) {
        cout << "❌ List empty!\n";
        return;
    }
    
    // Delete first node
    if (head->data == value) {
        Node* temp = head;
        head = head->next;
        delete temp;
        cout << "✓ Deleted " << value << "\n";
        return;
    }
    
    // Find and delete
    Node* current = head;
    while (current->next != NULL && current->next->data != value) {
        current = current->next;
    }
    
    if (current->next == NULL) {
        cout << "❌ " << value << " not found!\n";
    } else {
        Node* temp = current->next;
        current->next = current->next->next;
        delete temp;
        cout << "✓ Deleted " << value << "\n";
    }
}

// 4. Show list
void display(Node* head) {
    if (head == NULL) {
        cout << "List is empty!\n";
        return;
    }
    
    cout << "List: ";
    Node* temp = head;
    while (temp != NULL) {
        cout << temp->data;
        if (temp->next != NULL) cout << " → ";
        temp = temp->next;
    }
    cout << " → NULL\n";
}

// 5. Free all memory
void freeList(Node*& head) {
    Node* current = head;
    while (current != NULL) {
        Node* next = current->next;
        delete current;
        current = next;
    }
    head = NULL;
}


Q Create a BankAccount class.

Initialize account number and balance using a constructor.

Display a message when the destructor is called.

Create objects inside a function to observe destructor behavior.

// #include <iostream>
using namespace std;

class BankAccount {
private:
    int accountNumber;
    double balance;

public:
    // Constructor (initialize using user input values)
    BankAccount(int accNo, double bal) {
        accountNumber = accNo;
        balance = bal;
        cout << "Account Created! Account Number: " << accountNumber << endl;
    }

    // Destructor
    ~BankAccount() {
        cout << "Account Destroyed! Account Number: " << accountNumber << endl;
    }

    // Display function
    void display() {
        cout << "Account Number: " << accountNumber << endl;
        cout << "Balance: " << balance << endl;
    }
};

// Function to create objects using user input
void createAccounts() {
    int accNo;
    double bal;

    cout << "Enter Account Number: ";
    cin >> accNo;

    cout << "Enter Balance: ";
    cin >> bal;

    BankAccount acc1(accNo, bal);

    cout << "\nAccount Details:\n";
    acc1.display();

    // Destructor will run when function ends
}

int main() {
    cout << "Program Started\n\n";

    createAccounts();

    cout << "\nBack in main() function\n";

    return 0;
}


recreate an Employee class.

Make salary private.

Provide getter and setter functions.

Add validation: salary cannot be negative


#include <iostream>
using namespace std;

class Employee {
private:
    double salary;   // Private data member

public:
    string name;

    // Setter function with validation
    void setSalary(double s) {
        if (s >= 0) {
            salary = s;
        } else {
            cout << "Salary cannot be negative! Setting salary to 0.\n";
            salary = 0;
        }
    }

    // Getter function
    double getSalary() {
        return salary;
    }
};

int main() {
    Employee emp;

    cout << "Enter Employee Name: ";
    cin >> emp.name;

    double sal;
    cout << "Enter Salary: ";
    cin >> sal;

    emp.setSalary(sal);   // Set salary using setter

    cout << "\nEmployee Details:\n";
    cout << "Name: " << emp.name << endl;
    cout << "Salary: " << emp.getSalary() << endl;   // Get salary using getter

    return 0;
}


Q Create a class Calculator

Overload a function add() for: int double three parameters

#include <iostream>
using namespace std;

#include <iostream>
using namespace std;

class Calculator {
public:
    // Add two integers
    int add(int a, int b) {
        return a + b;
    }

    // Add two double numbers
    double add(double a, double b) {
        return a + b;
    }

    // Add three integers
    int add(int a, int b, int c) {
        return a + b + c;
    }
};

int main() {
    Calculator calc;

    int a, b, c;
    double x, y;

    // Input for two integers
    cout << "Enter two integers: ";
    cin >> a >> b;
    cout << "Sum (int): " << calc.add(a, b) << endl;

    // Input for two doubles
    cout << "\nEnter two decimal numbers: ";
    cin >> x >> y;
    cout << "Sum (double): " << calc.add(x, y) << endl;

    // Input for three integers
    cout << "\nEnter three integers: ";
    cin >> a >> b >> c;
    cout << "Sum (three integers): " << calc.add(a, b, c) << endl;

    return 0;
}

Create a struct Subject { string name; int marks; }. Create a class Student with: private: int roll; string name; Subject* subjects; int n; constructor allocates dynamic memory for n subjects member functions: input(), display(), total(), grade() make it user define and simple

#include <iostream>
using namespace std;

// Structure
struct Subject {
    string name;
    int marks;
};

class Student {
private:
    int roll;
    string name;
    Subject* subjects;
    int n;

public:
    // Constructor
    Student(int num = 0) {
        n = num;
        if (n > 0)
            subjects = new Subject[n];
        else
            subjects = NULL;
    }

    // Destructor
    ~Student() {
        delete[] subjects;
    }

    void input() {
        cout << "\nEnter Roll Number: ";
        cin >> roll;

        cout << "Enter Name: ";
        cin >> name;

        for (int i = 0; i < n; i++) {
            cout << "Enter Subject " << i + 1 << " Name: ";
            cin >> subjects[i].name;

            cout << "Enter Marks: ";
            cin >> subjects[i].marks;
        }
    }

    void display() {
        cout << "\nRoll: " << roll << endl;
        cout << "Name: " << name << endl;

        for (int i = 0; i < n; i++) {
            cout << subjects[i].name << " : " << subjects[i].marks << endl;
        }

        cout << "Total Marks: " << total() << endl;
    }

    int total() {
        int sum = 0;
        for (int i = 0; i < n; i++) {
            sum += subjects[i].marks;
        }
        return sum;
    }

    void grade() {
        float avg = total() / (float)n;

        if (avg >= 90)
            cout << "Grade: A\n";
        else if (avg >= 75)
            cout << "Grade: B\n";
        else if (avg >= 50)
            cout << "Grade: C\n";
        else
            cout << "Grade: Fail\n";
    }
};

int main() {
    int students, subjects;

    cout << "Enter number of students: ";
    cin >> students;

    cout << "Enter number of subjects: ";
    cin >> subjects;

    // Pointer to object array
    Student* s = new Student[students];

    // Re-assign each object with correct subject count
    for (int i = 0; i < students; i++) {
        s[i] = Student(subjects);
        s[i].input();
    }

    // Find Topper
    int maxTotal = 0;
    int topperIndex = 0;

    for (int i = 0; i < students; i++) {
        if (s[i].total() > maxTotal) {
            maxTotal = s[i].total();
            topperIndex = i;
        }
    }

    cout << "\n===== Student Details =====\n";
    for (int i = 0; i < students; i++) {
        s[i].display();
        s[i].grade();
        cout << "----------------------\n";
    }

    cout << "\n===== Topper =====\n";
    s[topperIndex].display();
    s[topperIndex].grade();

    // Free memory
    delete[] s;

    return 0;
}
Create a struct Node containing:

Patient data (id, name, severity)

Node* next

Create a class PatientQueue implementing:

enqueue (based on severity priority)

dequeue

display
Use dynamic memory (new/delete) and demonstrate queue operations.

#include <iostream>
#include <string>
using namespace std;

// Structure for Patient
struct Patient {
    int id;
    string name;
    int severity; // Higher number = higher priority
};

// Node structure
struct Node {
    Patient data;
    Node* next;
};

class PatientQueue {
private:
    Node* front; // Pointer to front of queue

public:
    // Constructor
    PatientQueue() {
        front = nullptr;
    }

    // Enqueue based on severity
    void enqueue() {
        Patient p;
        cout << "\nEnter Patient ID: ";
        cin >> p.id;
        cout << "Enter Patient Name: ";
        cin >> p.name;
        cout << "Enter Severity (higher number = more severe): ";
        cin >> p.severity;

        Node* newNode = new Node;
        newNode->data = p;
        newNode->next = nullptr;

        // Insert at front if queue empty or highest severity
        if (front == nullptr || p.severity > front->data.severity) {
            newNode->next = front;
            front = newNode;
        } else {
            // Find proper position
            Node* temp = front;
            while (temp->next != nullptr && temp->next->data.severity >= p.severity) {
                temp = temp->next;
            }
            newNode->next = temp->next;
            temp->next = newNode;
        }

        cout << "Patient added to queue.\n";
    }

    // Dequeue: remove patient with highest severity
    void dequeue() {
        if (front == nullptr) {
            cout << "Queue is empty.\n";
            return;
        }

        Node* temp = front;
        front = front->next;

        cout << "\nDequeued Patient:\n";
        cout << "ID: " << temp->data.id << endl;
        cout << "Name: " << temp->data.name << endl;
        cout << "Severity: " << temp->data.severity << endl;

        delete temp; // Free memory
    }

    // Display queue
    void display() {
        if (front == nullptr) {
            cout << "Queue is empty.\n";
            return;
        }

        cout << "\nPatients in Queue (High to Low Severity):\n";
        Node* temp = front;
        while (temp != nullptr) {
            cout << "ID: " << temp->data.id
                 << ", Name: " << temp->data.name
                 << ", Severity: " << temp->data.severity << endl;
            temp = temp->next;
        }
    }

    // Destructor: free all nodes
    ~PatientQueue() {
        while (front != nullptr) {
            Node* temp = front;
            front = front->next;
            delete temp;
        }
    }
};

int main() {
    PatientQueue pq;
    int choice;

    do {
        cout << "\n1. Add Patient (Enqueue)\n";
        cout << "2. Serve Patient (Dequeue)\n";
        cout << "3. Display Queue\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                pq.enqueue();
                break;
            case 2:
                pq.dequeue();
                break;
            case 3:
                pq.display();
                break;
            case 4:
                cout << "Exiting...\n";
                break;
            default:
                cout << "Invalid choice!\n";
        }
    } while (choice != 4);

    return 0;
}
Create a struct BookNode:

int id; string title; string author; bool issued;

BookNode* next

Create a class Library with:

BookNode* head addBook(), issueBook(id), returnBook(id), searchBook(title), displayAll() Use pointers to traverse linked list and manage memory safely.

#include <iostream>
#include <string>
using namespace std;

// Structure for Book
struct BookNode {
    int id;
    string title;
    string author;
    bool issued;
    BookNode* next;
};

// Library class
class Library {
private:
    BookNode* head;

public:
    // Constructor
    Library() {
        head = nullptr;
    }

    // Add a book
    void addBook() {
        BookNode* newBook = new BookNode;

        cout << "\nEnter Book ID: ";
        cin >> newBook->id;
        cin.ignore(); // To ignore leftover newline
        cout << "Enter Book Title: ";
        getline(cin, newBook->title);
        cout << "Enter Author Name: ";
        getline(cin, newBook->author);
        newBook->issued = false;
        newBook->next = nullptr;

        if (head == nullptr) {
            head = newBook;
        } else {
            BookNode* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newBook;
        }

        cout << "Book added successfully.\n";
    }

    // Issue a book by ID
    void issueBook(int id) {
        BookNode* temp = head;
        while (temp != nullptr) {
            if (temp->id == id) {
                if (!temp->issued) {
                    temp->issued = true;
                    cout << "Book issued successfully.\n";
                } else {
                    cout << "Book is already issued.\n";
                }
                return;
            }
            temp = temp->next;
        }
        cout << "Book not found.\n";
    }

    // Return a book by ID
    void returnBook(int id) {
        BookNode* temp = head;
        while (temp != nullptr) {
            if (temp->id == id) {
                if (temp->issued) {
                    temp->issued = false;
                    cout << "Book returned successfully.\n";
                } else {
                    cout << "Book was not issued.\n";
                }
                return;
            }
            temp = temp->next;
        }
        cout << "Book not found.\n";
    }

    // Search book by title
    void searchBook(const string& title) {
        BookNode* temp = head;
        while (temp != nullptr) {
            if (temp->title == title) {
                cout << "\nBook Found:\n";
                cout << "ID: " << temp->id << endl;
                cout << "Title: " << temp->title << endl;
                cout << "Author: " << temp->author << endl;
                cout << "Status: " << (temp->issued ? "Issued" : "Available") << endl;
                return;
            }
            temp = temp->next;
        }
        cout << "Book not found.\n";
    }

    // Display all books
    void displayAll() {
        if (head == nullptr) {
            cout << "No books in library.\n";
            return;
        }

        BookNode* temp = head;
        cout << "\nLibrary Books:\n";
        while (temp != nullptr) {
            cout << "ID: " << temp->id
                 << ", Title: " << temp->title
                 << ", Author: " << temp->author
                 << ", Status: " << (temp->issued ? "Issued" : "Available




Create a struct Transaction:

string type; double amount; string date; Transaction* next

Create a class BankAccount:

private: accountNo, holderName, balance, Transaction* historyHead

deposit(), withdraw(), showHistory(), showBalance() Store multiple accounts using BankAccount* array pointer and search account by number.

#include <iostream>
#include <string>
using namespace std;

// Structure for Transaction
struct Transaction {
    string type;       // Deposit or Withdraw
    double amount;
    string date;
    Transaction* next;
};

// BankAccount class
class BankAccount {
private:
    int accountNo;
    string holderName;
    double balance;
    Transaction* historyHead;

public:
    // Constructor
    BankAccount() {
        balance = 0;
        historyHead = nullptr;
    }

    // Initialize account
    void initAccount() {
        cout << "Enter Account Number: ";
        cin >> accountNo;
        cin.ignore();
        cout << "Enter Holder Name: ";
        getline(cin, holderName);
    }

    // Deposit
    void deposit() {
        double amt;
        string date;
        cout << "Enter amount to deposit: ";
        cin >> amt;
        cin.ignore();
        cout << "Enter date (dd/mm/yyyy): ";
        getline(cin, date);

        balance += amt;

        // Add transaction to history
        Transaction* t = new Transaction;
        t->type = "Deposit";
        t->amount = amt;
        t->date = date;
        t->next = nullptr;

        if (historyHead == nullptr)
            historyHead = t;
        else {
            Transaction* temp = historyHead;
            while (temp->next != nullptr)
                temp = temp->next;
            temp->next = t;
        }

        cout << "Deposit successful!\n";
    }

    // Withdraw
    void withdraw() {
        double amt;
        string date;
        cout << "Enter amount to withdraw: ";
        cin >> amt;
        cin.ignore();
        if (amt > balance) {
            cout << "Insufficient balance!\n";
            return;
        }
        cout << "Enter date (dd/mm/yyyy): ";
        getline(cin, date);

        balance -= amt;

        // Add transaction to history
        Transaction* t = new Transaction;
        t->type = "Withdraw";
        t->amount = amt;
        t->date = date;
        t->next = nullptr;

        if (historyHead == nullptr)
            historyHead = t;
        else {
            Transaction* temp = historyHead;
            while (temp->next != nullptr)
                temp = temp->next;
            temp->next = t;
        }

        cout << "Withdrawal successful!\n";
    }

    // Show balance
    void showBalance() {
        cout << "\nAccount Number: " << accountNo
             << "\nHolder Name: " << holderName
             << "\nBalance: " << balance << endl;
    }

    // Show transaction history
    void showHistory() {
        if (historyHead == nullptr) {
            cout << "No transactions yet.\n";
            return;
        }

        cout << "\nTransaction History:\n";
        Transaction* temp = historyHead;
        while (temp != nullptr) {
            cout << temp->date << " : " << temp->type
                 << " " << temp->amount << endl;
            temp = temp->next;
        }
    }

    // Get account number
    int getAccountNo() {
        return accountNo;
    }

    // Destructor to free transactions
    ~BankAccount() {
        while (historyHead != nullptr) {
            Transaction* temp = historyHead;
            historyHead = historyHead->next;
            delete temp;
        }
    }
};

// Main function
int main() {
    int n;
    cout << "Enter number of accounts: ";
    cin >> n;

    BankAccount* accounts = new BankAccount[n];

    // Initialize accounts
    for (int i = 0; i < n; i++) {
        cout << "\nEnter details for Account " << i + 1 << ":\n";
        accounts[i].initAccount();
    }

    int choice, accNo;
    do {
        cout << "\n===== Bank Menu =====\n";
        cout << "1. Deposit\n2. Withdraw\n3. Show Balance\n4. Show History\n5. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        if (choice >= 1 && choice <= 4) {
            cout << "Enter Account Number: ";
            cin >> accNo;

            // Search account
            BankAccount* acc = nullptr;
            for (int i = 0; i < n; i++) {
                if (accounts[i].getAccountNo() == accNo) {
                    acc = &accounts[i];
                    break;
                }
            }

            if (acc == nullptr) {
                cout << "Account not found!\n";
                continue;
            }

            switch (choice) {
                case 1: acc->deposit(); break;
                case 2: acc->withdraw(); break;
                case 3: acc->showBalance(); break;
                case 4: acc->showHistory(); break;
            }
        }
    } while (choice != 5);

    delete[] accounts; // Free memory for accounts
    cout << "Exiting program...\n";

    return 0;
}


recreate a struct Course:

courseCode, courseName, credits

Create a class Student:

roll, name Course* registeredCourses (dynamic) registerCourses(), dropCourse(code), showCourses(), totalCredits() Store multiple students using pointers and print list of students registered in a given course.

#include <iostream>
#include <string>
using namespace std;

// Structure for Course
struct Course {
    string courseCode;
    string courseName;
    int credits;
};

// Student class
class Student {
private:
    int roll;
    string name;
    Course* registeredCourses; // Dynamic array
    int n;                     // Number of registered courses

public:
    // Constructor
    Student(int maxCourses = 0) {
        n = maxCourses;
        if (n > 0)
            registeredCourses = new Course[n];
        else
            registeredCourses = nullptr;
    }

    // Destructor
    ~Student() {
        delete[] registeredCourses;
    }

    // Initialize student details
    void inputDetails() {
        cout << "Enter Roll Number: ";
        cin >> roll;
        cin.ignore();
        cout << "Enter Name: ";
        getline(cin, name);
    }

    // Register courses (user-defined)
    void registerCourses() {
        for (int i = 0; i < n; i++) {
            cout << "\nEnter Course " << i + 1 << " Code: ";
            cin >> registeredCourses[i].courseCode;
            cin.ignore();
            cout << "Enter Course Name: ";
            getline(cin, registeredCourses[i].courseName);
            cout << "Enter Credits: ";
            cin >> registeredCourses[i].credits;
        }
    }

    // Drop a course by code
    void dropCourse(const string& code) {
        bool found = false;
        for (int i = 0; i < n; i++) {
            if (registeredCourses[i].courseCode == code) {
                found = true;
                // Shift remaining courses
                for (int j = i; j < n - 1; j++)
                    registeredCourses[j] = registeredCourses[j + 1];
                n--;
                cout << "Course " << code << " dropped.\n";
                break;
            }
        }
        if (!found) cout << "Course not found.\n";
    }

    // Show all registered courses
    void showCourses() {
        cout << "\nCourses for " << name << " (Roll: " << roll << "):\n";
        if (n == 0) {
            cout << "No courses registered.\n";
            return;
        }
        for (int i = 0; i < n; i++) {
            cout << registeredCourses[i].courseCode << " - "
                 << registeredCourses[i].courseName
                 << " (" << registeredCourses[i].credits << " credits)\n";
        }
    }

    // Calculate total credits
    int totalCredits() {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += registeredCourses[i].credits;
        return sum;
    }

    // Get roll number
    int getRoll() {
        return roll;
    }

    // Check if registered in a course
    bool isRegisteredIn(const string& code) {
        for (int i = 0; i < n; i++)
            if (registeredCourses[i].courseCode == code)
                return true;
        return false;
    }

    // Get name
    string getName() {
        return name;
    }
};

int main() {
    int numStudents, numCourses;
    cout << "Enter number of students: ";
    cin >> numStudents;
    cout << "Enter max number of courses per student: ";
    cin >> numCourses;

    // Array of student pointers
    Student** students = new Student*[numStudents];

    // Input student details and courses
    for (int i = 0; i < numStudents; i++) {
        cout << "\nEnter details for Student " << i + 1 << ":\n";
        students[i] = new Student(numCourses);
        students[i]->inputDetails();
        students[i]->registerCourses();
    }

    // Display all students and courses
    cout << "\n===== All Students and Courses =====\n";
    for (int i = 0; i < numStudents; i++) {
        students[i]->showCourses();
        cout << "Total Credits: " << students[i]->totalCredits() << "\n";
    }

    // Show students registered in a given course
    string searchCode;
    cout << "\nEnter course code to find registered students: ";
    cin >> searchCode;
    cout << "\nStudents registered in " << searchCode << ":\n";
    bool found = false;
    for (int i = 0; i < numStudents; i++) {
        if (students[i]->isRegisteredIn(searchCode)) {
            cout << students[i]->getName() << " (Roll: " << students[i]->getRoll() << ")\n";
            found = true;
        }
    }
    if (!found) cout << "No student registered in this course.\n";

    // Free memory
    for (int i = 0; i < numStudents; i++)
        delete students[i];
    delete[] students;

    return 0;
}


Create a struct DirNode:

string name; bool isFile;

DirNode* child; DirNode* sibling;

Create a class DirectoryTree:

createFolder(path), createFile(path)

list(path) deleteNode(path)
Implement using pointers (tree navigation) and free memory in destructor.



#include <iostream>
#include <string>
#include <sstream>
using namespace std;

// Structure for directory node
struct DirNode {
    string name;
    bool isFile;
    DirNode* child;
    DirNode* sibling;
};

// DirectoryTree class
class DirectoryTree {
private:
    DirNode* root;

    // Helper: Split path by '/'
    void splitPath(const string& path, string parts[], int& count) {
        stringstream ss(path);
        string token;
        count = 0;
        while (getline(ss, token, '/')) {
            if (!token.empty())
                parts[count++] = token;
        }
    }

    // Helper: Find node by path
    DirNode* navigate(const string& path) {
        if (path == "/") return root;

        string parts[100];
        int n;
        splitPath(path, parts, n);

        DirNode* curr = root->child;
        for (int i = 0; i < n; i++) {
            DirNode* temp = curr;
            while (temp != nullptr && temp->name != parts[i])
                temp = temp->sibling;
            if (temp == nullptr) return nullptr;
            curr = temp->child;
            if (i == n - 1) return temp;
        }
        return nullptr;
    }

    // Helper: Free memory recursively
    void deleteTree(DirNode* node) {
        if (node == nullptr) return;
        deleteTree(node->child);
        deleteTree(node->sibling);
        delete node;
    }

public:
    // Constructor
    DirectoryTree() {
        root = new DirNode;
        root->name = "/";
        root->isFile = false;
        root->child = nullptr;
        root->sibling = nullptr;
    }

    // Destructor
    ~DirectoryTree() {
        deleteTree(root);
    }

    // Create folder
    void createFolder(const string& path) {
        string parts[100];
        int n;
        splitPath(path, parts, n);

        DirNode* curr = root;
        for (int i = 0; i < n; i++) {
            DirNode* prev = nullptr;
            DirNode* temp = curr->child;

            // Check if folder/file exists
            while (temp != nullptr && temp->name != parts[i]) {
                prev = temp;
                temp = temp->sibling;
            }

            if (temp == nullptr) {
                // Create new folder
                DirNode* newNode = new DirNode;
                newNode->name = parts[i];
                newNode->isFile = false;
                newNode->child = nullptr;
                newNode->sibling = nullptr;

                if (prev == nullptr) curr->child = newNode;
                else prev->sibling = newNode;

                curr = newNode;
            } else {
                curr = temp; // Folder exists, move inside
            }
        }
        cout << "Folder created: " << path << endl;
    }

    // Create file
    void createFile(const string& path) {
        string parts[100];
        int n;
        splitPath(path, parts, n);

        DirNode* curr = root;
        for (int i = 0; i < n - 1; i++) {
            DirNode* temp = curr->child;
            while (temp != nullptr && temp->name != parts[i])
                temp = temp->sibling;
            if (temp == nullptr) {
                cout << "Invalid path! Folder does not exist: " << parts[i] << endl;
                return;
            }
            curr = temp;
        }

        // Add file as child of last folder
        DirNode* newNode = new DirNode;
        newNode->name = parts[n - 1];
        newNode->isFile = true;
        newNode->child = nullptr;
        newNode->sibling = nullptr;

        if (curr->child == nullptr) curr->child = newNode;
        else {
            DirNode* temp = curr->child;
            while (temp->sibling != nullptr) temp = temp->sibling;
            temp->sibling = newNode;
        }

        cout << "File created: " << path << endl;
    }

    // List contents of a path
    void list(const string& path) {
        DirNode* node = navigate(path);
        if (node == nullptr) {
            cout << "Path not found!\n";
            return;
        }
        if (node->child == nullptr) {
            cout << "Empty folder.\n";
            return;
        }

        cout << "Contents of " << path << ":\n";
        DirNode* temp = node->child;
        while (temp != nullptr) {
            cout << (temp->isFile ? "File: " : "Folder: ") << temp->name << endl;
            temp = temp->sibling;
        }
    }

    // Delete node by path
    void deleteNode(const string& path) {
        if (path == "/") {
            cout << "Cannot delete root!\n";
            return;
        }

        string parts[100];
        int n;
        splitPath(path, parts, n);

        DirNode* curr = root;
        DirNode* prev = nullptr;
        DirNode* temp = root->child;

        for (int i = 0; i < n; i++) {
            prev = curr;
            DirNode* prevSibling = nullptr;
            temp = curr->child;

            while (temp != nullptr && temp->name != parts[i]) {
                prevSibling = temp;
                temp = temp->sibling;
            }

            if (temp == nullptr) {
                cout << "Path n



