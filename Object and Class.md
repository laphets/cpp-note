## Design principle
Only public function can access internal variable. For private(default is private), we can implement them inside the class. For public method, it's recommanded to implement them outside the function.

For example, if we have defined a function prototype inside the public sector, we can implement is as:
```c++
void Stock::acquire() {
  // Your implement here
}
```
Using the scope-resolution operator (`::`) to indicate to which class the function belongs. Out of class, we need use *qualified name* `Stock::acquire()`, inside class scope, we just use *abbreviation* name `acquire()`.

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

## Constructor
A constructor has no declared type (nor `void`)
We can have an example

To avoid same name for member and constructor arguments, we have two practical ways:
- Adding a `m_prefix`
- Using a underbar suffix for member name, such as `name_`

If we have define our own constructor to get rid of the default, so we also need to revise the default declaration. Otherwise, it may occur error.

```c++
class Player{
private:
    std::string name;
    int age;
public:
    Player(const std::string& n, int age);
};

Player::Player(const std::string &n, int age) {
    name = n;
    this->age = age;
}

int main() {
    // Two ways for using constructor
    Player p0 = Player("Laphets", 19);
    // or
    Player p1("Laphets", 19);
    // or using new
    Player* p2 = new Player("Laphets", 19);

}
```

If we just want to using default and give it `0` value, we can have
```c++
Player::Player() {
  name =  "";
  age = 0;
}
```

> When you design a class, you should usually provide a default constructor that implicitly initializes all class members.
That means we need provide default and our own constructor (which has arguments).


When you implicitly call the default constructor, you don’t use parentheses.
```c++
Player* p = Player;
Player* p = new Player("Laphets");
Player p;
Player p("Laphets");
Player p = "Laphets"; // If only one argument
```

### Optional initializer list
(preceded by a colon)
```c++
Player::Player(int arg, int second) : one(arg), two(second);
```


### Copy Constructor
Accept one argument of the another object reference.
```c++
Player::Player(Player& p);

Player a = b;
Player a(b);
```


## Destructor
```c++
class Player{
private:
    std::string name;
    int age;
public:
    Player(const std::string& n, int age);
    ~Player();
};

Player::Player(const std::string &n, int age) {
    name = n;
    this->age = age;
}

Player::~Player() {
    printf("Destructor~");
}
```
Preceded by a tilde `~`.

### When the destructor will be called?
- If it's an automatic storage class object, the detructor is called when exit that block.
- If it's created by new, which resides in heap memory, it's called when calling delete.


### Object assign
> When you assign one object to another of the same class, by default C++ copies the contents of each data member of the source object to the corresponding data member of the target object.

## `const` member function
It's used for function to promise that not to midify the invoking object.
In C++, we can place the `const` keyword after the function parentheses.
```c++
void Player::show() const;
```
Function defined this way is called `const` member function.

## `this` pointer
Try to explain which of each `const` is used for.
```c++
const Stock & topval(const Stock & s) const;
```

> Each member function, including constructors and destructors, has a this pointer. The special property of the this pointer is that it points to the invoking object. If a method needs to refer to the invoking object as a whole, it can use the expression *this. Using the const qualifier after the function argument parentheses qualifies this as being a pointer to const; in that case, you can’t use this to change the object’s value.

So `this` is a pointer to the object itself, to get the object, we have to use `*this`.

## Array of objects
```c++
Player player_list[10];
```
This declaration requires either that the class explicitly define no constructors at all, in which case the implicit do-nothing default constructor is used, or, as in this case, that an explicit default constructor be defined.

## Class Scope
```c++
static const int a = 1;
```