# proc_macro.js

**proc_macro.js** is a JavaScript/TypeScript implementation of [Rust](https://www.rust-lang.org/) procedural macros 🔥. The goal of this project is to combine the ideas from [syn](https://github.com/dtolnay/syn), [quote](https://github.com/dtolnay/quote), [proc_macro](https://doc.rust-lang.org/proc_macro/), and [proc_macro2](https://docs.rs/proc-macro2/1.0.19/proc_macro2/) in one comprehensive parsing package.

proc_macro.js is free and open source, you can find the source code on [GitHub](https://github.com/alexandre-lavoie/proc_macro.js). Issues and feature requests can be posted on the [GitHub issue tracker](https://github.com/alexandre-lavoie/proc_macro.js/issues).

## Limitations

Unlike [sweet.js](https://www.sweetjs.org/), the goal is to write hygenic/unhygenic macros that require only vanilla JavaScript. This would allow to run this library anywhere. This comes with the caveat of JIT compilation and [tagged templates](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals).

## License

proc_macro.js is released under the [MIT License](https://github.com/alexandre-lavoie/proc_macro.js).