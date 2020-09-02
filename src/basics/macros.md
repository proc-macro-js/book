# Macros ⚙️

Macros are metaprogramming structures that convert usually smaller/comprehensive code into longer code. Programming languages implement these structures to allow for the Don't Repeat Yourself (DRY) principle. 

A common example of these are `constants` like `const PI = 3.141592...`. In compiled languages, the "macro" `PI` is replaced with the value of PI at compile time (instead of having to write the value of PI everywhere). 

This package uses the JIT compiler, therefore macros are interpreted at runtime. We still attempt to closely replicate the compilation/debugging of the [proc_macro](https://doc.rust-lang.org/proc_macro/)s in [Rust](https://www.rust-lang.org/).

## Example

Here is the use of an arbitrary `macro` macro:
```typescript
let v = eval(macro`ident, {}`);
```