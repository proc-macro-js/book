# Templates 🏗️

Your macro will usually have at minimum the follow:

## Parsing Class

A parsing class that will convert the tokens into a code (should be defined in it's own file, default exported):

```typescript
import { TokenStream, Expression } from "proc_macro";

export class Expr extends Expression {

    // Parameters for type.

    constructor(/* Params */) {
        // Insert object parameters init.
    }

    public static parse(ts: TokenStream): Expr {
        // Insert parsing logic.
    }

    public static toJavaScript(): string {
        // Insert toJavaScript string logic.
    }
}
```

## Parsing Function

A function that will passed for the proc_macro (should be defined in a main file, not exported):

```typescript
import { proc_macro, TokenStream } from "proc_macro";
// import Expr from "./expr.ts"

const exprParser = (tokenStream: TokenStream): string | TokenStream => {
    // Insert parsing logic toJavaScript or toToken logic.

    // let [expr] = tokenStream.parse`${Expr}`;
    // return expr.toJavaScript();
}
```

## Macro

You can put the macro after the parsing function (should be defined with parsing function, exported):

```typescript
export const expr = proc_macro(exprParser);
```