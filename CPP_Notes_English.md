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
- Units formed by constants alone, variables alone, or these with their operators. Every expression has a type and a value category. References in C++:
1. L value reference (Left-hand reference)
2. R value reference (Right-hand reference)
3. Forwarding reference (Universal reference)

**Note:** There is a lot of pointer usage in C. However, pointer usage in C++ is much less compared to C. This is due to the precense of reference semantics to meet the needs of situations where pointers are used. In most scenerios where we use pointers to control the lifetime of dynamically lived objects, we use **smart pointers** classes, which are not present is C but exist in C++.

**Expression:**
```CPP
x
x + 5
f(x)
++X
x++
f(x) > g(x)
x * x + y * y
```

# Value Categories
**In C Language**
- L Value expression
- R Value expression
**C++ value categories:**
- Primary value categories:
- PR Value
- L Value
- X Value (Ex-pired value) related to an object that is about to end its life

**Value Categories Notes:**
- An expression being an L value indicates that it is an object in memory.
- An expression being R value means it's an expression created to calculate the value of an expression, without a permanent place in memory.
- Expressions that can appear ont both the left and right sides of the assignment operator are L value expressions.
- Expressions that can only appear on the right side of the assignment operator (not on the left side) are R value expressions.
- Expressions created by variables (including arrays) are L value expresions.
- L value expressions correspond to an object (Variables)
- PR value and X value combined are called R value.
- L value and X value combined are called GL value.

### Scope Resolution Operator
- The :: operator is used to find and access a name within a namespace.

### Namespaces:
- A container that holds names and seperates them from those in the global namespace.

## Static Lifespan Objects
- Global Variables.
- Local variables declared with the static keyword.
- Character arrays created by the compiler corresponding to string literals.

**Example:**
```CPP
bool b; // This globally defined variable starts with a value of false.
int *gp; // Its value starts as nullptr.
```

### Initialization
```CPP
int x;          // Default initialization
int x = 10;     // copy init
int x(98);      // direct init
int x{10};      // uniform init  // brace init
```
> Default initialization starts objects with garbage value. Using this value may cause undefined behaviour.

**Why did modern C++ introduce {} as the form of initialization?**
- Uniformity: You can use braces for any type of initial value.
- Syntax error for narrowing conversions: If you use braces for a conversion that loses data, it will give a syntax error.

```CPP
double dval = 5.6;
int i{dval}; // This will cause a syntax error due to data loss, whereas using normal parentheses would have been legal code.
```
**In C++, all these mean the same:**
```CPP
int a1[4] = {0};
int a2[4] = {};
int a3[4]{};
```
> They all are zero-initialized. In C, inside of the braces must be filled, but in C++ it can be empty.

## Type Deduction
- The act of the compiler automatically determining the type of a variable opr expression. Particularly after C++11 this is done with the keywords **auto** and **decltype**.

**Auto type deduction**: A compile - time mechanism. The compiler automatically deduces the variable's type from the assigned value.

**Decltype type deduction:** Determines the type of a variable or expression and can be used for other variables. It  represents an expression.
```CPP
decltype(expr);
```
> The type obtained here depends on the value category of the "expr" expression.

- Type deduction is a compile - time mechanism, static mechanism. In some cases, even if we don't explicitly write the type, the language rules allow the compiler to understand the type by looking at the code.

```CPP
int a = 10;
decltype(a) b = 20; // will be of the same type as a (int).
```
**What does a static mechanism mean?**
- If a feature or toolset is related to compile time, and compiler is generates some codes by looking at the code, such tools are called static tools. If the tool is related to the runtime of the program, the term dynamic is used.
- **Benefits of type deduction:**
- In some cases, defining a type requires using many tokens. Type deduction reduces the risk of making mistake.

## Type Deductions
- auto type deduction
- decltype type deduction
- decltype(auto)
- lambda expression
- template

**Example**
```CPP
int* foo(const int*, size_t);

int main()
{
    int* (*fp)(const int*, size_t) = &foo;  // auto fp = &foo
}
```

**Note**
- NULL is a macro, defined in the standart header file of C.
```CPP
time(NULL);
time(0);
```
> Equivalent. nullptr is a keyword, a constant, and its type is nullptr_t. To use it, no header file inclusion is necessary.

