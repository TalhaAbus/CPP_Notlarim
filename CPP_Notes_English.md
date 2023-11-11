# Some Definitions in C++ Language

### Undefined Behaviour
- It may be correct according to the language rules, but there is no guarantee about what the situation will be like when compiled and run.
### Unspecfied Behaviour
- A behaviour that is not specified in the standards, or even if specified, can result in more than one outcome. The compiler can generate code in any way.
### Implementation Defined
- This is also unspecified behaviour, but the compiler is required to document it. A behaviour is defined, but this definition is left to the compiler. The compiler must document it and is required to consistently choose a certain option in generating code.
### User Defined Type
- These are data types that the user can define themselves. The user creates type with a decleration. In addition to basic data types, it can be defined with struct, union, class.
### Internal Linkage
- The state of element (variable, function class) being visible only within certain source file. So, this element can only be accessed by elements in the same source file.
- **In short:** The same name used in different sources belonging to different entities.
- The **static** keyword makes the variable have internal linkage. **Example:**
```CPP
static int x; //internal linkage
```
### Scope LEakage
- If a variable is visibnle outside the area where it is defined, there is a scope leakage.
**Example:**
```CPP
void func()
{
    int i;
    for (i = 0; i < 10; ++i)    
}
```
**Some Differences Between C and C++**
- There is a type conversion from arithmetic types to the bool type, and vice versa. The conversion will be either 1 or 0.
- In C++, Global const objects have internal linkage. (In C, They have external Linkage.)
- In C++, There is no implicit type conversion between adress types and arithmetic types.
- There is no conversion from const t* type to t* type.
- There are also no implicit type conversion between different adress types.

# Lesson 1 Exercises
**Question 1: Is the code valid?**

```CPP
#include <iostream>

int* gp;

int main() {
    int x = 100;
    int* ptr = &x;

    bool b1 = ptr;
}

```
> There is an automatic conversion from adress, pointer types to the bool type.The value of b1 will be true. The conversion to true or false depends on whether the pointer is a null pointer or not. Since gp is zero-initialized, it takes the null pointer value and will convert to false.

**Question 2:**

```CPP
int main() {
    bool flag = true;
    bool is_on = false;

    int *ptr = is_on;
}
```
> There is no conversion from bool type to the pointer type. The code is incorrect. There is a conversion from pointer type to bool type, but not from bool type to pointer type.

**Question 3: Is the Code Valid?**
```CPP
int main() {
    const int x = 10;

    int* p = x;
}
```
> Syntax error. In C++, there is no conversion from const int* type to the int* type. (In C, there is)

**Question 4**
```CPP
int main{
    const int *p;  // Valid. This is not a const object but a pointer in question.
    int *const p;   // Invalid. Const objects must be initialized.
}
```

# Lesson 2

**Notes:**
- In C++, comparison operators produce boolean type values (True, False)
- While the type of character constants is int in C, it is char in C++
- In C, the constant "akif" is an array of type char[5], including the null characterat the end.There is array decay. The same string literal in C++ is of type const char[5]. In c++, when array decay occurs, the resulting adress is not char. It becomes const char*.
- In both languages, attempting to modify a string literal results in undefined behaviour.

## Array to Pointer Conversion
- Except for two exceptions, the array name is converted to the adress of the first element of the array in C.
- The two exceptions are:
> When the operand of the sizeof operator is an array.
> When the operand of the adress operator is an array.

**Example:**
```CPP
int a[10] = {1, 5, 7};
- The type of int a = int[10]
- The type of the address of a = int (*)[10]
- The expression a is converted to the address of the first element of the array via array decay.
- So here a = &a[0]
- In both expressions, the type is int*
```
## Reference Semantics:




























