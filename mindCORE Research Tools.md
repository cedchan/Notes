## R

### Variables

Variables are assigned with `<-`. 

Data types:
- Numeric
	- Integer
	- Complex
	- Floating point
	- Constants like `pi`
	- Typical operators: `+`, `-`, `*`, `/`, `%`
- Character
	- Denoted with double quotes—e.g., `"h"`, `"hi there"`
- Logical (Boolean)
	- `TRUE` or `FALSE`

Type casting with `as.{type}`. E.g., `as.integer("1")` is `1`. 

### Functions

Function arguments are similar to Python. That is, they can be literally entered (`func(arg0={value}, arg1={value)`), otherwise order is assumed.

Define functions with the following syntax:
```r
func_name <- function(arg0, arg1, ...) {
	...
}
```

### Boolean Logic

Equality operators are `==`, `!=`.

If/else statements can be done as ternary operators: `ifelse({condition}, {if TRUE}, {if FALSE})`