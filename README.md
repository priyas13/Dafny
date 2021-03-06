# Dafny
## Introduction
Dafny is a programming language with built-in specification constructs. Dafny static program verfier can be used to verify the functional correctness of the programs. The language is designed to support the static verification of programs. It supports imperative, sequential, generic classes, dynamic allocation, and inductive datatypes. It is build using specifications which include pre-condition, post-condition, frame specification and termination metrics. 

Dafny verifier is run as a part of the compiler. Programmers interact with Dafny in the same way as with the static type checker. So if the program throws an error (may be a type error for example) then programmer responds by changing the program's type declarations, statements and specifications.

The main goal of Dafny is to write correct codes. Correctness here covers both not only getting rid of the bad behaviors at run-time but also making sure that program does what it is suppose to do (that means program meets all its required specifications). Program written in Dafny are annotated with high-level annotations. These high-level specifications are not easy to write but also help to check for the correctness of the program. Writting a big-free annotation is always easier than writting a bug-free code.

## Overview
Dafny is like an imperative style programming. It has methods, variables, loops, types, if etc. The main building block of Dafny is method.

### Structure of a method:
```
method Sum (x: int) (y: int) returns (z: int)
{
   ...
}
```
In the above code method name is Sum which takes two inputs x and y and returns an output z. As we see in the code, Dafny requires us to put the type of each variable. 
```
method Sum (x:int, y: int) returns (z: int)
{
   ...
}
```
There can be another way to use comman to have multiple input or outputs.

### Simple example which includes specification 
As discussed earlier, we know that Dafny comes with a feature of adding high-level annotations which resembles specifications. For the Abs method, it should always return the absolute value of the input which means that it should be always more than or equal to zero. People generally write in comments that method Abs needs to have these properties but what happens in general scenario that these comments gives us nothing. If the method Abs is changed and comment remains same, the method will produce something different at run-time. But if the program is annoted with specification then Dafny will not allow the program to pass until it meets the specifications. 
**_Pre and Post conditions_** are the way to write specifications. Dafny supports the features to write pre and post conditions.
```
method Abs (x : int) returns (z : int)
ensures 0 <= y 
{
 ...
}
```
**_ensures_** keyword resembles the post condition. Post condition is a part of method declaration and is written before the method body.
**_requires_** keyword resembles the pre condition. Pre condition is a part of method declaration and is written before the method body.
**_Assertions_** As discussed above, pre and post conditions which can be only placed at the start of the program point and ensures that those conditions (post) are true only after the method is completely executed. Dafny also supports features to write specifications that needs to satisfied at particular program point. Assertions are placed at the middle of the program .i.e. in the body of the method. As compared to **_requires_** and **_ensures_** which are placed before the method body, **_assert_** can be placed in the body of the method.
```
method testing 
{
  assert 1 > 0;
}
```
The above program will pass through because the assertion 1 > 0 is always true at every program point.

### Functions as compared to methods in Dafny
As discussed above to annotate the assertions about the methods we need to add the variables. Assertions can be written directly in the function without capturing to a local variable. There are examples in the Examples directory which contains examples illustrating the functions.

### Loop Invariants 
Dafny supports imperative style of programming, hence it supports while loops. But it is not possible to know in advance how many times the while loop is going to execute. Dafny supports the feature of writing loop invariants which is another kind of annotation for a program. A loop invariant is an expession that holds upon entering a loop, and after every execution of the loop body. 
```
var i := 0;
while i < n
 invariant 0 <= i 
 {
   i := i + 1;
 }
```
In the above piece of code, we could see the job of the while loop is to maintian the positive nature of variable i. Hence we could add the loop invariant 0 <= i. Dafny proves two things (1) When the loop enters the invariant is true (2) The invariant is preserved by the loop

### Termination
Dafny supports the feature of code termination. The use of **_decreases_** annotation helps to write annotation which helps to get rid of loop from getting executed forever. Dafny helps in providing termination in both loops and recursion. 

### Arrays
Arrays are build as part of the language. The type of array is array<T> where T is the type of the element of the array. For example the type of array of integers is array<int>. Arrays can be null. Also there are build in methods to play around the array data type like a.Length, a[i] etc. 
```
   method Find (a:array<int>, key: int) returns (index: int)
     ensures 0 <= index ==> index < a.Length && a[index] == key
   {
     ...
   }
```
In the above code the post condition is written using ensures. It checks that the correct index is returned for the key provided as input. 
