# Chapter 1: JavaScript Fundamentals - Complete Notes

---

## 1. **VARIABLES** 📦

### What is a Variable?

A **variable** is a container to store data in JavaScript. We can store any type of data in it (numbers, strings, booleans, objects, arrays, etc.) and use it anywhere in our program after declaring and initializing it.

### Real-Life Examples:

**Example 1: ATM System**
- When you insert your card at an ATM to withdraw Rs.500, the system remembers your card details and saves your data in variables
- When you request withdrawal, it uses that stored data
- This is essentially what variables do in JavaScript

**Example 2: Snake Game**
- At game start, score = 0
- Each time snake eats apple, score increases by 1
- The system remembers and updates the score variable every time
- When game ends, it prints the current score value from memory

**Example 3: Wedding Card Printing**
- You're printing 100 wedding cards for "Aamir weds Maria"
- If you store names in a changeable variable, someone might change it to "Aamir weds Sara"
- This would damage the reputation of the real couple
- Solution: Use immutable variables (const) so no one can change the values

### Declaration Methods (Ways to Write Variables):

```javascript
// Method 1: Declare separately
var a; 
a = 12;                    ✔️ Correct

// Method 2: Declare & Initialize together
var a = 12;                ✔️ Correct

// Method 3: Using let
let a;
a = 12;                    ✔️ Correct

// Method 4: Let with initialization
let a = 12;                ✔️ Correct

// Method 5: Const with initialization
const a = 12;              ✔️ Correct

// Method 6: WRONG - Const without initialization
const a;
a = 12;                    ❌ WRONG - Cannot declare const without initialization
```

**Why Method 6 is Wrong:**
- With const, you cannot create an empty/undefined variable first and then initialize it later
- const requires initialization at declaration time itself

---

## 2. **DECLARATION vs INITIALIZATION** 🎯

### Definitions:

**Declaration:**
- Using a variable keyword to create/announce that a variable exists
- Example: `var a;` → This declares variable 'a' exists

**Initialization:**
- Giving a value to an already-created variable
- Example: `a = 12;` → This initializes variable 'a' with value 12

**Declaration + Initialization Together:**
- Creating a variable AND giving it a value at the same time
- Example: `var a = 12;` → Both declaration and initialization

### Important Rule:
```
✔️ Declaration must come BEFORE Initialization
❌ You cannot initialize a variable before declaring it
```

---

## 3. **VAR vs LET vs CONST** 👑

### Detailed Comparison:

#### **VAR (ES5 - Old Version)**

**Characteristics:**
- Can be re-declared with the same name
- Can be reassigned (value changed)
- Function scoped (not block scoped)
- Added to the window object
- Gets hoisted with `undefined` value
- Most problematic of the three

**Problems with var:**
1. Can accidentally re-declare variables without errors
2. Function-scoped instead of block-scoped
3. Leaks into the global window object
4. Can mask bugs because of loose constraints

**Code Example:**
```javascript
var a = 12;
a = 32;           ✅ Reassignment works
var a = 1232;     ✅ Redeclaration works (NO ERROR!)
```

**Problem:** If you accidentally re-declare with the same name, there's no error notification. You might create bugs that are hard to track.

---

#### **LET (ES6 - Modern)**

**Characteristics:**
- Cannot be re-declared with the same name
- Can be reassigned (value changed)
- Block scoped (limited to its block)
- NOT added to window object
- Gets hoisted but with Temporal Dead Zone
- Prevents accidental re-declarations

**Advantages over var:**
- If you try to re-declare, you immediately get an error
- This catches mistakes early before they become big problems
- Forces you to use proper naming or fix the issue right away

**Code Example:**
```javascript
let age = 25;
age = 30;         ✅ Reassignment works

let age = 40;     ❌ Redeclaration throws error
                  // Error: "age" has already been declared
```

**Function-Scoped vs Block-Scoped:**
- var is functional scoped: `var` can be used anywhere inside its parent function
- let is block scoped: `let` can only be used inside the block where it was declared (if statements, loops, etc.)

---

#### **CONST (ES6 - Modern) 👑**

**Characteristics:**
- Cannot be re-declared
- Cannot be reassigned
- Block scoped (like let)
- NOT added to window object
- Must be initialized at declaration time
- Value is immutable (cannot be changed)

**Code Example:**
```javascript
const PI = 3.14;
PI = 3.14159;     ❌ Reassignment throws error

// BUT: If const holds an object/array, contents CAN be modified:
const student = { 
    name: "Riya" 
};

student.name = "Priya";  ✅ Modifying object properties works
student = {};            ❌ Reassigning the object throws error
```

