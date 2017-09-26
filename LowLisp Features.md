# Features Necessary for LowLisp

This document lists everything that will be needed in LowLisp, in order to implement HighLisp.


## Language

### Functions

* Are not first class, but experience only a small amount of discrimination. There are function pointers (as in C), and attempting to assign a function to a variable just stores its respective address.
* Cannot be redefined. However, code can modify a function pointer that will be called in the future. This can be used to implement function redefinition in higher-level languagues.
* Lack reflection and metaprogramming. Code cannot see which S-expressions make up a function, and cannot modify the function in any way other than overwriting its machine code in memory (probably a bad idea).
* Must have their parameters and return values defined completely (the generic pointer counts as a defined type).

### Variables

* Are lexically scoped.
* Are allocated on the stack when declared inside of a function.
* Are allocated on the heap when declared outside of a function.
* Must have a type that is known at compile-time, which must include their size in memory.

### Pointers

* By default are reference-counted, and automatically deallocate their target once the last of their kind falls into oblivion.
* Are also available in raw form.
* Are also available in a raw form with no type information at compile-time, à la void pointer in C.
* Must point to a type known at compile time.
* May point to a tagged union (type :go, for “generic object”).
* Do not need to know the size of their target.

## Library

### Memory allocation

* Equivalents to C's malloc(), free(), and string functions.
* All memory is zeroed after being received from the OS, and before being returned to it.

### I/O

* Functions to run system calls
