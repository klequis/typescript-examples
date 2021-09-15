Source: [The TypeScript Handbook: Narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-in-operator-narrowing)


## Type Guard

```ts

function padLeft(padding: number | string, input: string) {
  return new Array(padding + 1).join(" ") + input;
}
```
TS will underline `padding + 1` with error `Operator '+' cannot be applied to types 'string | number' and 'number'.`

The fix is to use an `if`

```ts
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return new Array(padding + 1).join(" ") + input;
  }
  return padding + input;
}
```

> My take: The fact that the type on `padding` was a untion `number | string` indicates a typeguard was needed.
> TypeScript understands `typeof`


## Example

The `x === y` check works because the only time that `x: string | number` could be strictly equal to `y: string | boolean` is if they are both strings.

```ts
function example(x: string | number, y: string | boolean) {
  if (x === y) {
    // We can now call any 'string' method on 'x' or 'y'.
    x.toUpperCase();
          
    // (method) String.toUpperCase(): string
    y.toLowerCase();
          
    // (method) String.toLowerCase(): string
  } else {
    console.log(x);
               
    // (parameter) x: string | number
    console.log(y);
               
    // (parameter) y: string | boolean
  }
}
```
