#include <iostream>
#include <cstring>
using namespace std;

class Student {
private:
    char *name; // heap memory for name
    int age;

public:
    // Default Constructor
    Student() {
        name = new char[8];
        strcpy(name, "Unknown");
        age = 0;
        cout << "Default Constructor called" << endl;
    }

    // Parameterized Constructor
    Student(const char *n, int a) {
        name = new char[strlen(n) + 1];
        strcpy(name, n);
        age = a;
        cout << "Parameterized Constructor called" << endl;
    }

    // Deep Copy Constructor
    Student(const Student &s) {
        name = new char[strlen(s.name) + 1];
        strcpy(name, s.name);
        age = s.age;
        cout << "Copy Constructor (Deep Copy) called" << endl;
    }

    // Setter functions
    void setName(const char *n) {
        delete[] name; // free old memory before assigning new
        name = new char[strlen(n) + 1];
        strcpy(name, n);
    }
    void setAge(int a) {
        age = a;
    }

    // Getter functions
    const char* getName() const { // const means no modification
        return name;
    }
    int getAge() const {
        return age;
    }

    // Display function
    void display() const { // const method
        cout << "Name: " << name << ", Age: " << age << endl;
    }

    // Destructor
    ~Student() {
        delete[] name;
        cout << "Destructor called for " << name << endl;
    }
};

int main() {
    // Default Constructor
    Student s1;
    s1.display();

    // Parameterized Constructor
    Student s2("Aliza", 18);
    s2.display();

    // Copy Constructor (Deep Copy)
    Student s3 = s2;
    s3.display();

    // Change s3 data (won’t affect s2 due to deep copy)
    s3.setName("Ayesha");
    s3.setAge(20);

    cout << "\nAfter changing s3:" << endl;
    s2.display();
    s3.display();

    // Heap Pointer Object
    Student *ptr = new Student("Hina", 19);
    ptr->display();
    delete ptr; // free heap memory

    return 0;
}

    
