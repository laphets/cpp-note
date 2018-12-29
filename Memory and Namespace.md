### auto
auto induce type
```c++
auto a = 1
auto it = something.begin()
```

### Header file management
```c++
#ifndef SB_H_
#define SB_H_
...
#endif
```

### Initializing Static Variable
```c++
#include <cmath> 
int x;  // zero-initialization
int y = 5;  // constant-expression initialization
long z = 13 * 13;   // constant-expression initialization
const double pi = 4.0 * atan(1.0); // dynamic initialization
```
For constant initialization, it's initialized when complie.

### ODR P463
one definition rule
There is two kind:
- defining declaration(definition) - containing storage allocate
```c++
double up;
extern int cats = 20;
```
- referencing declaration(declaration) - not contain storage allocate
```c++
extern int cat; // use extern and has no initialization
```

### Access global variable when shadowing
```c++
::warming
```
### Some rule?
You can use an external variable to share data among different parts of a multifile program.You can use a static variable with internal linkage to share data among functions found in just one file.

### cv => const and volatile
volatile: compiler sometimes may use cache between context, so using volatile can specify do not using cache, since a variable may be modified by some hardware routine.

### namespace
*why do we need namespace?*

origional global scope => global namespace

namespace is open which means that we can add names to existing namespace.
(some like redefine?)

Then it comes how to access namespace:
use `::` scope-resolution operator
```c++
Jack::pair = 12.2;
Jill::Hill mole;
Jack::fetch();
```


### using 
- using declaration => A using declaration adds a particular name to the declarative region in which it occurs.
- using derective => make the whole(entire) namespace available

For example:
```c++
namespace Jill {
  double fetch;
}
char fetch;
int main () {
  using Jill::fetch;  // put fetch into local namespace
  cin >> fetch; // read into Jill::fetch
  cin >> ::fetch; // read into global namespace fetch
}
```

a using declaration add the name to the local declaration region
available to its scope

```c++
using namespace std; // make std available in the global scope
```

`using` increases the possibility of name conflicts.