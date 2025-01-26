# FOFI: Language Features

This document summarizes the current feature set of FOFI. For a broader overview and examples, see [GUIDE.md](./GUIDE.md) or the [docs folder](./docs/).

---

## Core Features

• Simple Lexical Structure:  
  - The FOFI lexer is built on deterministic finite automata, making tokenization fast and reliable.

• Recursive-Descent Parsing:  
  - Straightforward grammar, easy to extend.  
  - Error messages can be cryptic at times, but improvements are on the way.

• Strict Typing:  
  - Basic types: `numero`, `binario`, `texto`.  
  - Uniform type rules enforced at compile time.

• Built-in Functions:  
  - Input: `ler_numero(msg)`, `ler_binario(msg)`, `ler()`, `consultar()`  
  - Output: `mostrar(value)`  

• Control Structures:  
  - `se(...) { ... } senao { ... }`  
  - `enquanto(...) { ... }`  
  - `repita(<count>) { ... }`  

• Semantics:  
  - Variables default to zero or false if uninitialized.  
  - Purely functional "core" transformations behind the scenes, though user code can look imperative.

• JavaScript Code Generation:  
  - Generates ES5-compatible JS.  
  - Bundles declarations into separate sections for variables, statements, and function calls.

---

## Advanced Features

• Early-stage Error Handling:  
  - "Semantic error" vs. "Parse error" classification.  
  - Error messages are improving but remain a work in progress.

• Symbol Table & Type Checking:  
  - Detects duplicate variable declarations.  
  - Basic type inference (e.g., `numero` vs. `binario` mismatch).

• Continuation-Passing Style (CPS) IR:  
  - Under-the-hood representation that could be leveraged for potential optimizations.

---

## Experimental & Future

1. **User-Defined Functions**  
   - Partial support for custom inline or "macro-like" expansions.  
   - Future: dedicated function syntax and modules.

2. **Modules & Imports**  
   - A prototype system is in the works to let you separate code into multiple files with easy imports.

3. **Advanced Types**  
   - Possibly parametric polymorphism (like generics).  
   - Algebraic data types, optional pattern matching.

4. **Concurrency**  
   - Stretch goal. We're exploring concurrency or actor-like message passing. No timeline yet.

5. **Package Management**  
   - We hope to have a manager to publish and install shared FOFI libraries.

6. **Debugger & Tooling**  
   - A stable debugging interface or interactive REPL is on our radar.

---

## Recommended Usage

• **Small to Medium Scripts**  
  Great for teaching coding basics, especially if you want a language that's easy to parse and reason about.

• **Lightweight Tools**  
  Quick prototypes that compile down to JavaScript.

---

## Limitations

- **Single-File Orientation**: While you can compile multiple `.fofi` files separately, there is no official multi-module approach.  
- **Limited Native Library**: FOFI's built-in library covers only fundamental I/O and simple operations.  
- **No Formal Package Manager** (Yet!): All your code must be local or manually included.  
- **Error Feedback**: Limited insights in semantic errors, especially with line numbers or context.

Feel free to explore the language in your own projects and stay tuned for new features. We're excited to see what you build with FOFI! If you have feedback, please let us know through our GitHub repository. Happy coding! 