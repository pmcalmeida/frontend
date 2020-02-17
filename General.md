### Choose meaningful names

Variable and function names should clearly transmit it's responsibility through it's name.

### Favor pure functions

Pure functions are easier to test and to reason with. You can read them in isolation and understand it's intent.

### **Follow the Single Responsibility Principle**

Do not add logic lazily where its more convenient try to understand where the responsibility for such logic lies, and make an effort to place it there. Or at least pave the way so that it can be moved there ASAP.

### Avoid high complexity methods

Keep an eye for the *Cyclomatic complexity* of your methods, avoid to go over X.

*Cyclomatic complexity* is a software metric used to indicate the complexity of a program. It is a quantitative measure of the number of linearly independent paths through a program's source code.

### Follow the "boy-scout" rule

You don't have to fully refactor every piece of code you change, but make sure that you always leave the place cleaner than you found it.

*"Leave your code better than you found it."*

### Avoid "clever" abstractions

Simple duplication sometimes is preferable to a clever and hard to maintain abstraction. As a rule of thumb only make an effort to abstract if you duplicate the same code three or more times.

### Extract strings, “magic numbers”, hard-coded values

Reading a sum between magic numbers brings no meaning to the reader, if you replace such numbers with a variable with a meaningful name the code will be easier understood by the reader.

### Use guard clauses and early return instead of nested conditions

You have a group of nested conditionals and it’s hard to determine the normal flow of code execution:

```js
function getPayAmount(options) {
  let result;
  if (options.isDead) {
    result = deadAmount();
  } else {
    if (options.isSeparated) {
      result = separatedAmount();
    } else {
      if (options.isRetired) {
        result = retiredAmount();
      } else {
        result = normalPayAmount();
      }
    }
  }
  return result;
}
```

Isolate all special checks and edge cases into separate clauses and place them before the main checks. Ideally, you should have a “flat” list of conditionals, one after the other:

```js
function getPayAmount(options) {
  if (options.isDead) {
    return deadAmount();
  }
  if (options.isSeparated) {
    return separatedAmount();
  }
  if (options.isRetired) {
    return retiredAmount();
  }
  return normalPayAmount();
}
```

### Do not re-invent the wheel

We have util libs such as lodash, rxjs and react-use. Before creating a custom hook or a custom helper, make sure they're not already available in one of our utils libs.

### Files should be slug-case

TO BE ADDED...

### Avoid disabling the static analysis tool

TO BE ADDED...

### Only comment things that have business logic complexity.

TO BE ADDED...

### Use feature flags

TO BE ADDED...

### Avoid at all costs big Pull Requests

TO BE ADDED...

### In doing a code review, you should make sure that:

- The code is well-designed.
- The functionality is good for the users of the code.
- Any UI changes are sensible and look good.
- Any parallel programming is done safely.
- The code isn’t more complex than it needs to be.
- The developer isn’t implementing things they *might* need in the future but don’t know they need now.
- Code has appropriate unit tests.
- Tests are well-designed.
- The developer used clear names for everything.
- Comments are clear and useful, and mostly explain *why* instead of *what*.
- Code is appropriately documented (generally in g3doc).
- The code conforms to our style guides.
