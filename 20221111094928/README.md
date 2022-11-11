# Typescript: basics

Return type on an arrow function

```js
const greet = (name: string): string => {
  return `Hi ${name}`
}
console.log(greet("Dan"))
```

Prefer `type` or `interface` when return types are more complicated.

```js
type Player = {
  name: string;
  number: number;
}

const getPlayer = (): Player => ({
  name: "Jordan"
  number: 23
})
```

If your function could return different types, use a `union`

```js
function getNameOrNumber(name: string): string|number {
  if name === "Jordan" {
    return 23
  }
  return "who cares"
}
```

Tags:

    #typescript #programming
