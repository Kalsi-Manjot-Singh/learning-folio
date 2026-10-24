# JavaScript Conditionals

Conditionals allow a program to make decisions and execute different blocks of code depending on whether conditions are satisfied.

## 1. `if` Statement

An `if` statement executes its block when its condition evaluates to a truthy value.

### Syntax

```js
if (condition) {
  // Execute when condition is truthy
}
```

### Example

```js
const isLoggedIn = true;

if (isLoggedIn) {
  console.log("Welcome back!");
}

console.log("Program continues...");
```

Output:

```text
Welcome back!
Program continues...
```

If the condition is falsy, JavaScript skips the block and continues executing the program.

```js
const isLoggedIn = false;

if (isLoggedIn) {
  console.log("Welcome back!");
}

console.log("Program continues...");
```

Output:

```text
Program continues...
```

## 2. `if / else`

An `else` block provides an alternative when the `if` condition is falsy.

### Syntax

```js
if (condition) {
  // Execute when condition is truthy
} else {
  // Execute when condition is falsy
}
```

### Example

```js
const isLoggedIn = false;

if (isLoggedIn) {
  console.log("Welcome back!");
} else {
  console.log("Please log in.");
}
```

Output:

```text
Please log in.
```

The `else` block is optional. If omitted, JavaScript simply skips the `if` block when its condition is falsy.

**Key point:** An `if / else` statement executes only one of its two branches.

## 3. `else if`

Use `else if` when you need to check multiple conditions in sequence.

### Syntax

```js
if (condition1) {
  // First condition is truthy
} else if (condition2) {
  // First condition was falsy, second is truthy
} else {
  // All preceding conditions were falsy
}
```

### Example

```js
const score = 95;

if (score >= 90) {
  console.log("Grade A");
} else if (score >= 70) {
  console.log("Grade B");
} else {
  console.log("Grade C");
}
```

Output:

```text
Grade A
```

JavaScript evaluates conditions from top to bottom. Once a branch matches, the remaining branches in that chain are skipped.

### Why condition order matters

Consider this example:

```js
const score = 95;

if (score >= 70) {
  console.log("Grade B or above");
} else if (score >= 90) {
  console.log("Grade A");
}
```

Output:

```text
Grade B or above
```

Although `score >= 90` is also true, JavaScript never checks it because the first condition already matched.

**Best practice:** Put more specific conditions before broader conditions when necessary.

If no condition matches and there is no `else` block, none of the branches execute and the program continues after the conditional.

## 4. Nested `if`

A nested `if` is an `if` statement placed inside another conditional block.

Nested conditionals are useful when a decision depends on multiple levels of conditions.

### Example

```js
const isLoggedIn = true;
const isAdmin = false;

if (isLoggedIn) {
  if (isAdmin) {
    console.log("Welcome, admin!");
  } else {
    console.log("Access denied: admin privileges required.");
  }
} else {
  console.log("Please log in.");
}
```

Output:

```text
Access denied: admin privileges required.
```

### How it works

1. JavaScript evaluates the outer condition, `isLoggedIn`.
2. If it is truthy, execution enters the outer block and evaluates `isAdmin`.
3. The inner conditional selects its branch based on `isAdmin`.
4. If the outer condition is falsy, the inner conditional is never evaluated.

Nested `if` statements can be useful for access control, validation, and workflows where one decision depends on another.

## 5. Ternary Operator (`? :`)

The ternary operator is a concise way to choose between two expressions based on a condition.

### Syntax

```js
condition ? expressionIfTrue : expressionIfFalse;
```

- `?` separates the condition from the expression selected when it is truthy.
- `:` separates the truthy expression from the falsy expression.

### Example

```js
const temperature = 12;

const message = temperature > 25 ? "Hot" : "Not hot";

console.log(message);
```

Output:

```text
Not hot
```

The condition `temperature > 25` is falsy, so the expression `"Not hot"` is selected.

