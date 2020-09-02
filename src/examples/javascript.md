# JavaScript 🟨

Parsing from JavaScript back to JavaScipt. This demonstrates the most simple parser (which doesn't parse at all).

```typescript
import { TokenStream, proc_macro } from "proc_macro";

const javaScriptParser = (tokenStream: TokenStream): TokenStream => {
    return tokenStream;
};

const js = proc_macro(javaScriptParser);

let j = eval(js`1 + 1`);

// Should give `2`!
console.log(j);
```