# AnyPEG

AnyPEG is a vision for an universal PEG-like parser generator.

---

## Vision

AnyPEG should become a parser generator with this feature set:

- Parser generator implemented in Python
- Focus on PEG-like parsers with left-recursion and backtracking
- Nice, unbloated grammar definition language
- Built-in Abstract syntax tree definition
- Optional scannerless parsing
- Code generator using a template language and engine
- Efficient, stand-alone PEG parser generation for multiple target languages
  - should work without external dependencies, raw code construction (Yacc-style)
  - Python
  - C
  - C++
  - Rust
  - JavaScript
  - ... anything else (above is a personal favorite stack)
- Nice error reporting

## Background

Hello, my name is Jan Max Meyer. I'm a senior software developer, and heavily interested into topcis on parsing, compiler construction and language engineering.

I'm following `pegen`s development since its first lines of code made by Guido van Rossum in 2020 regarding [PEP-617](https://peps.python.org/pep-0617/).<br>
Since then, I became impressed by the simple but efficient algorithm and the fun in writing parsers again, as using left-recursive PEGs, there's no need to deal with limitations of the grammar or the parser generator, and rules become more clear due to their sequential ordering.

Based on `pegen`'s nice description of the algorithm, I've started working on [Tokay](https://github.com/tokay-lang/tokay) in 2020, written in Rust. Tokay is a programming language for ad-hoc parsing, and based on a similar technique like pegen's algoroithm, but it's a tool for implementing parsers and data-extractors in the style of awk-programs, with nice features influenced by Rust and Python. Therefore it is a project on its own, without a concurrency, as it isn't a code generator, but an entire language on its own, with some neat features currently under development.

Since 2007, I've also worked on [UniCC](https://github.com/phorward/unicc), written in C. It was my first vision of a scannerless LALR(1) parser generator, not limited to one particular programming language. IMHO, I've successfully matched this goal, althought UniCC has many disadvantages, especially because its implemented in C, its syntax is ugly and it's impractical to use in modern projects, because it doesn't use a template engine to construct the code and renders endless parse tables into the resulting program. A complete rewrite of UniCC has been abandoned in 2018, as it went into a similar direction as its predecessor, and limits where too high. LALR(1) is still a very efficient parsing algorithm, but Python since 3.9, Tokay and other implementations show, that PEG-parsers are also very efficient on modern architectures and the better choice to fit both the needs of the developer and the user.

`anypeg` shall become a tool integrating ideas and features from both of my projects, Tokay and UniCC, and its origin, Python, but with the goal to generate parsers language-independently and using the PEG-approach. Create a grammar and AST notation once, and compile it into different target languages, with all required tooling on hand.

And, for sure, maybe this highly-scaled and improved enhancement of `pegen` can still be used to provide the core parser for Python?

## Todo

This is a todo list I've started, and which is still unfinished.

- [ ] General
  - [ ] Use most current Python (3.10 + 3.11) only
  - [ ] generated parsers should be backward-compatible, probably Python 3.9 (but why?)
- [ ] Modularization
  - [ ] Merge current feature set of CPythons peg_generator and pegen
  - [ ] Move utility scripts to subfolders
    - [ ] first_sets.py
    - [ ] grammar_visualizer.py
  - [ ] The Grammar class should not be modified by ParserGenerator
    - [ ] left_recursive-flag
  - [ ] Tokenizer
    - [ ] part of the target language
    - [ ] backtracking features
- [ ] Features
  - [ ] Redefine meaning of keyword and soft keyword (equivalent to Tokay's Match and Touch string token)
  - [ ] Remove Tokenizer class and rely on builtins
  - [ ] Think about generics like in [Tokay](https://tokay.dev)?
  - [ ] AST notation, automatic AST construction
  - [ ] Built-in Tokens (like in [Tokay](https://tokay.dev))
    - [ ] Int
    - [ ] Float
    - [ ] Word
    - [ ] Ident
  - [ ] Scannerless parsing
    - [ ] Span over rules (maybe mark them as sticky, or so)
    - [ ] `_` and `__` for whitespace (like in [Tokay](https://tokay.dev))
  - [ ] Code generation using a template engine
    - [ ] [Logics/Vistache](https://github.com/viur-framework/logics) (which can be re-implemented in pegen on its own)
    - [ ] or Jinja2, as it's well known, but a third party tool
- [ ] Generators
  - [ ] Python
  - [ ] C (stand-alone, without CPython)
  - [ ] C++ (stand-alone)
  - [ ] JavaScript
  - [ ] Rust
