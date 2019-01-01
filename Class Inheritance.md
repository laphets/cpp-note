## Constructor
For the derived class, it doesn't have access to the base class's private members, so it need use some public method to help access them.

When a program constructs a derived-class object, it first constructs the base-class object. Conceptually, that means **the base-class object should be constructed before the program enters the body of the derived-class constructor**. C++ uses the member initializer list syntax to accomplish this.

For example:
```c++
RatedPlayer::RatedPlayer (unsigned int r, const string & fn, const string & ln, bool ht) : TableTennisPlayer(fn, ln, ht) {
  rating = r; 
}
```
Here, `TableTennisPlayer(fn, ln, ht)` is the member initializer list. And should be called before `RatedPlayer`'s constructor.
If you miss the list initializer, it will call the **default constructor** for the base class.

### Copy constructor
Accept one argument `const MyClass& t` a reference.
And the compiler will also generate a default copy constructor.

### Key Points
These are the key points about constructors for derived classes:
- The **base-class** object is **constructed first**.
- The derived-class constructor should pass base-class information to a base-class constructor via a **member initializer list**.
- The derived-class constructor should initialize the data members that were added to the derived class.

## Destructor
Destroying an object occurs in the opposite order used to construct an object.That is, the body of the derived-class destructor is executed first, and then the base-class destructor is called automatically.

> A program first calls the base-class constructor and then calls the derived-class constructor. The base-class constructor is responsible for initializing the inherited data members. The derived-class constructor is responsible for initializing any added data members.


## Relationship between derived and base class
- a derived-class can use base-class's method which is not private
- a base-class pointer can point to a derived-class object without an explicit type cast (since a derived-class contains members of the base-class, but the opposite is not true) **Just in one direction, use base pointer to derived object**.
```c++
Base-class* p = &derived-obj  // OK
Derived-class* q = &base-obj  // Wrong, the base class may not have member of the derived class
```
  But in default, the base class pointer or reference can only invoke just base-class methods.
  
  Let's see another example:
```c++
Derived-class d1(...);
Base-class d2(d1);
```
  Why this is acceptable? Since we know that for base-class, it has a default copy constructor, which accept a reference of `Base-class&`, but when we pass d1(`Derived-class`) into it, it's translated into `Base-class`, which can be explained.
  
  Therefore, you can assign a `Base-class` with a `Derived-class` object;
```c++
Base-class d2 = d1;   // same as calling implicit copy constructor
```
  
- a base-class reference can refer to a derived-class object without an explicit type cast