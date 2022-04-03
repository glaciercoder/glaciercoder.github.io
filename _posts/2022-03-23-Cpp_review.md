---
layout: default
title:  "C++ review"
date:   2022-03-23 14:15:23 +0800
categories: Programming
---

# Background

This is a C++ review based on *C++ primer fifth edition*



# Type

1. C++ is a statically typed language; type checking is done at compile time.
1. Signed values are auto- matically converted to unsigned, 
1. If we assign an out-of-range value to an object of unsigned type, the result is the remainder of the value modulo the number of values the target type can hold. If we assign an out-of-range value to an object of signed type, the result is **undefined**. 
2. The form and value of a literal determine its type
2. The type of a literal can be specified by adding prefix and suffix
3. An extern that has an initializer is a definition
4. A temporary object is an unnamed object created by the compiler when it needs a place to store a result from evaluating an expression.

## Compound types

1. By default, a reference may be bound only to an object, not to a literal or to the result of a more general expression. However, const reference is an exception.
2. We cannot use a `void*` to operate on the object it addresses
3. The understanding of declarator should follow the **right to left, inside to outside** rule.

### `const`

1. By Default, const objects are local to a file. To share a const object among multiple files, you must define the variable as extern.
2. We can initialize a reference to const from any expression that can be converted to the type of the reference.
3. When we copy an object, top-level consts are ignored. On the other hand, low-level const is never ignored.

#### constexpr

1. Whether a given object (or expression) is a constant expression depends on the types and the initializers
2. Generally, it is a good idea to use `constexpr` for variables that you intend to use as constant expressions.
3. The key point of `constexpr` is that it can only be evaluated at compile time. So anything used to initialize the constexpr variable must have values that are ==totally determined== at compile time. This kind of variable is said to have **Literal Type**

    ```cpp
    const int max_files = 20; // literal type
    int size = 3; // not a literal type
    constexpr int *np = nullptr; // Literal type
    constexpr int &s = size; //error! not a literal type
    ```

4. `constexpr` imposes a top-level const:

    ```cpp
    constexpr int * p = nullptr; // p is a const pointer rather than a pointer to const
    ```

### `auto` and `decltype`

1. `auto` ordinarily ignores top-level consts.  As usual in initializations, low-level consts, such as when an initializer is a pointer to const, are kept. However, we can add `const` to pertain the top-level const

    ```cpp
    const auto &j = 42;
    ```

2. When we ask for a reference to an auto-deduced type, top-level consts in the initializer are not ignored. 
3. decltype((*variable*)) (note, double parentheses) is always a reference type, but decltype(*variable*) is a reference type only if *variable* is a reference.
4. If  `decltype` is used for an expresstion that yield a result can be used as modifiable lvalue, it may genertate a reference type, ignore this by transferring the expresstion that yields a non-reference result

    ```cpp
    int i = 3; int &r = i;
    decltype(r + 0) k;// k is not a reference type
    ```





# Strings, Vectors and arrays

Headers Should Not Include `using` Declarations

## String

```cpp
// Initilizers for string
string s1;//default
string s4(n, ’c’); //Initialize s4 with n copies of the character ’c’.
//Copy constructors
string s2(s1);
string s2 = s1;
string s3("value");
string s3 = "value";
```

1. The string class—and most other library types—defines several companion types. These companion types make it possible to use the library types in a machine-independent manner. 
2. The type `size_type` is string's companion type.

## Vector

```cpp
// Initilizers for vector
vector<T> v1; // default
vector<T> v3(n, val); // n elements of val
vector<T> v4(n); // n empty elem
vector<T> v5{a,b,c . . . }; //list initilizer
vector<T> v5 = {a,b,c . . . };
// Copy constructors
vector<T> v2(v1);
vector<T> v2 = v1; 
```

Attention: If list initialization isn’t possible, the compiler looks for other ways to initialize the object from the given values.

## Array