**Important:** 
- const's VALUE cannot change
- But if const contains an OBJECT or ARRAY, the properties/elements inside can be modified
- The difference: you can't change what the variable points to, but you can change what's inside it

---

### Quick Comparison Table:

| Feature | var | let | const |
|---------|-----|-----|-------|
| **Redeclaration** | ✅ Yes | ❌ No | ❌ No |
| **Reassignment** | ✅ Yes | ✅ Yes | ❌ No |
| **Scope** | Functional | Block | Block |
| **Window Object** | ✅ Added | ❌ No | ❌ No |
| **Hoisting** | undefined | TDZ | TDZ |
| **Must Initialize** | ❌ No | ❌ No | ✅ Yes |

**Best Practice:** Use `const` by default, use `let` when you need to reassign, avoid `var` in modern JavaScript.

---

## 4. **SCOPE** 🎯

### What is Scope?

**Scope** is your accessible area. It defines where in your code a variable can be used and accessed.

### Three Types of Scope:

#### **1. Global Scope**
- Variables declared outside any function or block
- Accessible everywhere in the entire file
- Can be accessed from any function or block

```javascript
let globalVar = 10;  // Global scope

function myFunction() {
    console.log(globalVar);  // ✅ Can access
}

if (true) {
    console.log(globalVar);  // ✅ Can access
}
```

#### **2. Functional Scope (Function Scope)**
- Variables declared inside a function
- Only accessible within that function
- This is how `var` behaves

```javascript
function myFunction() {
    var functionVar = 20;  // Functional scope
}

console.log(functionVar);  // ❌ Error: functionVar is not defined
```

#### **3. Block Scope**
- Variables declared inside a block (if, for, while, etc.)
- A block is any code enclosed in curly brackets `{}`
- Only accessible within that specific block
- `let` and `const` have block scope

```javascript
if (true) {
    let blockVar = 30;  // Block scope
    console.log(blockVar);  // ✅ Can access (inside block)
}

console.log(blockVar);  // ❌ Error: blockVar is not defined (outside block)
```

### Important Distinctions:

**var is Functional Scoped:**
```javascript
if (true) {
    var x = 10;
}
console.log(x);  // ✅ 10 (var escapes the block!)
```

**let and const are Block Scoped:**
```javascript
if (true) {
    let y = 20;
}
console.log(y);  // ❌ Error: y is not defined (can't escape block)
```

### Why Block Scope is Better:

Every programming language prefers block-scoped variables because:
- They isolate variables to their intended area
- Prevent accidental use of variables outside their intended scope
- Reduce naming conflicts
- Make code more maintainable

---

## 5. **HOISTING** 🚀

### What is Hoisting?

**Hoisting** is JavaScript's behavior of moving declarations to the top of their scope before execution.

When you create a variable, JavaScript breaks it into TWO parts:
1. **Declaration part** - `var a;` (moves to top)
2. **Initialization part** - `a = 32;` (stays where it is)

### How Hoisting Works:

#### **VAR Hoisting:**

```javascript
// Your code:
console.log(a);     // Line 1
var a = 32;         // Line 3

// What JavaScript actually does:
var a = undefined;   // Declaration moved to top (undefined!)
console.log(a);      // Line 1 → prints: undefined
a = 32;              // Initialization stays here
```

**Result:** Prints `undefined` (no error)

**Why?** Because the declaration `var a;` is hoisted to the top and initialized with `undefined` by default, but the actual value assignment `a = 32;` stays at line 3.

#### **LET Hoisting:**

```javascript
// Your code:
console.log(b);     // ❌ Error!
let b = 20;

// JavaScript knows b exists, but:
// Declaration is hoisted BUT in "Temporal Dead Zone"
// You cannot use it before initialization
```

**Result:** `ReferenceError: Cannot access 'b' before initialization`

**Key Point:** let IS hoisted, but it's in the Temporal Dead Zone and cannot be used.

#### **CONST Hoisting:**

Same as `let` - it's hoisted but in Temporal Dead Zone.

```javascript
console.log(c);     // ❌ Error!
const c = 30;
// ReferenceError: Cannot access 'c' before initialization
```

### Comparison:

| Type | Before Initialization | Error Message |
|------|----------------------|---------------|
| var | undefined | No error |
| let | Temporal Dead Zone | "Cannot access before initialization" |
| const | Temporal Dead Zone | "Cannot access before initialization" |

---

## 6. **TEMPORAL DEAD ZONE (TDZ)** 💹

### What is Temporal Dead Zone?

The **Temporal Dead Zone** is the period from the start of execution until a `let` or `const` variable is initialized. During this zone, the variable exists but cannot be accessed.

### Understanding TDZ:

```javascript
// Lines 1-11: TDZ for variable 'a'
// Line 12 is where 'a' is initialized

let a = someValue;  // Line 12 - TDZ ENDS here

// Lines 1-11: If you try to use 'a' here, you get error:
// "Cannot access 'a' before initialization"
// NOT "a is undefined"
```

**Error Message is the Key:**
- If you get: `"Cannot access 'a' before initialization"` → variable EXISTS but in TDZ
- If you get: `"a is not defined"` → variable was NEVER declared

### Important Distinction:

```javascript
// Scenario 1: Variable is declared but in TDZ
console.log(x);     // ❌ "Cannot access 'x' before initialization"
let x = 10;         // TDZ ends here

// Scenario 2: Variable is never declared
console.log(y);     // ❌ "y is not defined"
// y is never declared anywhere
```

### Multiple Variables Example:

```javascript
// Variable 'a' initialized at line 15
// Variable 'b' initialized at line 17

// Lines 1-14: TDZ for 'a' (can't use 'a')
// Lines 1-16: TDZ for 'b' (can't use 'b')

let a = 10;  // Line 15
let b = 20;  // Line 17
```

**TDZ Zones:**
- Variable 'a': TDZ is from line 1 to line 14
- Variable 'b': TDZ is from line 1 to line 16

### Key Takeaway:

```
TDZ = From start of code until the line where initialization happens
```

**Only affects:** `let` and `const`
**Does NOT affect:** `var` (can be used before initialization with value `undefined`)

---

## 7. **REASSIGNMENT vs REDECLARATION** 🔄

### Definitions:

**Reassignment:**
- Changing the value of an already-created variable
- Using the variable name without a keyword
- Example: `a = 12;` (no keyword, just assignment)

**Redeclaration:**
- Creating a NEW variable with the same name (using var/let/const keyword)
- Example: `var a = 12;` (using keyword)

### Behavior by Type:

#### **VAR: Can Reassign AND Redeclare**

```javascript
var a = 12;
a = 32;         // ✅ Reassignment works

var a = 1232;   // ✅ Redeclaration works (NO ERROR)
```

**Problem:** Both work, so you can accidentally redeclare without knowing.

#### **LET: Can Reassign BUT NOT Redeclare**

```javascript
let b = 12;
b = 32;         // ✅ Reassignment works

let b = 1232;   // ❌ Redeclaration throws error
                // Error: Identifier 'b' has already been declared
```

**Advantage:** Prevents accidental redeclaration and catches mistakes early.

#### **CONST: Cannot Reassign AND Cannot Redeclare**

```javascript
const c = 12;
c = 32;         // ❌ Reassignment throws error

const c = 1232; // ❌ Redeclaration throws error
```

**Exception with Objects/Arrays:**
```javascript
const obj = { name: "Azam" };
obj.name = "Ahmed";     // ✅ Modifying properties works
obj = {};               // ❌ Reassignment throws error
```

---

## 8. **KEYWORDS vs WORDS** 🏷️

### Definitions:

**Keyword:**
- Every word with a specific meaning in JavaScript
- Reserved by the language for specific purposes
- Can only be used as intended by the language

**Word:**
- Any text that does NOT have a specific meaning in JavaScript
- Can be used as variable names, function names, etc.
- NOT reserved by the language

### Examples:

**Keywords (Reserved - Cannot be used as variable names):**
```javascript
if, else, var, let, const, function, return, for, while, class, 
new, true, false, null, undefined, this, switch, case, break, 
continue, try, catch, finally, throw, typeof, instanceof, delete, 
and many more...
```

**Words (Not Reserved - Can be used as variable names):**
```javascript
myName, age, count, userName, data, result, myFunction, handleClick, etc.
```

### Practical Examples:

```javascript
// ❌ WRONG - Using keyword as variable name
let var = 10;       // SyntaxError: var is a keyword

// ✅ CORRECT - Using a word as variable name
let myVar = 10;     // Works fine

// ❌ WRONG
const if = 20;      // SyntaxError: if is a keyword

// ✅ CORRECT
const condition = 20;  // Works fine
```

---

## 9. **CHAPTER 1 PRACTICE QUESTIONS** 📝

### Practice Question 1:
**Declare your name and city using `const`, and your age using `let`.**

```javascript
const myname = "Azam Gohar";
const mycity = "Karachi";
let myage = 17;
```

---

### Practice Question 2:
**Try this and observe the result:**
```javascript
let x = 5;
let x = 10;
```

**Result:** ❌ **SyntaxError: Identifier 'x' has already been declared**

**Why:** `let` does not allow redeclaration. When you try to declare 'x' a second time, JavaScript throws an error because 'x' already exists in that scope.

---