### Lesson 2 Exercises

**Question 1: What is the type of the value produced by the sizeof operator?**

> size_t type.

**Question 2: Is this expression valid? What is its value?**
```CPP
#include <stdio.h>

int main()
{
    int x = 10;
    sizeof x+5;
}
```
> It is valid, and the value is 9.The predence of the sizeof operator is higher than arithmetic operators.

**Question 3: What will be printed on the screen when this code is run on a system where the int type is 4 bytes?**

> The output will be y = 4, x = 10. No operation code is generated for theh expression that is the operand of sizeof operator. In C++, situations where no operation code is generated for an expression are called "unevaluated context." In C, the unevaluated context exist only for the sizeof operator. In C++, there are 8-9  context where no operation code is generated.

**Question 4: What is the error?**
```CPP
int main()
{
	char* p = "batuhan";
}
```
> The answer is that since that is a const char array, it is undergoes array decay to const char* type. Since there is no imlicit conversion from const char* to char* in C++, it causes a syntax error. Error code: a value of const char* type cannot be used to initialize an entity of type char *

**Question 5: what is the type?**

```CPP
int main()
{
    short s1 = 5, s2 = 7;
    s1 + s2 
}
```
> The type of the expression s1 + s2 is not short, but int. Operations below the int type are converted to int type.

**Question 6: What is the type?**

```CPP
int main()
{
    int x = 10;
    x > 5 ? 3 : 4.7; 
}
```
> regardless of runtime and the value of x, the type of this expression is double.

**Question 7: Explain the code.**
```CPP
#include <iostream>

int main()
{
    std::cout << "hello world";
}
```
> The scope resolution operator is used to find and access a name within a namespace. Cout is the name of a variable, which is a global variable of the class type named ostream. Bitwise shift operator is used here as a part of mechanism **operator overloading**. When a class object becomes the operand of an operator, the compiler transforms this expression into a function call. Since the cout object is the operand of the << operator, the compiler converts it into a function call. The function called by the compiler receives the cout object and the string literal as arguments.

# Lesson 3 Examples

**Q1: Which function is called first?**
```CPP
x = f1() + (f2() * 5);
```
> Unspecified behaviour. There is no guarantee. It depends on the compiler.

**Q2: Will it enter the true part of if statement?**

```CPP
int main()
{
    const char* p1 = "oytun";
    const char* p2 = "oytun";

    if(p1 == p2){
    }
}
```
> Unspecified Behaviour. Whether the same string literals are stored in the same memory location by the compiler is entirely up to the compiler. When tested with C++ visual studio, it was observed that they are stored at the same adress.

**Q3: Is the code is correct?**
```CPP
int x;

int main()
{
#include <stdio.h>

int main(void)
{
    int printf = 5;
    printf("hello \n");
}
```
> There is a syntax error here, but the reason of error is not name lookup. It is undestood from name lookup that printf is a name of a variable of type int, and it becomes the operand of the function call operator. This is a syntax error.

**Question 4: Is the code correct?**
```CPP
#include <stdio.h>

int main(void)
{
    printf("merhaba \n");
    int printf = 5;
}
```
> There is no syntax error here. It's legal code. The name printf could not be found in the local scope, so it continued in the global scope and was found.

**Question 5: Is the code valid?**
```CPP
int main()
{
    for(int i = 0; i<10; i++)
    int i = 56;
}
```
> This code is valid in C language. It's a syntax error in C++.

**Question 6: Is the code valid?**
```CPP
void x();

int main() {
    int x = 34;

    x(); // Invalid
    ::x(); // Valid, searches the global namespace
}

```
**Question 7: Is the code valid?**
```CPP
int main(){
    
    int printf{};
    ::printf(_Format: "ali");
}
```
> Valid. It calls printf from the global namespace.

**Question 8: What is the value of y?**
```CPP
int main()
{
    int x =  0;
    int y = 10;

    int a = x && ++y;
}
```
> The value of y remains 10. No operation code is generated. There is short circuit behaviour.

# Lesson 5