1. The key of the type of array is: ==The number of elements in an array is part of the array’s type.== As a result, the dimension must be known at compile time, which means that the dimension must be a constant expression.
2. There is no such thing as *Copy or Assignment* of an array, this feature has an influence on the definition of the function that uses array.
3. `size_t` is the companion type of the array.
4. Unlike subscripts for vector and string, the index of the built-in subscript operator is not an unsigned type.

    ```cpp
    int a[3] = {1, 2, 3, 4};
    int *p = &a[2];
    int j = p[-1];// valid in array
    ```

5. When use `auto` for array, it will yield a pointer, this will casue bug in multidimensional array:

   ```cpp
   size_t cnt = 0;
   for(auto &row : array)
     for(auto col : row)
       ...
   ```

   To use a multidimensional array in a range for, the loop control vari- able for all but the innermost array must be references. Since pointer can not be used to loop.



# Expressions

1. Roughly speaking, when we use an object as an rvalue, we use the object’s value (its contents). When we use an object as an lvalue, we use the object’s identity (its location in memory).
2. Operators can be classfied by the operands lvalue or rvalue, and reture type lvalue or rvalue.
3. Precedence and associativity specifies how the operands are grouped. It says nothing about the order in which the operands are evaluated.
4. Relational Operators are left associative.
5. Assignment Is Right Associative
6. Because there are no guarantees for how the sign bit is handled, we strongly recommend using unsigned types with the bitwise operators.
7. The sizeof operator is unusual in that it does not evaluate its operand

## Type conversion

1. The implicit conversions among the arithmetic types are defined to preserve precision, if possible.
2. In an initialization, the type of the object we are initializing dominates. 
3. `const_cast` can be used to change the const status. However, using a const_cast in order to write to a const object is undefined.
4. `static_cast` can only be used where low-level const is not involved.



# Statements

1. case labels must be integral constant expressions 



# Functions

1. A function call does two things: It initializes the function’s parameters from the corresponding arguments, and it transfers control to that function. 
2. Typically, a function may be defined only once but may be declared multiple times.
3. Put declarations in header file has the following benefits: ensure that all the declarations for a given function agree. Moreover, if the interface to the function changes, only one declaration has to be changed.
4. ==Parameter initialization works the same way as variable initialization.==
5. Use non-const parameter will unduly limits the type of arguments that can be used with the function.
5. The return value is used to initialize a temporary at the call site, and that temporary is the result of the function call.

## Function with varying parameters and varying return value

1. Template type `initilizer_list<T>` provides a way to give varying parameters with the same type:

    ```cpp
    initilizer_list<int> t{1,2,3,4,5};
    int adder(initilizer_list<int> t){
      //...
    }
    ```

2. Actually there is no varying return value, but we can return a list that can be used to initialize a vector:

   ```cpp
   vector<string> process(){
     //...
     return {"asf", "asdf", "asdf"};
   }
   ```
   

### Trailing return

```cpp
// fcn takes an int argument and returns a pointer to an array of ten ints 
auto func(int i) -> int(*)[10];
```

## Overloaded Function

1. A parameter that has a top-level const is indistinguishable from one without a top-level const.
2. `const_cast` is very useful in the code reuse for const overloading function.
3. In C++, name lookup happens before type checking, but names do not overload across scopes. So if the caller can not find the right name in the scope, it can't do a right function match.

## `constexpr` function

A `constexpr` function must have return type and the type of each parameter in be a literal type, and should be defined in a header file.

## Function pointer

1. A function’s type is determined by its return type and the types of its parameters. The function’s name is not part of its type. 

2. When we use the name of a function as a value, the function is automatically converted to a pointer. This can also be explicitly delcared.

   ```cpp
   int (*func) (int&, int&)
   // The following two are equivalent
   func = adder;
   func = &adder;
   // The following two are equivalent
   void F(int (*func)(int&, int&));
   void F(int func(int&, int&));
   ```

3. As with arrays, we can’t return a function type but can return a pointer to a function type.



# Class

1. The compiler processes classes in two steps—the member declarations are compiled first, after which the member function bodies, if any, are processed.
2. Members that define types must appear before they are used.

