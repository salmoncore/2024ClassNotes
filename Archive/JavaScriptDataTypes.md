<< [README](README.md)

# Data Types

## Contents
- [Primitives](#primitives)
- [Type Coercion](#type-coercion)
- [Undefined](#undefined)
- [null](#null)
- [Nullish Coalescing Operator](#nullish-coalescing-operator)
- [Resources](#resources)

## Primitives
- string
- number - 64 bit
- bigint - unlimited accuracy
- boolean
- undefined
- symbol
- null

## Type Coercion
- JavaScript isn't picky about types matching when using operators like `+`, `-`, `/`, `%`.
- `+` is string concatenation.
- `/`, `*`, `%` will automatically do type coercion string to number.

- Type coercion is different from type conversion in that it is implicit while type conversion can be either implicit or explicit.

## Undefined
- `undefined` is automtically stored in variables that have been delcared but not assigned a value.

- Distinct from [null](#null) in that `null` is the intentional absence of a value.

## null
- Coalesence operator

## Nullish Coalescing Operator
- Nullish coalescing (`??`) operator allows for the use of a default if the first expression is [null](#null).

## Resources
- [Primitive](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) - MDN Web Docs article on Primitve types.
- [Type coercion↗️](https://developer.mozilla.org/en-US/docs/Glossary/Type_coercion) - 📄 MDN Web Docs on type coercion.
- [null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/null) - 📄🕹️ MDN Web Docs on `null` with interactive "Try it".
- [Nullish coalescing operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing) - 📄🕹️ MDN Web Docs on nullish coalescing operator (??) with interactive "Try it".