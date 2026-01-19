# Refactoring-var-to-const-and-let

## Overview
This project refactors JavaScript code by replacing all var declarations with let or const. The goal is to improve code reliability, readability, and scoping behavior by using modern ES6 variable declarations.

## Refactoring Summary
Each var was replaced with either let or const based on how the variable is used:
- let was used for variables that are reassigned or updated.
- const would be used for values that never change (none applied in this specific code).
- Block‑scoped variables (message, loggedIn, i) were updated to prevent leakage outside their intended scope.
Your code comments explain these decisions directly in the file.

## Potential Issues Caused by the Original Use of var
1. Hoisting Leading to Unexpected Behavior
var is hoisted to the top of its function, meaning variables exist earlier than intended.
In the original code:
- userRole was hoisted and initialized as undefined, making the admin check always fail.
- message inside the if and else blocks was actually the same variable, even though it looked like two separate declarations.
This can create subtle logic bugs.

2. Lack of Block Scope
var ignores block boundaries (if, else, for, etc.), which can cause variables to leak into outer scopes.
Examples from the original code:
- message was accessible outside the if block.
- loggedIn inside the loop leaked outside the loop.
- i remained accessible after the loop ended.
Using let prevents this by keeping variables inside their intended blocks.

3. Accidental Re‑declaration
var allows redeclaring the same variable name without errors.
In the original code:
var message = "User is logged in.";
...
var message = "User not logged in.";


These two declarations actually referred to the same variable, which can cause confusion or unintended overwriting.

4. Silent Logic Errors
Because var initializes variables as undefined, the code can fail quietly.
Example:
var userRole;
if (userRole === "admin") { ... }


This condition will always be false, but the code gives no warning.
Using let makes this easier to spot because the variable is clearly uninitialized and scoped more tightly.

5. Loop Behavior Problems
Using var in loops can cause:
- Shared loop counters
- Unexpected overwriting
- Variables persisting after the loop ends
Replacing var with let ensures each iteration has its own block‑scoped values.