## `const` function

1. By default, the type of `this` is a const pointer to the nonconst version of the class type. A `const` following the parameter list indicates that this is a pointer to const.
2. A const member function that returns `*this` as a reference should have a return type that is a reference to const.

## Constructers

1. When we create a const object of a class type, the object does not assume its “constness” until after the constructor completes the object’s initialization. Thus, constructors can write to const objects during their construction.
2. The default constructor is one that takes no arguments. The compiler-generated constructor is known as the **synthesized default constructor**.
3. Under the new standard, if we want the default behavior, we can ask the com- piler to generate the constructor for us by writing **= default** after the parameter list.
4. Constructors should not override in-class initializers except to use a different initial value.
5. Members that do not appear in the constructor initializer list are initialized by the corresponding in-class initializer (if there is one) or are default initialized.
6. We *must* use the constructor initializer list to provide values for members that are const, reference, or of a class type that does not have a default constructor. 
7. Members are initialized in the order in which they appear in the class definition in initilizer list.
8. New standard permits **Delegating Constructers**
9. 

## Friends

1. Classes and nonmember functions need not have been declared before they are used in a friend declaration.  A friend declaration only specifies access. It is not a general declaration of the function. If we want users of the class to be able to call a friend function, then we must also declare the function separately from the friend declaration.
2. The member functions of a friend class can access all the members, including the nonpublic members, of the class granting friendship. 
3. Friendship is not transitive.
4. Making a member function a friend requires careful structuring of our programs to accommodate interdependencies among the declarations and definitions. Sometimes forward declaration will be helpful.

## Class Scope

1. Once the class name is seen, the remainder of the definition—including the parameter list and the function body—is in the scope of the class. When a member function is defined outside the class body, any name used in the return type is outside the class scope.

### Name Lookup

There are several important sets of name-looking-up rule:

1. For names in plain block:

   - First, look for a declaration of the name in the block in which the name was used. ==Only names declared before the use are considered.==
   - If the name isn’t found, look in the enclosing scope(s).
   - If no declaration is found, then the program is in error.

2. For names in the body of a member function, there is a two-phase process:

   - First, the member declarations are compiled.
   - Function bodies are compiled only after the entire class has been seen.

   The second step in detail:

   - First, look for a declaration of the name inside the member function. As usual, only declarations in the function body that precede the use of the name are considered.
   - If the declaration is not found inside the member function, look for a declaration inside the class. All the members of the class are considered.
   - If a declaration for the name is not found in the class, look for a declaration that is in scope ==before the member function definition==.

   In this process, the name declared in outer scope will be overrided, however, even though the class member is hidden, it is still possible to use that member by qualifying the member’s name with the name of its class or by using the this pointer explicitly.

3. For names in declarations, including names used for the return type and types in the parameter list:

   - First, look for declaration of the name before this declaration in the class
   - If not found, the compiler will look for that name in the scope(s) in which the class is defined ==before the member function declaration==.

## Static

1. Static member functions are not bound to any object; they do not have a `this` pointer.

2. When we define a static member outside the class, we do not repeat the static keyword. The keyword appears only with the declaration inside the class body.

3. we must define and initialize each static data member outside the class body

4. we can provide in-class initializers for static members that have const integral type.

4. The `static const`/`static constexpr` initilizer in class will just result in text substitution, which means ==they are not actually definition==s. So it is always preferred to define them outside with no initilizer:

    ```cpp
    constexpr int Account::period; //static keyword can be omitted outside
    ```

5. static member can have incomplete type in its declaration.

## Implicit Class-Type Conversion

Constructers with one argument is called **converting constructors**. If a class has converting constructers, when a function needs an object of the class as input, the existence of convering constructors will allow a type other than the class object to be used.This  is the implicit type conversion of class.

There are several features of implicit type conversion:

1. Only One Class-Type Conversion Is Allowed: implicit class-type conversion doesn't allow other conversions be used again.
2. Use `explicit` keywork to ban the implicit class-type conversion.
