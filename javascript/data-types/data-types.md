# JavaScript Data Types

## 1. Primitive Data Types

JavaScript has seven primitive data types:

- `number` — represents numbers, including integers, decimals, `NaN`, and `Infinity`.
- `string` — represents text enclosed in single quotes, double quotes, or backticks.
- `boolean` — represents either `true` or `false`.
- `undefined` — represents a value that has not been assigned or is otherwise unavailable.
- `null` — represents the intentional absence of a value.
- `bigint` — represents integers larger than the range that `number` can safely represent.
- `symbol` — represents a unique value commonly used as an object property key.

### What about `object`?

`object` is also a data type in JavaScript, but it is non-primitive.

Arrays, ordinary objects, and many other structures are objects. An array is a special kind of object with additional behavior, such as indexed elements and array-specific methods.

Functions are also objects, although they have special callable behavior.

## 2. The `typeof` Operator

`typeof` is used to determine the type category of a value in JavaScript. It returns a string describing the type.

```js
let age = 23;
let name = "Manjot";
let isLearning = true;

console.log(typeof age);        // "number"
console.log(typeof name);       // "string"
console.log(typeof isLearning); // "boolean"
```

### Weird JavaScript Behaviour

```js
console.log(typeof null);      // "object"
console.log(typeof []);        // "object"
console.log(typeof {});        // "object"
console.log(typeof undefined); // "undefined"
```

There are a few important things to understand here:

- `typeof null` returns `"object"` because of a historical JavaScript bug that has been retained for backward compatibility.
- `typeof []` returns `"object"` because arrays are objects in JavaScript.
- `typeof {}` returns `"object"` because ordinary objects belong to the object type category.
- `typeof undefined` returns `"undefined"`.

Remember that `typeof` returns a string, not the data type itself.

### Checking Whether a Value Is an Array

Since `typeof` returns `"object"` for arrays, it cannot reliably distinguish arrays from ordinary objects.

JavaScript provides `Array.isArray()` for this purpose:

```js
console.log(Array.isArray([]));   // true
console.log(Array.isArray({}));   // false
console.log(Array.isArray("hi")); // false
```

`Array.isArray()` returns a Boolean indicating whether the supplied value is an array.

### The `bigint` Type

BigInt is used to represent integers beyond the range that JavaScript's `number` type can safely represent.

```js
const bigNumber = 9007199254740993n;

console.log(typeof bigNumber); // "bigint"
```

The `n` suffix indicates a BigInt literal.

Ordinary numbers have a maximum safe integer of `9007199254740991`. BigInt allows us to work with larger integers without losing integer precision, subject to available memory.

## 3. `null` vs. `undefined`

```js
let a;
let b = null;

console.log(a); // undefined
console.log(b); // null
```

- `undefined` commonly means that a variable has been declared but has not been assigned a value.
- `null` commonly represents an intentional absence of a value.

The difference is that `undefined` often indicates that a value hasn't been provided, whereas `null` is commonly used to explicitly represent the absence of a value.

Both are primitive values in JavaScript.

```js
console.log(typeof a); // "undefined"
console.log(typeof b); // "object"
```

Remember that `typeof null` returning `"object"` is a historical quirk. It does not mean that `null` is actually an object.

## 4. Explicit Type Conversion

Explicit type conversion means that we deliberately tell JavaScript to convert a value from one type to another.

Some common conversion functions are `Number()`, `String()`, and `Boolean()`.

```js
let a = "42";
let b = Number(a);
let c = Boolean(a);

console.log(typeof a); // "string"
console.log(typeof b); // "number"
console.log(typeof c); // "boolean"

console.log(b); // 42
console.log(c); // true
```

The string `"42"` is converted into the number `42`, while the non-empty string is converted into the Boolean value `true`.

Converting `a` does not change the original variable. The converted value is stored in `b`, while `a` remains the string `"42"`.

More examples:

```js
console.log(Number("123"));    // 123
console.log(Number("hello"));  // NaN
console.log(Number(""));       // 0

console.log(String(42));       // "42"
console.log(Boolean(0));       // false
console.log(Boolean("hello")); // true
```

`NaN` stands for *Not a Number*. It is a special numeric value used when a numeric operation or conversion does not produce a valid number.

