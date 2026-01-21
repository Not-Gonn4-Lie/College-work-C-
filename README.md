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
