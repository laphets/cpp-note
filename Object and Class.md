## Design principle
Only public function can access internal variable. For private(default is private), we can implement them inside the class. For public method, it's recommanded to implement them outside the function.

For example, if we have defined a function prototype inside the public sector, we can implement is as:
```c++
void Stock::acquire() {
  // Your implement here
}
```
Using the scope-resolution operator (`::`) to indicate to which class the function belongs. Out of class, we need use *qualified name* `Stock::acquire()`, inside class scope, wo just use *abbreviation* name `acquire()`.

Also, the method can access private data members.

Any function with a definition in the class declaration automatically becomes an inline function.

## How to create object
```c++
Stock kate, joe;
```

## A typical class declaration
```c++
class className { 
private:
  data member declarations 
public:
  member function prototypes 
};
```