### Using a ternary to assign values

```js
const age = 20;

const category = age >= 18 ? "Adult" : "Minor";

console.log(category); // "Adult"
```

The ternary operator is an expression, so its result can be assigned to a variable, returned from a function, or passed as an argument.

### Ternary versus `if / else`

Use a ternary for simple choices between two expressions.

Use `if / else` when the branches contain multiple statements or when the ternary would make the code difficult to read.

```js
if (isLoggedIn) {
  loadDashboard();
  fetchUserProfile();
  showWelcomeMessage();
} else {
  redirectToLogin();
}
```

Avoid deeply nested ternary expressions when they reduce readability.

## 6. `switch` Statement

A `switch` statement selects a branch based on the value of an expression. It is useful when comparing one expression against several possible values.

### Syntax

```js
switch (expression) {
  case value1:
    // Statements
    break;
  case value2:
    // Statements
    break;
  default:
    // Fallback statements
}
```

### Example

```js
const choice = 2;

switch (choice) {
  case 1:
    console.log("Start game");
    break;
  case 2:
    console.log("Settings");
    break;
  case 3:
    console.log("Quit");
    break;
  default:
    console.log("Invalid choice");
}
```

Output:

```text
Settings
```

### The `break` keyword

`break` exits the `switch` statement. Without it, execution falls through into subsequent cases, executing their statements until another `break` or the end of the `switch` is reached.

```js
const choice = 2;

switch (choice) {
  case 1:
    console.log("One");
  case 2:
    console.log("Two");
  case 3:
    console.log("Three");
    break;
  default:
    console.log("Other");
}
```

Output:

```text
Two
Three
```

Execution starts at `case 2`, falls through into `case 3`, and exits at its `break`. The `default` block does not execute.

### The `default` case

`default` is the fallback branch when no case matches. It is optional.

```js
const choice = 9;

switch (choice) {
  case 1:
    console.log("One");
    break;
  case 2:
    console.log("Two");
    break;
  default:
    console.log("Unknown choice");
}
```

Output:

```text
Unknown choice
```

### Important: `switch` uses strict matching

A `switch` case uses strict equality semantics, so a number and a string containing the same digits do not match.

```js
const choice = "2";

switch (choice) {
  case 2:
    console.log("Number two");
    break;
  case "2":
    console.log("String two");
    break;
}
```

Output:

```text
String two
```

## 7. Practice Exercises

Try predicting the outputs before running these examples.

### Exercise 1: `if / else`

```js
const age = 16;

if (age >= 18) {
  console.log("Eligible");
} else {
  console.log("Not eligible");
}
```

### Exercise 2: `else if`

```js
const score = 82;

if (score >= 90) {
  console.log("A");
} else if (score >= 80) {
  console.log("B");
} else if (score >= 70) {
  console.log("C");
} else {
  console.log("D");
}
```

### Exercise 3: Nested `if`

```js
const hasAccount = true;
const hasPassword = false;

if (hasAccount) {
  if (hasPassword) {
    console.log("Log in");
  } else {
    console.log("Enter your password");
  }
} else {
  console.log("Create an account");
}
```

### Exercise 4: Ternary

```js
const number = 7;
const result = number % 2 === 0 ? "Even" : "Odd";

console.log(result);
```

### Exercise 5: `switch`

```js
const day = 2;

switch (day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  default:
    console.log("Unknown day");
}
```

## Key Takeaways

- `if` executes its block when the condition is truthy.
- `else` provides an alternative when the `if` condition is falsy.
- `else if` checks additional conditions in order; only the first matching branch executes.
- Condition order matters because a broad condition can match before a more specific one.
- Nested `if` statements handle decisions that depend on earlier decisions.
- The ternary operator is a concise expression for choosing between two values or expressions.
- `switch` selects a branch based on matching case values.
- `break` prevents fall-through; `default` provides a fallback when no case matches.
