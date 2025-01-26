# FOFI Compiler

This project began as an initiative to support inclusive education tools, 
particularly benefiting children with ASD (Autism Spectrum Disorder). 
To learn more, you can learn more here (in Portuguese): 
<a href="https://g1.globo.com/sp/sao-paulo/bom-dia-sp/video/universitarios-criam-tapete-para-criancas-autistas-12778632.ghtml">
here</a> 

A high-performance, functionally-pure compiler for the FOFI language, implemented in Haskell.
FOFI (Framework Orientado para Facilitação Inclusiva) is a simple, statically-typed programming language inspired by both imperative and functional paradigms. Our compiler is built with modular design techniques, providing a clean architecture for lexical analysis, parsing, semantic analysis, and code generation.

<div align="center">
  
[FOFI Docs] | [User Guide] | [Contributing] 

</div>

[FOFI Docs]: ./docs/README.md
[User Guide]: ./docs/README.md#table-of-contents
[API Documentation]: ./docs/README.md
[Contributing]: ./CONTRIBUTING.md
[Changelog]: ./CHANGELOG.md

---

## Table of Contents
1. [Introduction](#introduction)  
2. [Features](#features)  
3. [Installation](#installation)  
4. [Using the Compiler](#using-the-compiler)  
5. [Code Overview](#code-overview)  
6. [Examples](#examples)  
7. [Contributing](#contributing)  
8. [License](#license)

---

## Introduction

FOFI is designed to be easy to learn and powerful enough to demonstrate key concepts of compiler design. It achieves:
• Functional-purity: Emphasizing immutable data structures and declarative design.  
• High-level abstractions: Leveraging Haskell's monadic parser combinators and lazy evaluation.  
• Readable syntax: Drawing ideas from both imperative and functional styles, making it easy to transition from other languages.

See the [FOFI language documentation](./docs/README.md) for more details about the syntax, data types, control structures, and built-in functions.

---

## Features

• Lexical Analysis using deterministic finite automata (DFA).  
• Recursive Descent Parsing with monadic combinators.  
• Polymorphic Type Inference and advanced semantic checks.  
• Intermediate Representation in continuation-passing style (CPS).  
• Optimized JavaScript Code Generation.  
• Cross-platform: The compiler is written in Haskell using GHC, so it runs on most systems.

---

## Installation

To build and install the compiler, make sure you have GHC (Glasgow Haskell Compiler) and Cabal installed.  
Then, from the repository root, run:

```bash
cabal update
cabal install --only-dependencies
cabal build
```

This will produce the binary (called "fofi-compiler" by default) in one of Cabal's build directories.

---

## Using the Compiler

Once compiled, run:

```bash
./dist/newstyle/build/.../fofi-compiler <input-file>
```

The compiler will:
1. Lex and parse the input FOFI file.  
2. Perform semantic checks (type checking, variable declarations, etc.).  
3. Generate the corresponding JavaScript code (saving it in <input-file>.js).

A typical command might look like:

```bash
fofi-compiler my_program.fofi
```

If compilation succeeds, you'll see:
```
Compilation successful!
```

Check out the newly generated "my_program.fofi.js" file in the same directory.

---

## Code Overview

This repository is organized into key modules, each handling a major phase of compilation. Below are brief overviews of some files and a sample of how they work.

### 1. Main Entry Point

The compiler's top-level behavior is defined in [src/Main.hs](./src/Main.hs). It reads command-line arguments, calls into the different phases, and writes the final JavaScript output.

```haskell:src/Main.hs
module Main where

import System.Environment (getArgs)
import Lexer (tokenize)
import Parser (parse)
import SemanticAnalyzer (analyze)
import CodeGenerator (generate)

main :: IO ()
main = do
    args <- getArgs
    case args of
        [inputFile] -> do
            contents <- readFile inputFile
            let tokens = tokenize contents
            case parse tokens of
                Left error -> putStrLn $ "Parse error: " ++ error
                Right ast -> do
                    case analyze ast of
                        Left error -> putStrLn $ "Semantic error: " ++ error
                        Right _ -> do
                            let code = generate ast
                            writeFile (inputFile ++ ".js") code
                            putStrLn "Compilation successful!"
        _ -> putStrLn "Usage: fofi-compiler <input-file>"
```

### 2. Lexer

[Lexer.hs](./src/Lexer.hs) transforms raw text into tokens (e.g., identifiers, types, operators):

```haskell:src/Lexer.hs
module Lexer where

import Data.Char (isAlpha, isAlphaNum, isDigit, toLower)

data Token = Token
    { tokenType :: String
    , tokenValue :: String
    , tokenLine :: Int
    } deriving (Show, Eq)

-- Core lexer function 
tokenize :: String -> [Token]
tokenize input = ...
```

### 3. Parser

[Parser.hs](./src/Parser.hs) converts tokens into an Abstract Syntax Tree (AST). We use a recursive descent approach. Once the AST is built, we can do further checks or transformations:

```haskell:src/Parser.hs
module Parser where

import Lexer (Token(..))

data AST = ...
-- This data type encapsulates the entire structure of the program.
 
parse :: [Token] -> Either String AST
parse tokens = ...
```

### 4. Semantic Analysis

[SemanticAnalyzer.hs](./src/SemanticAnalyzer.hs) checks for type correctness, variable declarations, etc. It uses a symbol table to ensure everything is well-typed:

```haskell:src/SemanticAnalyzer.hs
module SemanticAnalyzer where

import qualified Data.Map as Map
import Parser (AST(..), Expression(..))

analyze :: AST -> Either String ()
analyze (Program _ varDecls stmts) = ...
```

### 5. Code Generation

[CodeGenerator.hs](./src/CodeGenerator.hs) traverses the validated AST and emits JavaScript code:

```haskell:src/CodeGenerator.hs
module CodeGenerator where

import Parser (AST(..), Expression(..))

generate :: AST -> String
generate (Program desc varDecls stmts) = ...
```

---

## Examples

Below is a minimal "Hello, FOFI!" example. For a more in-depth guide, see the [FOFI Language Documentation](./docs/README.md).

Create a file named `hello.fofi`:

```fofi
programa
"This is a simple FOFI program"

var
texto message;

{
    message : "Hello, FOFI!";
    mostrar(message);
}
```

Compile it:
```bash
fofi-compiler hello.fofi
```

You'll get `hello.fofi.js`. Run it with Node.js (or any JavaScript runtime):
```bash
node hello.fofi.js
```

Expected output:
```
Hello, FOFI!
```

For additional examples, including control structures, function usage, and advanced graphics/animation, check out [docs/README.md](./docs/README.md#examples).

---

## Contributing

We welcome contributions! If you'd like to propose a feature or fix a bug:
1. Fork the repository and make your changes in a new branch.  
2. Create a Pull Request describing your changes.  
3. Ensure your code passes any relevant tests.  

Also, please open an issue if you find any bugs or have feature requests. See [CONTRIBUTING.md](./CONTRIBUTING.md) for details.

---