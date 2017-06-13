---
title: "3 LightScript features I want when I write JavaScript"
date: 2017-06-11
---

## 3 LightScript features I want when I write JavaScript

[LightScript](http://lightscript.org) is a compile-to-js language with the semantics of JavaScript and a cleaned-up syntax. It has many similarities to [CoffeeScript](http://coffeescript.org) as a language and as a project.

CoffeeScript, however, has a problem. JavaScript took the nice language features of CoffeeScript and added more useful features like `import`, so CoffeeScript is now behind in terms of features. LightScript is more strictly a superset of JavaScript and is implemented as a fork of [Babel](https://babeljs.io) so it works with the same tools as JavaScript.

Additionally, as JavaScript got better, the liberties CoffeeScript took with syntax became less compelling. I find that the implicitness of CoffeeScript causes surprises. LightScript takes less liberties. Function calls need parenthesis and objects literals need curly braces.

For me, LightScript is worthwhile because JavaScript's backwards compatibility means some syntactic cruft will never be fixed.

Here are 3 LightScript features that offer improvements over JavaScript.

## 1. Optional control flow parenthesis

```javascript
// JavaScript
if (input.checked) {
  alert('Checked')
}
```

becomes

```javascript
// LightScript
if input.checked {
  alert('Checked')
}
```

One would only need parenthesis when the test is multiple lines.

## 2. Automatic `const`

```javascript
const message = 'Welcome to my site.'
```

becomes

```javascript
message = 'Welcome to my site.'
```

In JavaScript, it's silly that an unqualified assignment is a global variable.

The only time I don't use `const` is conditionals such as:

```javascript
let totalCost
if (purchase === null) {
  totalCost = 0
} else {
  totalCost = purchaseFee + purchase.cost
}
```

which would be unnecessary with `if` expressions...

## 3. `if` expression

```javascript
alert(
  input.checked ?
  'Checked' :
  'Not checked'
)
```

becomes

```javascript
alert(if input.checked {
  'Checked'
} else {
  'Not checked'
})
```

I find ternary operator to be quite useful but I don't like its syntax in JavaScript. Especially since when a ternary is spread over multiple lines, there's no clear convention as to where the symbols should go.

<br>

LightScript also has 1-line ternary expressions:

```javascript
alert(if input.checked: 'Checked' else: 'Not checked')
```

However I would prefer:

```javascript
alert(if input.checked 'Checked' else 'Not checked')
```

At least the second colon should not be necessary.

Clearly the preferred syntax isn't obvious, which might indicate this feature isn't ready. In my version for example, does the combination of optional control flow parenthesis and `if` expressions cause ambiguity?

This is a case where the CoffeeScript has a consistent, readable solution. But it would look out of place if ported exactly.

```coffeescript
# CoffeeScript
alert(
  if input.checked
    'Checked'
  else
    'Not checked'
)

# Or inline:

alert(if input.checked then 'Checked' else 'Not checked')
```

Considering the lack of a clear improved 1-line syntax, the current JavaScript ternary operator is not bad for 1-line use cases.

```javascript
alert(input.checked ? 'Checked' : 'Not checked')
```

<br>

Here's a more complex example to consider.

```javascript
let targets = []

if target instanceof String {
  targets = toArray(document.querySelectorAll(target))
} else if target instanceof Object && target.nodeName instanceof String {
  targets = [target]
}
```

becomes

```javascript
targets = if target instanceof String {
  toArray(document.querySelectorAll(target))
} else if target instanceof Object && target.nodeName instanceof String {
  [target]
} else {
  []
}
```

Though it's possible to avoid reassignment using chained ternaries, it's not very readable.

One counterargument: unlike in conventional `if` statements, conditional side effects or local variables might not be possible in `if` expressions. In those cases, a helper function might be in order.

## LightScript Status

All of these language features are available in LightScript as of now, which is great!

Many other features are available as well, but more LightScript features means a steeper learning curve and sometimes multiple ways to do the same thing. A style guide would help by identifying the idiomatic way, but so far I haven't found the trade-offs of additional features to be compelling.

For example, comprehensions are available in LightScript, but in JavaScript, `map` and `filter` are standard for arrays and `reduce` works for objects (see [appendix 2 below](#appendix-2-using-reduce-to-accomplish-object-comprehensions)), so in my opinion no special syntax is necessary.

Additionally, I like Python's use of significant whitespace, but it's not a big deal that JavaScript uses curly braces.

## Honorable mention: `==` and `!=` without type conversion

It's a standard practice to never use `==` in JavaScript but `===` is annoying to type and looks weird.

```javascript
1 + 1 === 2
```

becomes

```javascript
1 + 1 == 2
```

However, `equals` can be implemented in userspace and has benefits over `==`:

```javascript
{} === {} // false
R.equals({}, {}) // true
```

([Docs for Ramda `equals`](http://ramdajs.com/docs/#equals))

As such, it's not necessary to change this on the language level. Though maybe `==` could be aliased to `R.equals`? ![:starstruck:](/img/star-struck.png){:height="20px" style='vertical-align: middle'}

---

#### Appendix 1: Is `if` obsolete in application code? If so, no need to fix it

If we don't need `if` in application code, there's no real need to worry about making the parenthesis optional (#1 above).

We can avoid `if` in by making values lazy and passing them to a sort of `if` function:

```javascript
// Library
function when(predicate, f) {
  if (predicate) {
    f()
  }
}

// Application
function alertChecked() {
  alert('Checked')
}

when(input.checked, alertChecked)
```

This has an interesting effect on the program: the side effects are forced to be separate.

However, the verbosity is troublesome, and most anybody reading this would roll their eyes and tell me to just use `if`.

---

#### Appendix 2: using `reduce` to accomplish object comprehensions

Python dictionary comprehensions:

```python
months = ['January', 'February']

{
    index + 1: month
    for index, month in enumerate(months)
}
# {1: 'January', 2: 'February'}
```

Can be translated to:

```javascript
// Vanilla JavaScript approach
const months = ['January', 'February']

months.reduce((values, month, index) => {
  values[index + 1] = month
  return values
}, {})
// {1: "January", 2: "February"}


// Using a library like Ramda
months.reduce((values, month, index) => (
  R.assoc(index + 1, month, values)
), {})


// One attempt to further remove boilerplate:

// Library
const comprehension = (f, array) => (
  array.reduce((obj, item, index) => (
    R.assoc(...f(item, index), obj)
), {})

// Application
comprehension((month, index) => [
  index + 1, month
], months)
```
