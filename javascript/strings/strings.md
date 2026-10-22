# JavaScript Strings

## 1. String Indexing

Strings allow us to access individual characters using indexing.

JavaScript uses **zero-based indexing**, which means the first character is at index `0`, the second at index `1`, and so on.

```js
const language = "JavaScript";

console.log(language[0]); // "J"
console.log(language[4]); // "S"
console.log(language[9]); // "t"
```

To access the last character without knowing the string's length beforehand, use `length - 1`.

```js
console.log(language[language.length - 1]); // "t"
```

Since indexing starts at `0`, the last index is always one less than the string's length.

## 2. The `length` Property

The `length` property tells us how many UTF-16 code units a string contains.

```js
const language = "JavaScript";

console.log(language.length); // 10
```

`length` is a **property**, not a method.

- A property provides information about a value.
- A method is a function that can be called to perform an operation.

For example:

```js
language.length;        // Property
language.toUpperCase(); // Method

Array.isArray([1, 2]);  // Static method
```

Static methods are called on a constructor or class itself, while instance methods are called on a particular value or instance. JavaScript primitives can also expose methods through automatic boxing.

The relationship between a string's length and its last index is:

```js
lastIndex = string.length - 1;
```

**Technical note:** String length counts UTF-16 code units, not necessarily user-perceived characters. Most basic English characters occupy one code unit, but some Unicode characters, such as many emoji, occupy two.

## 3. String Immutability

Strings in JavaScript are **immutable**, meaning their contents cannot be changed after the string value is created.

```js
let language = "JavaScript";

language[0] = "Y";

console.log(language); // "JavaScript"
```

The first character does not change because string characters are exposed through read-only indexed properties.

In ordinary non-strict code, this assignment has no effect. In strict mode, attempting this assignment throws a `TypeError`. JavaScript modules run in strict mode by default.

Think of it like trying to edit a read-only file: the attempted modification cannot change the original contents.

### Immutability vs. Reassignment

Using `let` allows us to reassign a variable, but it does not make the string itself mutable.

```js
let language = "JavaScript";

language = "YavaScript";

console.log(language); // "YavaScript"
```

Here, we are not modifying the original string. We are assigning a different string value to the variable.

String methods such as `trim()`, `slice()`, `toLowerCase()`, and `toUpperCase()` also return string results without mutating the original string.

## 4. `trim()`

The `trim()` method removes whitespace from the beginning and end of a string.

```js
const username = "   manjot   ";

console.log(username.trim()); // "manjot"
console.log(username);        // "   manjot   "
```

`trim()` returns a new string and does not modify the original string.

It removes whitespace from both ends, but it does not remove whitespace between words.

```js
const message = "   hello   world   ";

console.log(message.trim()); // "hello   world"
```

JavaScript also provides:

- `trimStart()` — removes whitespace from the beginning.
- `trimEnd()` — removes whitespace from the end.

## 5. Case Conversion

JavaScript provides two common methods for changing the case of letters:

- `toLowerCase()` — converts letters to lowercase.
- `toUpperCase()` — converts letters to uppercase.

```js
const language = "JaVaScRiPt";

console.log(language.toLowerCase()); // "javascript"
console.log(language.toUpperCase()); // "JAVASCRIPT"
console.log(language);               // "JaVaScRiPt"
```

These methods return new strings without modifying the original.

To store the lowercase version back in the same variable, reassign the result:

```js
let language = "JaVaScRiPt";

language = language.toLowerCase();

console.log(language); // "javascript"
```

The variable is reassigned; the original string is not mutated.

## 6. `slice()`

The `slice()` method extracts part of a string and returns it as a new string.

### Syntax

```js
string.slice(startIndex, endIndex);
```

- `startIndex` — the index where extraction begins; this character is included.
- `endIndex` — the index where extraction stops; this character is excluded.
- If `endIndex` is omitted, extraction continues to the end of the string.
- Negative indexes count backward from the end of the string. For example, `-1` refers to the last UTF-16 code unit.