## Type Conversion
- A situation where the compiler, to perform an operation, uses a different type of value instead of the static type of an expression in the code.
- Generally, a temporary object is created here.

1. Implicit Type Conversion
2. Explicit Type Conversion

**Implicit:** Even without a specific instruction given to the compiler by a code, the compiler performs an implicit type conversion based on the language rules.
**Explicit:** We instruct the compiler to perform this conversion

## References

**In modern C++, There are three seperate reference categories:**

- L value Reference
- R value Reference
- Forwarding Reference (Universal Reference)

**Example:**
```CPP
int main()
{
    int x = 10;
    int* p = &x;

    *p = 20;
}
```
> Here, *p is the object "x" itself. When you use *p, you are using "x".

> The object we are operating on is "x" itself. So "*p" means "x".

- References can not be default initialized:
```CPP
int& x; //  Syntax error
int& r = x; // Valid
```
```CPP
int* p = nullptr;
int* & r = p;

Here, r = p is the case.
```

### Usage of references

**99% probability is for:**

- Passing an object to a function by reference
- A function sends/passes an object itself to the code that calls it
- In C, function call expressions are always R value expressions.
- In C++, if the return type of a function is an L value reference, the type of the function call is alse a left-hand value.

## Type Deduction
- It has nothing to do with runtime. It is entirely related to compile-time.
- Determination of an object's type at runtime. (This is dynamic type)
- Type deduction is done for auto, not for the declared variable's type.

```CPP
const int cx = 6;
auto y = cx; // Here, the type of y is int. The const is dropped.

int main
{
    int a[3] = {1,2,3};
    
}
```
# Lesson 5 Examples

**Question 1: Is the code legal?**
```CPP
int main()
{
	int x= 5;
	int y = 9;
	int a = x+++y;
	std::cout << "a =" << a << "\n";
}
```
> Valid. The maximal munch rule applies. Tokenizing is done in a way to form the longest possible token.

**Question 2: Print "hello" on the screen but don't use ;.**

```CPP
int main() {
    if (std::cout << "hello\n") {
    }
}
```

```CPP
int main() {
    while (!(std::cout << "hello")) {
    }
}
```


```CPP
int main() {
    switch (!(std::cout << "hello")) {
    }
}
```

**Question 3: What is the output?**

```CPP
#include <iostream>

int main()
{
	int x = 10;

	int* p = &x;

	++* p;
	std::cout << x;
}
```

> The variable "x" itself is changing.

**Question 4: What is the output?**

```CPP
#include <iostream>

int main() {
    int x{ 3 };
    int& r{ x };
    // From here on, writing r in the scope is the same as writing x.
    std::cout << "x = " << x << "\n";

    r = 67;
    std::cout << "x = " << x << "\n";
    ++r;
    std::cout << "x = " << x << "\n";
}
```
> The outputs are x = 3, x = 67, x = 68.

**Question 5: What is the value of x in both C and C++ in this situation?**

```CPP
int main()
{
	int x = 45;
	// func(x);
	std::cout << "x =" << x << "\n";
}
```
> In C, all function calls are call by value. Therefore, the value of x is always 45. However, in C++, the same "func" function might use reference semantics. Without seeing the function's code, this question cannot be answered.

# Lesson 6

```CPP
auto x{3};      //  Here, the deduction is made as int.
auto x = {3};   // Here, the inference is made as std::initializer_list.
```
```CPP
int x = 10;
auto p1 = &x;       // int *p1 = &x; auto ==> int*
auto* p2 = &x;      // int *p2 = &x; auto ==> int
```
```CPP
int* ptr = &x;

auto p1 = &ptr;     // The type replacing auto is int**
auto* p2 = &ptr;    // int*
auto** p3 = &ptr;   // int

But ultimately, p1, p2, p3 are variables of type int**. The inference is made for auto, not the variable.
```

**Reference Collapsing**

- In the rules of C++ language, there is no reference to reference. But it can be created in some contexts.
- Instead of reference to reference, L value or R value reference is used.

### Default Argument

- A tool not exist in C. An argument, is the expression used in a function call.

**Parameter:** The function's parameter.

**Argument:** The value sent in the function call.

