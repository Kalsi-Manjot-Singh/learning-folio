#Variables

## What a variable is
A variable in JavaScript or any programming language for that matter is used to store information that can be used repeatedly across the program.

## let, const, var
In JavaScript, three different keywords can be use to create a variable, var, let, and const although const keyword creates a binding that cannot be reassigned.
- `let` and `const` are block-scoped. `var` is function-scoped.
- `var` can escape an `if`/`for` block, but it cannot escape the function in which it was declared.

## Reassignment vs const
```
let age = 25;
age = 26;
var name = "Manjot";
name = "mango";
```
is valid and wont' throw any errors but 
```
const age = 26;
age = 26;
```
will throw error: Assignment to constant variable

## Block scope vs function scope
Block scope: A block scoped variable only exists within the scope of the code block it was created in
Function scope: A function-scoped variable is accessible throughout the function in which it was declared, even if it was declared inside a block within that function.

## One example demonstrating the let/var difference
Let keyword is block scoped meaning the variables created by it only exist in that code block  but var is functionally scoped meaning its value is avaible to the function as well even if it was created inside a block within that function.

```
function example() {
  if (true) {
    let n1 = 23;
    var n2 = 24;
  }

  console.log(n1); // ❌
  console.log(n2); // 24
}
```

## Naming conventions / rules
- We generally use `camelCase` for variable names.
- A variable name cannot start with a number, although numbers can appear later.
- Variable names can contain letters, numbers, `_`, and `$`.
- Spaces and other special characters are not allowed.
- Class names conventionally start with a capital letter.