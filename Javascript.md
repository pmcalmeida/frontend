### Javascript: Use colors from our Color Palette

Avoid the 50 shades of gray by sticking with our color palette.

### Javascript: Coding style

Our coding style conventions are defined by our eslint and prettier rules. 

Check [https://github.com/dashdash/eslint-config](https://github.com/dashdash/eslint-config) to have a undestand of our eslint rules.

### Javascript: Use default arguments instead of short circuiting or conditionals

Default arguments are often cleaner than short circuiting. Be aware that if you use them, your function will only provide default values for undefined arguments. Other "falsy" values such as '', "", false, null, 0, and NaN, will not be replaced by a default value.

```js
Bad:
function createMicrobrewery(name) {
  const breweryName = name || "Hipster Brew Co.";
  // ...
}

Good:
function createMicrobrewery(name = "Hipster Brew Co.") {
  // ...
}
```

### Javascript: Limit function arguments to two or less

Limiting the amount of function parameters is incredibly important because it makes testing your function easier. Having more than three leads to a combinatorial explosion where you have to test tons of different cases with each separate argument.

One or two arguments is the ideal case, and three should be avoided if possible. Anything more than that should be consolidated. Usually, if you have more than two arguments then your function is trying to do too much. In cases where it's not, most of the time a higher-level object will suffice as an argument.

Since JavaScript allows you to make objects on the fly, without a lot of class boilerplate, you can use an object if you are finding yourself needing a lot of arguments.

To make it obvious what properties the function expects, you can use the ES2015/ES6 destructuring syntax. This has a few advantages:

1. When someone looks at the function signature, it's immediately clear what properties are being used.
2. Destructuring also clones the specified primitive values of the argument object passed into the function. This can help prevent side effects. Note: objects and arrays that are destructured from the argument object are NOT cloned.
3. Linters can warn you about unused properties, which would be impossible without destructuring.

```js
Bad:
function createMenu(title, body, buttonText, cancellable) {
  // ...
}

Good:
function createMenu({ title, body, buttonText, cancellable }) {
  // ...
}

createMenu({
  title: "Foo",
  body: "Bar",
  buttonText: "Baz",
  cancellable: true
});
```

### Javascript: Don't use flags as function parameters

Flags tell your user that this function does more than one thing. Functions should do one thing. Split out your functions if they are following different code paths based on a boolean.

```js
Bad:
function createFile(name, temp) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}

Good:
function createFile(name) {
  fs.create(name);
}

function createTempFile(name) {
  createFile(`./temp/${name}`);
}
```