```CPP
foo(12); // Sent the argument with the value 12 to the function.
void func(int, int, int = 10);
```
> If the function's third parameter is not sent, it's assumed that 10 is sent.Default arguments are valid for the last parameters.

**It doesn't have to be a constant expression, for example:**

```CPP
void f(int = x);
veya,
int f1(int x = 0);
void f2(int y = f1());
int main()
{
    f2(); == f2(f1(0));
}
```

# Lesson 7

## Function Overloading
- Function overloading is a mechanism related to compile time.

**In the general programming, popular terms are used:**

- The compiler determines which function is called by looking at the code and will call that function. The binding of the call to the function is determined by the code generated by compiler.

> If a function call is bound to function at compile time, this is knows as **static binding** (early binding) in programming. If which function is being called is understood during runtime,  (identified by code running at runtime), this is called **dynamic binding** (late binding).

- Without function overloading, it would be like in C. We would have to give different names to multiple functions even if they do the same job, this makes code writing more difficult.
- If we don't know how to select overloaded functions, we might call the wrong function.

**According to the rules of the language, functions with the same name may may or may not overloading**

**For function overloadin occur:**
- The functions must have the same name
- They must be in the same scope
- Their signatures must be different

**C++ Scope Categories**

1. Namespace scope
2. Class scope
3. Block scope
4. Function prototype scope
5. Function scope

- When functions with the same name are in different scopes: name hiding, name masking, or name shadowing can occur.
- Functions in different scopes do not create overloads. Names in different scopes can hide each other.

**Function Signature:**
- The number of function parameter variables and type of each parameter. For overloading to occur, their signatures also need to be different.
```CPP
int foo(int, int);
int func(int, int);
```
> Have the same signatures.

## Function Overload Resolution
- The process of the compiler trying to figure out which function to call is called function overload resolution.
- It is a situation that does not change according to the compiler.

**How is Overload Resolution Done?**
- In the first stage, the compiler only records functions with the same name based on the function name. There are the candidate functions.
- In the second stage, compiler answer the question "Would it be legal to call this function with argumnents in this function call if this function were only one?". If answer is yes, there functions are called "viable functions."

**Note**
- Just because function overloading exist doesn't mean that every call to a fucntion with that name is legal. The function call could also be syntax error.

**User - Defined Coversion:**
- A conversion that normally doesn't exist, Occuring throughthedecleration of a function and the compiler using this function to perform the conversion.

# Lesson 7 Examples

**Question 1: Examine**
```CPP
#include <iostream>
#include <cstdint>


void func(int *)
{
    std::cout << "int *\n";
}

void func(const int *)
{
    std::cout << "const int *\n";
}

int main()
{
    const int cx = 5;
    func(&cx);
}
```
> Here, if the second function didn't exist, this call wouldn't be legal.

> If the object sent was "t*" instead of "cosnt t*", and if any one of the functions existed alone, the code would still be legal.

> The benefit is, we create 2 seperate codes for const and non-const objects and let the compiler make this choice at compile time.

**Question 2: Is there function overloading?**
```CPP
#include <iostream>

int foo(int);

int main()
{
	int foo(double);
}
```
> There is no fucntion overloading because their blockscopes are different. Here namehiding occurs.

**Question 3: Is there function overloading?**
```CPP
#include <iostream>

int foo(int);
double foo(int);
int main()
{
	
}
```
> There is no function overloading. Also this code is violates the language rules. This function is redeclered and it's return type is different.

**Question 4: Is there function overloading?**
```CPP
#include <iostream>

int foo(int);
int foo(int,int);
int main()
{
	
}
```
> There is overloading. They are in the same scope but have different signatures.

**Question 5: Is there function overloading?**
```CPP
#include <iostream>

void f(double* const p);
void f(double* p);
int main()
{
	
}
```
> Not overloading, but decleration. 

**Question 7: Is there function overloading?**
```CPP
#include <iostream>

void func(int&);
void func(cont int&);
int main()
{
	
}
```
> There is overloding. Reference semantics are used instead of the pointer semantics in the previous examples. This is one of most commonly used overloading structures in the standard library.