```js
const language = "JavaScript";

console.log(language.slice(0, 4));   // "Java"
console.log(language.slice(4, 10));  // "Script"
console.log(language.slice(4));      // "Script"
console.log(language.slice(-6));     // "Script"
console.log(language.slice(0, -6));  // "Java"
console.log(language.slice(-6, -3)); // "Scr"
```

### Understanding Negative Indexes

The string `"JavaScript"` has a length of `10`.

- `slice(-6)` starts six positions from the end, at index `4`, and takes the rest of the string.
- `slice(0, -6)` starts at index `0` and stops six positions from the end, equivalent to an end index of `4`.
- `slice(-6, -3)` starts at index `4` and stops at index `7`, excluding index `7`.

`slice()` does not modify the original string. It returns a new string containing the extracted portion.

## 7. Template Literals

Template literals use backticks (`` ` ``) instead of ordinary single or double quotes.

They provide a readable way to embed variables and expressions inside strings without repeatedly using `+` for concatenation.

```js
const name = "Manjot";
const age = 25;

console.log(`My name is ${name} and I am ${age} years old.`);
// "My name is Manjot and I am 25 years old."
```

The `${...}` syntax allows us to embed expressions inside a template literal. JavaScript evaluates the expression and inserts its result into the string.

```js
console.log(`Next year, I'll be ${age + 1}.`);
// "Next year, I'll be 26."
```

### Multiline Strings

Template literals can contain line breaks directly, making multiline strings easier to write.

```js
const message = `Hello!
Welcome to JavaScript.
Let's keep learning.`;

console.log(message);
```

The resulting string contains the line breaks.

## 8. Quick Reference

- **Indexing:** Access individual characters using zero-based indexes, starting at `0`.
- **`length`:** A property that returns the number of UTF-16 code units in a string.
- **Immutability:** A string's contents cannot be changed after creation, although a variable holding a string can be reassigned.
- **`trim()`:** Removes whitespace from both ends of a string and returns a new string.
- **Case conversion:** `toLowerCase()` and `toUpperCase()` return strings with converted letter case.
- **`slice()`:** Extracts a portion of a string. The start index is included and the end index is excluded.
- **Template literals:** Use backticks and `${...}` to embed expressions and create multiline strings conveniently.

## 9. Practice Exercises

Try predicting the outputs before running the code.

### Exercise 1 — Last Character

```js
const framework = "React";

console.log(framework[framework.length - 1]); // "t"
```

### Exercise 2 — Immutability

```js
let greeting = "hello";

greeting[0] = "H";

console.log(greeting); // "hello"
```

The original string remains unchanged because strings are immutable. In strict mode, the attempted assignment throws a `TypeError`.

### Exercise 3 — `slice()`

```js
const language = "JavaScript";

console.log(language.slice(4, 7)); // "Scr"
console.log(language.slice(-3));   // "ipt"
```

The end index is excluded, and a negative start index counts backward from the end.

### Exercise 4 — Template Literals

```js
const product = "Laptop";
const price = 50000;

console.log(`The ${product} costs ${price} rupees.`);
// "The Laptop costs 50000 rupees."
```

### Exercise 5 — Combined Practice

```js
const username = "   MANJOT   ";

// 1. Remove leading and trailing whitespace.
// 2. Convert the result to lowercase.
// 3. Print the last three characters of the result.

const cleanedUsername = username.trim().toLowerCase();

console.log(cleanedUsername);                  // "manjot"
console.log(cleanedUsername.slice(-3));        // "jot"
```

This exercise combines `trim()`, case conversion, and `slice()`.

## Key Takeaways

- Strings use zero-based indexing.
- `length` is a property, not a method.
- String length counts UTF-16 code units.
- Strings are immutable, but variables holding them can be reassigned.
- String methods return results without mutating the original string.
- `slice()` includes the start index and excludes the end index.
- Template literals support expression interpolation and multiline strings.