## 5. Truthy and Falsy Values

A **truthy** value is a value that becomes `true` when converted to a Boolean.

A **falsy** value is a value that becomes `false` when converted to a Boolean.

### Falsy Values

The falsy values in JavaScript are:

- `false`
- `0`
- `-0`
- `0n`
- `""` (empty string)
- `null`
- `undefined`
- `NaN`

Everything else is truthy, including empty arrays and empty objects.

### Examples

```js
console.log(Boolean("false")); // true
console.log(Boolean(""));      // false
console.log(Boolean(0));       // false
console.log(Boolean(-1));      // true
console.log(Boolean([]));      // true
console.log(Boolean({}));      // true
```

The string `"false"` is truthy because it is a non-empty string. JavaScript does not interpret the text inside a string when converting it to a Boolean.

Likewise, empty arrays and empty objects are truthy values.

Remember: **an empty value is not necessarily a falsy value.**

## 6. Implicit Type Coercion

Implicit type coercion occurs when JavaScript automatically converts values from one type to another while evaluating an expression.

The result can depend on the operator being used.

### The `+` Operator

The `+` operator can perform either numeric addition or string concatenation.

When string concatenation occurs, values are converted to strings and joined together.

```js
console.log("5" + 2);  // "52"
console.log("10" + 5); // "105"
```

Here, JavaScript converts the numbers to strings and joins them with the existing strings.

### Other Arithmetic Operators

Operators such as `-` and `*` perform numeric operations, so JavaScript converts operands to numbers when possible.

```js
console.log("5" - 2);  // 3
console.log("10" * 5); // 50
```

JavaScript converts the strings into numbers before performing the operations.

### More Examples

```js
console.log("123" - 0); // 123
console.log("hello" * 2); // NaN
console.log(Number("hello")); // NaN
console.log(Number("")); // 0
```

`Number("hello")` is an example of explicit conversion, whereas `"123" - 0` relies on implicit coercion.

### Why Can Implicit Coercion Be Risky?

Relying on implicit coercion can lead to unexpected outputs and application bugs.

For example, if an application expects a number but receives a string, the `+` operator might concatenate the values instead of adding them.

```js
let quantity = "10";
let bonus = 5;

console.log(quantity + bonus); // "105"
```

If we intended to perform numeric addition, we should convert the input explicitly:

```js
let quantity = "10";
let bonus = 5;

console.log(Number(quantity) + bonus); // 15
```

In real applications, we should validate untrusted input as well as convert it when necessary. Explicit conversion helps make our intentions clear, but it does not replace input validation.

## 7. Equality: `==` vs. `===`

JavaScript has two commonly used equality operators.

- `==` is the loose equality operator. It can convert operands before comparing them.
- `===` is the strict equality operator. It does not coerce operands of different types before comparing them.

### Examples

```js
console.log("1" == 1);  // true
console.log("1" === 1); // false
```

With `==`, JavaScript converts the string `"1"` into a number before comparing the values.

With `===`, the string and number are different types, so the comparison returns `false`.

### Why Is `===` Generally Preferred?

Strict equality makes comparisons more predictable because it avoids implicit type coercion between different types.

For this reason, `===` is generally preferred in application code unless loose equality is deliberately needed.

However, strict equality is not a substitute for input validation or correct application logic.

## 8. Quick Reference

### Explicit Type Conversion

When I explicitly tell JavaScript to convert a value into a particular type.

Example:

```js
Number("42"); // 42
```

### Implicit Type Coercion

When JavaScript automatically converts values to perform an operation.

Example:

```js
"42" - 2; // 40
```

### Strict Equality

When I compare two values without allowing JavaScript to coerce operands of different types.

Example:

```js
"42" === 42; // false
```

### Key Takeaways

- JavaScript has seven primitive data types.
- Arrays are objects, and `typeof` cannot distinguish arrays from ordinary objects.
- `typeof null` returns `"object"` because of a historical quirk.
- `null` and `undefined` are different primitive values.
- Explicit conversion lets us control how values are converted.
- Truthy and falsy values affect how values behave in Boolean contexts.
- Implicit coercion can produce unexpected results, especially with the `+` operator.
- `===` is generally preferable to `==` because it avoids coercion between different types.
