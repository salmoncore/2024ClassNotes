## Declaration
- Three ways to declare a variable:
    - Function scoped - old way of declaring variables
        - `var a = 1;`
    - Block scoped:
        - `let b = 2;`
        - `const c = 3;`
    
`TypeError: Assignment to constant variable.` if you attempt to update the value of a variable declared with const.

## Hoisting
- JavaScript's default behavior for handling variable declarations.

- var variables can be used prior to the declaration of the variable.
- let variables cannot be accessed prior to initialization and will result in a `ReferenceError` error.
- const variables will result in a syntax error.

## Functions
- Functions are first class citizens
    - Can be 
        - Treated as any other value
        - Stored in a variable
        - Used as a return value
        - Used as a parameter




## Resources
- [Difference between function scope and block scope in javascript?↗️](https://blog.coolhead.in/difference-between-function-scope-and-block-scope-in-javascript#) - 📄 Article discussin the various scopes in JavaScript including local and global scope.
- [JavaScript Hoising↗️](https://www.w3schools.com/js/js_hoisting.asp) - 📄🕹️ Document discussing variable hoisting in Javascript. Includes some "Try it yourself" sections.