**Question 8: Is there function overloading?**
```CPP
typedef double flt_type;

void f(double);
void f(flt_type);

int main() {

}

```
> Not Overloading. Typedef doesn't mean a different type. There is no syntax error but redecleration exist.

**Question 9: How many function overloads are there?**
```CPP
void f(char);
void f(signed char);
void f(unsigned char);

int main() {

}
```
> There are 3 overeloads. The char type is implementation defined. It can be either signed or unsigned. In the type system, these are different types.

**Question 10: How many function overloads are there?**
```CPP
void f(int *);
void f(int **);
void f(int ***);

int main()
{

}
```
> There are 3 overloads. Each one is a different type.

**Question 11: Is there function overloading?**
```CPP
void f(int &);
void f(int &&);

int main() {

}
```
> Yes. One parameter is an lvalue reference, the other is an rvalue reference.

**Question 12: How many function overloads are there?**
```CPP
void f(int &);
void f(const int &);
void f(int &&);

int main() {

}

```
> There are 3 overloads.

**Question 13: Is there function overloading?**

```CPP
void f(std::int32_t);
void f(int);

int main() {

}

```
> It depends on the compiler. Implementation-defined. int32_t is an alias name for a type. If in another compiler this alias name belongs to a different type, then there is overloading here.

**Question 14: How many overloads are there?**
```CPP
void foo(int p[]);
void foo(int p[20]);
void foo(int *p);

int main() {

}
```
> There is 1 overload. All these are the same declaration. There is array decay here. The parameter of the function is a pointer. They all are of type int*.

**Question 14: Overloading or redeclaration?**
```CPP
void foo(int (int));
void foo(int(*)(int));

int main() {
    
}
```
> There is redeclaration. The type below is the type of a function's address of the type above.

- Top: "function type"
- Bottom: "function pointer type"


> So, (int (int)) is a function type, and (int(*)(int)) is a function pointer type. Therefore, a function's parameter type cannot be a function type.

**Question 15: How many overloads are there?**
```CPP
void foo(int (*)[5]);
void foo(int (*)[6]);
void foo(int (*)[7]);
void foo(int (*)[8]);

int main() {
    
}
```
> There are 4 overloads. One is a pointer type to a 5-element array, another is a pointer type to a 6-element array, and so on.

**Question 16: Are these two functions viable?**
```CPP
void func(double *);

int main() {
    func(2);
}

```
> Not viable. There is no conversion from int type to pointer type.

**Question 17: Are these two functions viable?**
```CPP
void func(double *);

int main() {
    func(0);
}

```
> Viable. There is null pointer conversion. The integer constant 0 will convert to a null pointer.

**Question 18: Is the code valid?**
```CPP
void func(bool);

int main() {
    int x{};
	func(&x);
}

```

> Yes. This is a direct pointer type. There is a conversion from pointer types to the bool type: if it's not a null pointer it's true, if it is a null pointer it's false.

**Question 19: Is the code valid?**
```CPP
void func(void *);

int main() {
    int x{};
    double f{};

    func(&x);
    func(&f);
}

```
> Both are valid because there is a conversion to void* type.

**Question 20: Is the code valid?**

```CPP
void func(char *);

int main() {
    func("talha abus");
}

```
> Invalid code. The string literal will decay to const char* type, but the function's parameter is char*.

**Question 21: Is the code valid?**
```CPP
enum pos {on, off, hold};
enum class color{yellow, deak_blue};

void f(pos);
void g(color);

int main() {
    f(1);
    f(2);
}

```
> Invalid code. There is no conversion from arithmetic types to enum types.

**Question 22: Is the code valid?**
```CPP
enum pos {on, off, hold};
enum class color{yellow, deak_blue};

void f(int);

int main() {
    f(color::yellow);
    f(off);
}

```
> The second call is valid, the first call is invalid. There is no conversion from scoped enum enumerators to the int type.

> Error code: "argument of type 'class' is incompatible with parameter of type 'int'"

**Question 23:**
```CPP
void f(int *);
void f(int, int);
void f(int);
void f(double);

int main() {
    double d{};
    f(&d);
}

```
> Received error code: "no instance of overloaded function 'f' matches the argument list"

