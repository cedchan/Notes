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

### Vectors

Vectors are 1-D arrays in R

A vector with the eleemnts `x, y, z, ...` can be created with 
```r
c(x, y, z, ...)
```

A sequence can be created with `seq(start, end, increment)` (similar to `range()` in Python)
```r
> seq(1, 10, 2)
  [1] 1 3 5 7 9
```

Repetitive vectors can be created with `rep()`
```r
> rep(1,10)
  [1] 1 1 1 1 1 1 1 1 1 1
> rep(c(1,2), 10)
  [1] 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2
```

A random normal vector can be generated with `rnorm(n, mean, sd)`

Like in MATLAB, you can access multiple indexes or index ranges in R.

### Dataframes

Dataframes can be seen as 2-D vectors.

For 2-D datasets, the `$` character can be used to view named columns. For example, `data$col1` would return the column labeled `col1` of the dataframe `data`. Similarly, `$` can be used to create new columns.

Assigning a value to a column assigns the value to each element in the column. Simple arithmetic operations between columns are done element-wise.