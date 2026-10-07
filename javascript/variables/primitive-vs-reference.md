# Primitive Vs Reference Data Types and how mutation and reassignment affect them

## What happens when primitive values are assigned and mutated?

Suppose we have the following code example

```
  let num1 = 7;
  let num2 = num1;
  num1++;
```

### Q. What do you suppose would happen to the value of num2?
A. It would remain 7.
Breakdown:
Initially the value of num1 is 7. then we made another variable num2 and assigned it the value of num1. 
num2 is a different variable that stored the value 7.
Doing num1++ only mutates num1 to 8 and not num2 because when a primitive value is assigned to another variable, the value itself is copied

## What happens when an object/array is assigned?

Suppose we have the following code example

```
  let arr1 = [1,2,3];
  let arr2 = arr1;
  arr1.pop();
```

### Q What happens to the value of arr2 after the pop operation and why?
A. The value of arr2 becomes [1,2] because both the arr1 variable and the arr2 variable are pointing towards the same array.
Breakdown: When we do `arr1=[1,2,3];` we create a new array [1,2,3] and arr1 stores a reference for that array. When an array/object is assigned to another variable, the reference to that object is copied.
In the next line, when we do `arr2=arr1;` we essentially stored the reference stored in arr1 to arr2 so both the variables point to the same array.
Mutating the shared array means that both arr1 and arr2 now observe the changed array because arr1 itself really isn't "the array". It's a variable holding a reference to the array.

## Mutation Vs Reassignment

Suppose we have the following code example

```
  let arr1 = [1,2,3];
  let arr2 = arr1;
  arr1 = [4,5,6];
```

### Q. What happens to the value of arr2 and why?
A. The value of arr2 remains unaffected.
Breakdown: We stored the same reference in arr1 and arr2 but when we reassigned arr1, didn't do anything to the value stored in arr2 which is still pointing to [1,2,3]

Note: This behaviour remains the same for objects


### Example with objects

```
let person1 = {
  name: "Manjot",
  age: 25
}
let person2 = person1;
person1.age = 26;
```

Here, when we do `person1.age = 26;`, both person1 and person2 refer to the same object. When we mutate that object's age property, the change is visible through both variables.
Reassignment would work the same as in case of an array