**Notes from the questions:**
- The constness of a parameter does not create a signature difference.
- Type aliases given to the same type do not create overloading.
- Call by value and call by reference create overloading.

# Lesson 8

**Some Definitions**

**Function Overloading**
- The feature of having the same name in the same scope. Whichfunction is called is understood through function overload resolution.

### User - Defined Conversion
- A conversion not implicitly possible,but because a user defined a function for it, the compiler performs the conversion by calling this function.

```CPP
void func(int x, int y = 0);
void func(int x);
```
> This is function overloading because their signatures are different.

```cPP
int x = 10;
int &r = x;
```
> The value category of r is L value.

**Some Definitions:**

### One definition Rule
- Some entities, even though they are external but have the same definitions across different source files, don't violate the ODR.

### Inline Expension
- One of the most frequently used optimization techniques by compilers. It is a compiler optimization.

### Compiler Optimization
- The compiler is not obliged to produce the identical assembly code. As long as the observable behaviour doesn't change, the compiler can generate any code it wants.

### Dead Code Elimination
- The compiler deletes any code that doesn't change observable behaviour.

**In short:**
- We give the compiler what we want, and it guarantees the result while generating any code it wants. And this optimization is done with 

**Loop Unrolling:**
- Even though there is a loop, the compiler compiles the code as if the loop doesn't exist to eliminate additional costly operations. It can rewrite the code as many times as the loop (along with additional optimizations)

**Loop reversal:**
Reversing the direction of loop.

**Generic Programming**
- What the compiler writes at compile time, and some checks it makes at compile time, determine the code.
- Different versions of code can be written and optimized by the compiler.

**Inline Expension:**
- The most frequently used and oldest technique. It provides the most efficiency.

**Notes on these Definitions:**
- One of biggest differences between C++ and C, C++ compilers not only translator programs. They write code for us. The paradigm used for this writing is the generic programming paradigm.

```CPP
a = func();
```
> Func has a return value. And there is a memory adress to be written. Let's say the compiler generates code to copy the value at that memory adress to "a".

> Assuming func's definition is before this line of code. The compiler directly generates code such as "a = (function code)" But why generate such code?

> There is a cost to entering and exiting a function. But when optimized, there are direct arithmetic operations in the code.

> For example, if the function does 3 units of work inside, and the cost of entering and exiting the function is 10 units, the compiler calculatesthe cost to see if it's more efficient. This called **inline expension**. That is, there is a function call but the compiler-generated code has arithmetic operations.

> The best candidates for this are functions that have small code and called frequently.

### Inline Functions
- They do not violate the one definition rule.

```CPP
inline int func(int x, int y)
{
    
}
```
- If the definition of this function is the same in multiple source files, it doesn't violate the one definition rule. This means that if the inline function's definition is placed in a header file, it will not violate the ODR.

**Why do we do this?**

- To allow the compiler the possiblity of inline expansion. when we make a function inline, we ensure the compiler sees the function.

**Note:**
- The compiler is not obliged to inline a function just because the inline keyword is used, and it can inline expand functions that are not marked inline.
- The purpose of writing inline is to put it in the header file; if it were not inline, it would be violation of the ODR.

### Complete - Incomplete Type
```CPP
class Nec; // Class decleration
```
- The compiler is aware of the existence of a type but doesn't know its details.
- If we make such a decleration, the compiler knows the class type when it sees this declaration but does not see its definition.
- This is an incomplete type, The complete type is the opposite. The compiler is aware of all information.

**Why does it matter if a type is complete or incomplete type?**
> For some codes, it is sufficient for the type to be incomplete for the code to be compiled.

# Lesson 9

## Inline Functions
- If the definition of an inline function requires significant processing, expending it inline will not yield a high benefit.

1. Direct definition with the inline keyword
2. Decleration with a class

```CPP
class Myclass{
    void func();
}
```
> Functions declared within a class are always considered inline.

**Entities in the header file that do not violate the ODR**
-  Inline Functions
-  Class definitions
-  Templates

> Function templates, class templates, alias templates, variable templates.

**Inline Variables:**
```CPP
inline int x = 10;
```
> 































