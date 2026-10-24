# JavaScript Operators

## 1. Comparison Operators

Comparison operators compare two values and return a boolean: `true` or `false`.

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `>` | Greater than | `10 > 5` | `true` |
| `<` | Less than | `10 < 5` | `false` |
| `>=` | Greater than or equal to | `10 >= 10` | `true` |
| `<=` | Less than or equal to | `7 <= 6` | `false` |

### Comparing strings and numbers

When comparing a string with a number, JavaScript attempts to convert the string to a number.

```js
console.log("20" > 3);  // true
console.log("10" > 20); // false
console.log("12abc" > 3); // false
```

In the last example, `"12abc"` cannot be converted into a valid number, so the comparison involves `NaN` and returns `false`.

### Comparing two strings

When both operands are strings, JavaScript compares them lexicographically, using their UTF-16 code units.

```js
console.log("banana" > "apple"); // true
console.log("apple" > "Apple");  // true
console.log("12" > "3");         // false
```

String comparison proceeds character by character until the characters differ or one string ends.

**Important:** Numeric-looking strings are not automatically converted into numbers when compared with other strings.

```js
console.log("10" > "2"); // false
console.log("10" > 2);   // true
```

The first comparison is between strings. The second converts `"10"` to the number `10`.

## 2. Equality and Inequality

JavaScript provides loose and strict equality operators, along with their inequality counterparts.

| Operator | Meaning | Type coercion |
|---|---|---|
| `==` | Loose equality | May convert types |
| `===` | Strict equality | Does not convert types |
| `!=` | Loose inequality | May convert types |
| `!==` | Strict inequality | Does not convert types |

### Loose inequality: `!=`

The `!=` operator returns `true` when two values are not equal after the applicable type conversions.

```js
console.log(5 != "5");   // false
console.log(0 != false); // false
console.log(5 != 6);     // true
```

In these examples, `"5"` is converted to `5`, and `false` is converted to `0`.

### Strict inequality: `!==`

The `!==` operator checks whether two values are different without converting their types.

```js
console.log(5 !== "5");   // true
console.log(0 !== false); // true
console.log(5 !== 6);     // true
console.log(5 !== 5);     // false
```

A number and a string containing the same digits are strictly unequal because their types differ.

### `==` versus `===`

Prefer strict equality (`===`) and strict inequality (`!==`) in most everyday JavaScript code. They make comparisons more predictable by avoiding implicit type conversion.

```js
console.log(5 == "5");  // true
console.log(5 === "5"); // false
```

Remember that loose equality has defined conversion rules; it does not simply compare whether two values are truthy or falsy.

## 3. Logical Operators

Logical operators are used to combine conditions and control which expressions are evaluated.

### Logical AND: `&&`

`&&` evaluates the left operand first.

- If the left operand is falsy, it returns that operand.
- If the left operand is truthy, it evaluates and returns the right operand.

When both operands are booleans, the result is `true` only when both are `true`.

```js
console.log(true && true);   // true
console.log(true && false);  // false
console.log(false && true);  // false

console.log("hello" && 42);  // 42
console.log("" && 42);       // ""
console.log(0 && "default"); // 0
```

### Logical OR: `||`

`||` evaluates the left operand first.

- If the left operand is truthy, it returns that operand.
- If the left operand is falsy, it evaluates and returns the right operand.

When both operands are booleans, the result is `true` if at least one operand is `true`.

```js
console.log(false || true);   // true
console.log(false || false);  // false

console.log("hello" || 42);   // "hello"
console.log("" || 42);        // 42
console.log(0 || "default");  // "default"
console.log(null || false);   // false
```

Notice that `||` does not guarantee a truthy result. If the left operand is falsy, it returns the right operand even when that operand is also falsy.

## 4. Short-Circuit Evaluation

Short-circuit evaluation means JavaScript evaluates only as much of a logical expression as needed to determine its result.

With `&&`, a falsy left operand prevents the right operand from being evaluated.

With `||`, a truthy left operand prevents the right operand from being evaluated.

```js
console.log(false && someFunction()); // false; function isn't called
console.log(true || someFunction());  // true; function isn't called
```

These examples assume `someFunction` is a defined function. Since the left operand determines the result, JavaScript never attempts to call it.

### Using `||` for default values

The OR operator is commonly used to provide a fallback when a value is falsy.

```js
const username = "";
const displayName = username || "Guest";

console.log(displayName); // "Guest"
```

Be careful: this also replaces valid values such as `0` and `false`, because they are falsy.

## 5. Practice Exercises

Try predicting the results before running each snippet.

### Exercise 1: Comparisons

```js
console.log(8 >= 8);
console.log("15" < "3");
console.log("15" < 3);
console.log("hello" > "Hello");
```

### Exercise 2: Equality

```js
console.log(10 != "10");
console.log(10 !== "10");
console.log(false == 0);
console.log(false === 0);
```

### Exercise 3: Logical operators

```js
console.log("JS" && "Learning");
console.log(0 || 100);
console.log(null && "Hello");
console.log("Ready" || "Start");
```

### Exercise 4: Short-circuiting

Explain why the second log statement does not print `"Called!"`.

```js
function greet() {
  console.log("Called!");
  return true;
}

console.log(false && greet());
console.log(true || greet());
```

## Key Takeaways

- Comparison operators such as `>`, `<`, `>=`, and `<=` return booleans.
- Two strings are compared lexicographically; a string compared with a number may be converted to a number.
- `!=` and `==` may perform type conversion; `!==` and `===` do not.
- `&&` returns the first falsy operand, or the last operand if all operands are truthy.
- `||` returns the first truthy operand, or the last operand if all operands are falsy.
- Both `&&` and `||` use short-circuit evaluation.
- Prefer `===` and `!==` for predictable equality checks.