### Practice Question 3:
**Guess the output:**
```javascript
console.log(count);
var count = 42;
```

**Output:** `undefined`

**Why:** Due to hoisting:
- The declaration `var count;` is hoisted to the top
- It's initialized with `undefined`
- The actual value assignment `count = 42;` stays at its original line
- So when console.log runs, count exists but has value `undefined`

---

### Practice Question 4:
**Create a const object and add a new key to it — does it work?**

```javascript
const obj = {
    name: "Azam Gohar",
}

obj.newKey = "newValue";  // ✅ Works!
```

**Result:** ✅ **YES, it works!**

**Why:** 
- `const` prevents reassigning the object itself
- But it does NOT prevent modifying the contents of the object
- You can add new properties, modify existing properties
- You just cannot reassign the entire object to something else

```javascript
obj = {};  // ❌ This would throw an error (reassignment)
```

---

### Practice Question 5:
**Try accessing a `let` variable before declaring it — what error do you see?**

```javascript
console.log(beforeDeclare);
let beforeDeclare = 12;
```

**Error:** ❌ `ReferenceError: Cannot access 'beforeDeclare' before initialization`

**Why:** 
- `let` is hoisted but placed in Temporal Dead Zone
- The error message specifically says "before initialization" (not "undefined")
- This tells us the variable EXISTS but is in TDZ and cannot be accessed yet

---

### Practice Question 6:
**Change a const array by pushing a value. Will it throw an error?**

```javascript
const myArray = [1, 2, 3, 4];
console.log(myArray.push(5));  // Pushes 5 to array
console.log(myArray);          // [1, 2, 3, 4, 5]
```

**Result:** ✅ **NO, it does NOT throw an error!**

**Why:**
- `const` prevents reassigning the array variable
- But it allows modifying the contents (elements) of the array
- `.push()` modifies the array contents, not the array reference
- So this operation is allowed

```javascript
myArray = [5, 6, 7];  // ❌ This would throw error (reassignment)
```

---

## 10. **QUICK REFERENCE GUIDE** ⚡

### When to Use What:

| Situation | Use |
|-----------|-----|
| Value will NEVER change | `const` |
| Value will change | `let` |
| Old code (pre-ES6) | `var` (avoid in new code) |

### Common Mistakes to Avoid:

1. ❌ Declaring const without initialization
   ```javascript
   const x;  // ❌ Error
   ```

2. ❌ Using var (causes scope and redeclaration issues)
   ```javascript
   var x = 10;  // ❌ Avoid, use let/const instead
   ```

3. ❌ Trying to reassign const
   ```javascript
   const x = 10;
   x = 20;  // ❌ Error
   ```

4. ❌ Trying to redeclare let
   ```javascript
   let x = 10;
   let x = 20;  // ❌ Error
   ```

5. ❌ Mixing up "Cannot access before initialization" with "not defined"
   ```javascript
   console.log(x);  // Different errors depending on declaration type!
   let x = 10;
   ```

### Hoisting Summary:

```javascript
// var: Hoisted with undefined
console.log(a);  // undefined
var a = 10;

// let: Hoisted to TDZ (cannot access)
console.log(b);  // ❌ ReferenceError
let b = 20;

// const: Hoisted to TDZ (cannot access)
console.log(c);  // ❌ ReferenceError
const c = 30;
```

---

## 11. **KEY TAKEAWAYS** 🎓

1. **Variables** are containers to store data
2. **Declare** = announce variable exists, **Initialize** = give it a value
3. **var** is old and problematic - avoid it
4. **let** is for values that change, **const** is for values that don't
5. **Scope** defines where a variable can be accessed
6. **var** = functional scope, **let/const** = block scope
7. **Hoisting** = declarations move to top, but initialization stays
8. **TDZ** = period where let/const exist but can't be used
9. **Reassignment** = change value, **Redeclaration** = create with same name again
10. **Keywords** are reserved words, **Words** are custom names

---

## 12. **PRACTICE EXERCISE CHECKLIST** ✅

After studying this chapter, make sure you can:

- [ ] Explain what a variable is with real-life examples
- [ ] Declare variables using const, let, and var
- [ ] Understand the difference between declaration and initialization
- [ ] Explain why const should be default choice
- [ ] Identify differences between var, let, and const
- [ ] Explain global, functional, and block scopes
- [ ] Predict hoisting behavior for each variable type
- [ ] Identify variables in Temporal Dead Zone
- [ ] Distinguish between reassignment and redeclaration
- [ ] Recognize keywords vs words
- [ ] Solve all 6 practice questions from Chapter 1

---

**Created on:** April 6, 2026  
**Course:** JS Everything - Chapter 1  
**Status:** ✅ Complete with all details covered
