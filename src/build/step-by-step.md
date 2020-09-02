# Step by Step 👣

Building a macro involves having a relatively concrete idea of the source structure and resulting structure. If the source structure is already existent ([JSON](https://google.github.io/styleguide/jsoncstyleguide.xml), [HTML](https://google.github.io/styleguide/htmlcssguide.html), etc) there should already exist a style guide. If there doesn't already exist a style guide, we recommend that you take time to analyze the structures - even write a guide yourself if necessary. This will reduce the bugs during the parsing step. For this example, we will create a parser for the `bee` structure found in the examples.

## Bee analysis (for this example)

The `bee` number system is defined like an integer where every number is replaced by a `b` followed by n < 10 `e`s. For example, `be b bee beeee` would be `1024`. We would like to convert this "esoteric" code back to the integer. Therefore, for parsing, we should seperate the `bee...` and count the number of `e`s. We can then combine those counts to create the number value.

## Import

This package includes all the necessary functions at the top module. Therefore, all the classes/values that you will need can be imported as follows:

```typescript
import { ... } from "proc_macro";
```

The rest of the step be step will assume that the required classes are imported.

## Making the Parsing Class

We recommend that you keep parsing classes in seperate files. They should also all be subclasses of `Expression`. In this example, a good parsing name could be `Bee`, therefore, we could create the following in `bee.ts`:

```typescript
export default class Bee extends Expression {
    // Value is going to contain the integer value.
    value: string

    constructor(value: string) {
        this.value = value;
    }
```

Every `Expression` should override the `static parse` and the `toJavaScript` methods. Let's tackle the `parse` first. The function takes in a tokenized code and outputs `this` object:

```typescript
public static parse(ts: TokenStream): Bee {
```

Now, we need to make the logic for the parsing. Using the analysis from before, we expect identifiers until the `End` of stream therefore:

```typescript
let accumulator = "";

while(!(ts.peek`${End}`)) {
```

We can then try to parse the identifiers:

```typescript
let [bee] = ts.parse`${Ident}`;
```

We can use regex to determine if the identifier value is `bee...` else throw an error:

```typescript
if(!/^[Bb]e*$/.test(bee.value)) throw ts.error("Passed text is not bee.");
```

We expect also all `bee...` to have less than 10 `e` (due to integer definition):

```typescript
if(bee.value.length > 10) throw ts.error("Bee should be smaller than 11 letters.");
```

Finally, we can add the number to the string number accumulator:

```typescript
accumulator += bee.value.length - 1;
}
```

And return the Bee object:

```typescript
return new Bee(accumulator);
}
```

We can then tackle the `toJavaScript` which in this case will simply return the value (you can use `quote` to remove the number of `toJavaScript` to use):

```typescript
public toJavaScript(): string {
    return quote`${this.value}`;
}
}
```
## Making the Parsing Function

The parsing function will englobe the parsing objects. This should be in a main file like `index.ts`, not exported. Given we are already englobing everying with another object, the parsing function can be as simple as:

```typescript
const beeParser = (tokenStream: TokenStream): string => {
    let [bee] = tokenStream.parse`${Bee}`; // or Bee.parse(tokenStream);
    return bee.toJavaScript();
}
```

## Making the Macro

The macro is simply the parsing function englobed by the `proc_macro` function. You can assign it to a const that is exported:

```typescript
export const bee = proc_macro(beeParser);
```

You should now be able to use the macro using the following structure (where `b` will become the output of the macro):

```typescript
let b = eval(bee`be b bee beeee`);

// Should give `1024`!
console.log(b);
```

Congrats, you now have a working macro 🎈. This said, it is possible that it fails...

## Testing

You should really unit test your macros. You will often find that you failed to consider an edge case for your input (or simply validate your logic). [Jest](https://jestjs.io/) is a great package to do so:

```
npm install --save-dev jest
```

You can then perform a unit test in a `.test.js` or `.test.ts` file:

```typescript
test("Bee ident should be less than 10 long.", () => {
    expect(bee`beeeeeeeeee`).toThrow(Error);
});
```

In this case, it could be possible that previous test failed, meaning your previous logic was incorrect. For this example, we could have written `bee.value.length >= 10` previously.

You should have unit tests for most of your edge cases. You might also want to look into a fuzzer package that can automate some of this process.

You should now have a fully working macro 🎂. You should now be able to create your own macros using the templates. You can also look at more examples!