# Parse 🛥️

Parsing converts a `TokenStream` to commands. In compiled languages, this step usually outputs to Assembly. In the case of this package, code is converted back to JavaScript.

The `TokenStream` class has useful functions to make parsing more efficient. 

## Parsing

The `parse` function can be used to extract token(s) from the stream (expected them to follow this pattern). You can use the function to extract a specific type:

```typescript
let [ident] = tokenStream.parse`${Ident}`;
```

You can parse a specific token using:

```typescript
tokenStream.parse`<`;
```

You can combine multiple tokens into a single parse:

```typescript
let [ident, literal] = tokenStream.parse`let ${Ident} = ${Literal};`;
```

## Peeking

You can use the `peek` function to check if the following tokens has a certain pattern (similar uses as `parse`):

```typescript
if(tokenStream.peek`<${Ident}></${Ident}`)) {
    ...
}
```

## Error handling

You can use the `error` function to throw more accurate debug errors:

```typescript
throw tokenStream.error("Expected `let`.");
```

Would lead to a debug similar to the following:

```
|
|   const x = 1;
|   ^
|   |
|   Expected `let`.
|
```

## Raw stream (more advanced)

You can get the stream using `stream` which will let you navigate the raw tokens:

```typescript
for(let token of tokenStream.stream) {
    ...
}
```

You can then use `next` to extract the next raw token(s).