# Tokenize 🔤

Tokenizing involves coverting plain code into a simpler representation for parsing. This packages converts all tokens into four types (TokenTree). This is similar to the [Rust](https://www.rust-lang.org/) [proc_macro](https://doc.rust-lang.org/proc_macro/) package:

- `Indent`: An identifier (variable name, condition statements, etc) represented as a string.
- `Punct`: A non-numeric/non-alpha character used to seperate inputs (addition, substraction, etc) which can be alone or joint.
- `Literal`: A string or numeric value.
- `Group`: A collection of tokens delimited by brackets, parentheses, or braces.

Multiple tokens are collected in a `TokenStream` for parsing.

## Example

The following input code:

```
x += 1;
```

Would convert to the following `TokenStream` (represented in Lisp like notation):

```
(TokenStream (Ident x) (Punct joint +) (Punct alone =) (Literal number 1) (Punct alone ;))
```