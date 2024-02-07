## Variables

JavaScript automatically detects type.

```JavaScript
let x; // Undefined
x = 5; // Gets type number
const v = "Hello"; // Becomes string
```

### Hoisting

>[!definition]
>**Hoisting** is when variable definitions are brought up to the top of the scope.

This means that variables can be accessed before declaration, which can potentially lead to unexpected errors.

Variables have three different types: `let`, `var`, and `const`. `let` variables cannot be accessed before declaration `const` variables must be initialized `var` variables can be accessed before declaration. 

>[!warning]
>In general avoid `var`.

### Undefined and Null Variables

When variables are operated on, they will return `NaN`. For example, `1 + undefined === NaN`.

Meanwhile when `null` values are operated on, they are cast to 0. For example, `1 + null === 1 + 0 === 1`. 

The difference is that `undefined` is not a value, whereas `null` is (or more precisely, is a reference to nothing).
## Objects

Objects can relate keys to values.
```JavaScript
const student = {name: "Bob", major: "CIS"};
```

An equivalent definition would be as follows. Notably, JavaScript allows the creation and editing of fields at runtime.
```JavaScript
const student = new Object();
student.name = "Bob";
student.major = "CIS";
```