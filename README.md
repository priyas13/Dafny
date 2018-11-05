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
Pre and Post conditions are the way to write specifications. Dafny supports the features to write pre and post conditions.
```
method Abs (x : int) returns (z : int)
ensures 0 <= y 
{
 ...
}
```
**_ensures_** keyword resembles the post condition. Post condition is a part of method declaration and is written before the method body.
