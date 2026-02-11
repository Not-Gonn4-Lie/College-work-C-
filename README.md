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

