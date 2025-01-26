# FOFI in 15 Minutes – The Definitive Guide!

Welcome to the FOFI language guide! FOFI is a simple, statically typed language with roots in both imperative and functional paradigms. Originally designed for educational use, it aims to be readable, safe, and fun to program in. This document will walk you through the essentials of FOFI, from syntax basics to some advanced language features. By the end, you should be able to write, compile, and run simple FOFI programs.

If you want a deeper understanding of the compiler internals (lexing, parsing, type analysis, code generation), see our main [README.md](./README.md). If you just want to learn how to get started, read on!

---

## Table of Contents

1. [Installing FOFI](#installing-fofi)  
2. [Hello, FOFI!](#hello-fofi)  
3. [Variables and Types](#variables-and-types)  
4. [Control Structures](#control-structures)  
5. [Functions](#functions)  
6. [Built-in Functions](#built-in-functions)  
7. [Immutability and the Rationale](#immutability-and-the-rationale)  
8. [FOFI Future Plans](#fofi-future-plans)

---

## Installing FOFI

### Requirements

• A working installation of the Glasgow Haskell Compiler (GHC).  
• Cabal (usually ships with GHC).  
• Node.js if you want to run the generated JavaScript code.

### Steps

1. Clone or download the FOFI compiler repository.  
2. Navigate into the project folder and run:
```bash
cabal update
cabal install --only-dependencies
cabal build
```

3. Assuming everything compiles fine, the binary "fofi-compiler" should appear in the Cabal build directory.

4. Optionally, confirm that "fofi-compiler" is in your PATH or copy it to a convenient location.

---

## Hello, FOFI!

Here's the simplest FOFI program:

```fofi
programa
"HelloWorld Program"

var
texto greeting;

{
    greeting : "Hello, FOFI!";
    mostrar(greeting);
}
```

• `programa "HelloWorld Program"` is a special prefix telling the compiler about the program title (optional).  
• `var texto greeting;` declares a single variable (`greeting`) of type `texto` (string).  
• The block `{ ... }` is the program's main body.

Compile and run:

```bash
fofi-compiler hello.fofi
node hello.fofi.js
```

Output should be:

```
Hello, FOFI!
```

---

## Variables and Types

FOFI has three built-in types at the moment:

1. `numero`: For numeric operations.  
2. `binario`: Boolean values (`true`/`false`).  
3. `texto`: For strings.

### Declaration

A single line can declare one or more variables of the same type:

```fofi
numero a, b, sum;
binario done;
texto message;
```

### Initialization

Use the assignment statement (`:`) to initialize:

```fofi
a : 3;
b : 4;
sum : a + b;  // sum : 7;
done : false;
message : "FOFI is neat!";
```

---

## Control Structures

FOFI provides classic control structures for flow control, including if-else, while, and a custom "repeat" loop.

### If-Else

```fofi
se (done) {
    mostrar("All done!");
} senao {
    mostrar("Not done yet...");
}
```

### While

```fofi
enquanto (a < 10) {
    mostrar(a);
    a : a + 1;
}
```

### Repeat

```fofi
repita (3) {
   mostrar("Repeat me!");
}
```

---

## Functions

FOFI supports user-defined functions to keep your code organized. While not as extensive as some purely functional languages, it's enough to separate logic into modular chunks.

Below is an example of a simple function that returns the sum of two numbers. Right now, functions in FOFI are declared inline in the main block (there is no separate "function" keyword, so we typically define them using custom syntax or macros).

```fofi
// Suppose we create a function style in an external file or as part of the AST:
numero soma(numero x, numero y) {
    retornar x + y;
}
```

Then in your main block, you might do:

```fofi
var numero result;
result : soma(2, 5);
mostrar(result); // 7
```

(You'll need the compiler's function definitions to be placed before usage. This can be handled manually or with a FOFI "import" placeholder.)

---

## Built-in Functions

The FOFI core library includes some handy built-in functions:

• `ler_numero(msg)`: Displays `msg` (string), reads an integer from input.  
• `ler_binario(msg)`: Displays `msg` (string), reads true/false from input.  
• `ler()`: Reads raw input from a special device (like a file or standard input).  
• `consultar()`: A non-blocking I/O check.  
• `mostrar(value)`: Prints `value` on the screen (or console).

Example usage:

```fofi
numero age;
age : ler_numero("Enter your age: ");
mostrar(age);

binario ok;
ok : ler_binario("Continue? ");
mostrar(ok);
```

---

## Immutability and the Rationale

One curious aspect is that FOFI tries to be functionally pure at heart. While the language allows mutable variables for simplicity, the compiler uses certain techniques for optimization behind the scenes, including possible transformations into immutable structures. This approach helps with:

• Easier reasoning about code.  
• Fewer side-effects that can break code unexpectedly.  
• Potential for optimizations in code generation.

However, it does mean you might occasionally see limitations or warnings if your code tries to mutate variables in unusual patterns. Long-term, we plan to add more purely functional data structures to highlight the advantages of immutability in performance and design.

---

## FOFI Future Plans

FOFI is still evolving. Future improvements include:

• Enhanced type system (polymorphic or parametric types).  
• More robust I/O bindings (file IO, network IO).  
• Possibly, concurrency constructs.  
• Enhanced error handling (try-catch style).  
• Extended standard libraries (string manipulation, data structures, etc.).

Despite being new, FOFI can already handle a variety of tasks, from basic input-output scripts to more advanced numeric computations. We invite you to explore, experiment, and help shape its development.

---