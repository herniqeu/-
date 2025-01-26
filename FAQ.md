# Known Issues and Frequently Asked Questions

Below are some frequently asked questions that new users of the FOFI language and its compiler might encounter. If you don't see your question here, feel free to open an issue or reach out on our discussion boards.

---

## Installation and Setup

### 1. Does FOFI work on Windows?
Currently, we haven't fully tested the compiler on Windows. Some users have reported success using [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install) with Ubuntu. We plan to add Windows support in upcoming releases, but for now, WSL2 is the safest bet.

### 2. My Node.js run fails with "ReferenceError: window is not defined"?
Make sure you're running the compiled JavaScript (`.fofi.js`) in Node.js, not a browser environment. FOFI's code generation expects a Node-like environment by default.

### 3. The compiler complains about Cabal or GHC version mismatch
Ensure your Cabal is up to date. Try: 
```bash
cabal update
```
Then re-run the build steps documented in [README.md](./README.md). If problems persist, you may need to upgrade GHC (we recommend GHC 8.10+).

### 4. "Command not found" after installing
Your system PATH may not include Cabal's bin path. Check your shell configuration (`.bashrc`, `.zshrc`, etc.) and make sure something like `~/.cabal/bin` is in your `$PATH`.

---

## Compilation and Runtime

### 1. Why do I get "Parse error" when there's a minor typo?
FOFI's parser is sensitive to keywords and punctuation (like semicolons, parentheses). A small deviation can cause parse errors. Verify your syntax carefully or consult [docs/README.md](../docs/README.md) for syntax references.

### 2. My generated ".fofi.js" is huge or unreadable
FOFI's code generator is not optimized for minimal size or readability. It emphasizes correctness first. You can use a minifier or bundler if you want to shrink the output.

### 3. Are there any plans for an REPL or interactive shell?
We're actively discussing the possibility of providing an interactive environment. This would likely come after we stabilize the compiler features.

---

## Language Features

### 1. Can I create custom data structures beyond "var" declarations?
Yes. Although still limited, you can define them as separate modules or expansions in the grammar. We intend to add a dedicated syntax for user-defined types soon.

### 2. Is pattern matching supported?
Not yet in the official grammar. We rely on if-else constructs or function expansions to handle branching. Pattern matching is on the roadmap.

### 3. Are higher-order functions or lambdas part of FOFI?
Currently, no. Our focus is on simpler imperative constructs and some functional purity. We do have partial internal handling of closures (a stepping stone to lambdas), but it's not user-facing.

---

## Debugging and Logging

### 1. How do I debug my code?
We lack a formal debugger, but you can insert `mostrar(...)` statements throughout your code or rely on node inspection tools on the generated JavaScript. Also, watch the compiler output for warnings.

### 2. The compiler doesn't show line numbers for semantic errors
This is a known shortcoming. We'd like to improve error messages to show file name, line number, and more.

---

## Future

### 1. Will concurrency or parallelism be added?
It's under consideration. The language, in theory, can be extended with concurrency primitives or messages. However, we want to ensure we have a robust single-threaded foundation first.

### 2. Any plan for official package management?
Yes, but that's after we've stabilized the standard library design. We see the need for a package manager akin to npm or cargo for stable distribution of FOFI libraries.

### 3. Where to report bugs or request features?
Please open an issue in our GitHub repository. The more details you include (OS, GHC/Cabal versions, minimal code snippet) the faster we can fix or address your request.

We hope this FAQ helps you navigate FOFI's quirks and potential pitfalls. If you're still stuck, feel free to reach out. Happy coding!
