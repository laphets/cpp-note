## Declaration of function
```c++
// function prototype
double pam(int);

// fucntion declaration
double (*pf)(int);  // pf points to a function which takes int argument and returns a double
```

> one tip is that, we can write a prototype of a function, and replace the name with a pointer

**And we may need to add parentheses**
```c++
double (*pf)(int);

double* pf(int);  // returns a pointer to double
```

### To invoke a function
```c++
// Two ways
(*pf)(1);


// or
pf(1)
```
Holy syntax!

There comes a sample
```c++
double first(double arg);
double second(double arg);

void estimate(double (*pf)(double a));

int main() {

    estimate(first);
    estimate(second);
    return 0;
}

double first(double a) {
    printf("First %lf\n", a);
    return 0;
}

double second(double a) {
    printf("Second %lf\n", a);
    return 0;
}
void estimate(double (*pf)(double)) {
    (*pf)(1);
}
```

In c++11, we have
```c++
int a(int);

int main() {
  auto b = a;
}
```

### Using typedef
```c++
typedef const double *(*p_fun)(const double *, int); 
p_fun p1 = f1; // p1 points to the f1() function
```