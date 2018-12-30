## reference
```c++
int rats;
int& r = rats;  // make r an ali
```

`int&` means reference to int, it serves as part of the type identifier.
And in this case, `rats` and `r` refer to the same value and same memory location. (Kind of making difference on symbol table?)

Also, it necessary to initialize the reference when declare it.

The reference relation will not change by assign other value.

### reference as funtion parameter
or we call it `passing by reference`, diff from `passing by value`. One variable, two names.
If you want to pass by reference, and do not modify the variable unintendedly, you can use `const int& a`.

Also, do not do like this:
```c++
int foo(int& a) {
  return a;
}
int main() {
  int a = 1;
  foo(a+2);   // wrong
}
```



### Temporary variable
**An argument that’s an lvalue is a data object that can be referenced by address.**
Both regular and constant variable can be considered as lvalue. (Although constant variable can't be modified)

For `rvalue`, such as common return value of function, or some expression like `1+1` and `x+y`, they resides in a temporary memory location that doesn't necessarily persist even until next statement. Also for array `a[10]` for example, a is also not a `lvalue`, since you can't try to access its memory location(it's stored in symbol table), neither can modify the store value of them.

> Note: If a function call argument isn’t an lvalue or does not match the type of the corresponding const reference parameter, C++ creates an anonymous variable of the correct type, assigns the value of the function call argument to the anonymous variable, and has the parameter refer to that variable.

We can have an example:
```c++
const int& w(const int&a) {
    return a;
}

int main() {
    long b = 1;
    w(b);
    w(b + 2);
}
```
In this case, since it's argument is defined as const, so although the call argument isn't a lvalue nor a matching type, the C++ will create an anonymous variable assign to the argument.


Assigning a value to a function call—works because the return value is a reference.
```c++
int& test(int& a) {
    return a;
}

int main() {

    int a = 1;
    test(a) = 2;

    return 0;
}
```

### Constant for reference return
In last example, we found that we can modify the return reference by `test(a) = 2`, but that may occur some problem, therefore, if we do not want the return reference be modified, we can use `const int&` instead.

> Making the return type a const reference therefore protects you from the temptation of obfuscation

Let's see an example
```c++
int a = 1;
const auto& b = a;
a = 2;
b = 2;  // wrong
```

### Using reference with a class object
The usual c++ practice for passing class object to a function is using reference.

For example, we have
```c++
string combine(const string& a, const string& b) {
  return a + b;
}

string another_combine(string a, string b) {
  return a + b;
}
```
The second way will copy all the data into the stack, which is not efficient.


### Why do we need reference?
- Allow you to alter a data object calling by function
- When in C++ class, passing by reference can speed up, instead of passing an entire date object.

### Some guidelines:
A function uses passed data without modifying it:
- If the data object is small, such as a built-in data type or a small structure, pass it by value.
- If the data object is an array, use a pointer because that’s your only choice. Make the pointer a pointer to const.
- If the data object is a good-sized structure, use a const pointer or a const reference to increase program efficiency.You save the time and space needed to copy a structure or a class design. Make the pointer or reference const.
- If the data object is a class object, use a const reference.The semantics of class design often require using a reference, which is the main reason C++ added this feature.Thus, the standard way to pass class object arguments is by reference.

A function modifies data in the calling function:
- If the data object is a built-in data type, use a pointer. If you spot code like fixit(&x), where x is an int, it’s pretty clear that this function intends to modify x.
- If the data object is an array, use your only choice: a pointer.
- If the data object is a structure, use a reference or a pointer.
- If the data object is a class object, use a reference.

In conclusion, if the data is a class object, just passing by reference. If it's a small type, using pointer to clearify that the function may change the value of the variable. If the data is array, you must use pointer. If it's a structure, both pointer and reference will be OK.