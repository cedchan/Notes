## Getting Started

Open a new script by selecting `Praat > New Praat script`.

Praat scripting essentially allows users to access all the functions and menu options available in the Praat GUI. This means that the general approach should be to think about how to achieve some goal manually, then convert each step into code. For example, to get to a particular position, you could do `Move cursor: [time]`.

Unlike most programming languages, Praat functions take in comma-separated parameters after a colon `:`.

### Debugging Tips

Single-line comments can be made by prepending a line with `#`. 

`pause` can be used as a breakpoint for debugging.

## Data Structures

### Variables

Variables are set with `=`. 

```Praat
a = 10
```

Variables can be numeric, strings, (Praat) objects, etc.
### Strings

Praat separates numeric variables and string variables. String variables must end with `$`. This dollar sign must appear when the variable is used as well. For example,

```Praat
a$ = "text"
```

String functions must also have the `$`. For example, 
```Praat
replace$ ([string], [search], [replace], n)
```

where $n$ is the number of occurrences to replace. To replace all, use $n=0$. 
### Lists

Lists in Praat are [objects](Praat%20Scripting.md#Objects) in the same sense that audio files or TextGrids are. It follows that to use them, we must first select them. 

To find the number of elements in a list, use `getNumberOfString` on the current list. 

To get the $i$-th element, use `Get string: i`.

>[!note]
>Praat is 1-indexed.
## Loops

### For loops

To do a certain number of iterations $i\in[1..a]$, use
```Praat
for i to a
	# ...
endfor
```

For a specific range of numbers $i\in[a..b]$, use
```Praat
for i from a to b
	# ...
endfor
```

## Objects

>[!hint]+
>"Objects" in Praat refer to the objects in the main Praat screen, such as TextGrids, sound files, etc. It is not the same as objects in OOP languages.

Once you select an object in the GUI home panel in Praat, you can run functions from a script. For example, 

```Praat
Rename: "[name]"
```

### Selecting Objects

To select objects from a script, use the `selectObject` function. You can either use the object's number (as seen in the home panel) or name as a string. When using name, you must also include the type in the name (e.g., `TextGrid example` for a TextGrid called "example").

```Praat
selectObject: [number]/"[name]"
```

Objects can be assigned to variables.

```Praat
textGrid = selectObject: 1
sound = selectObject: 2

selectObject: textGrid
```

To add one (or more) objects to the current selection, use `plusObject`. 
### Editor Windows

The aforementioned functions work from the main object selection window. To "open" up the audio editor to access tools like pitch analysis, we must open specific editor windows for objects.

1. Open the main viewing window with `View & Edit`
2. Open the editor for your file with `editor: [number]/[name]`

Now, you can access tools in your specific editor. For example, the following gets the $F_0$ at the current location, then plays the audio:

```Praat
Get pitch
Play
```
## Input/Output

### Print

Praat scripts are primarily debugged through print statements.

`writeInfoLine:` Clears the info window and prints a statement
`appendInfoLine:` Print statement that doesn't clear the line.

These functions can take in an arbitrary number of parameters. For example,

```Praat
a = 10
b = 5
writeInfoLine: a, " ", b, " text"
c = a + b
appendInfoLine: "the sum of a and b is ", c

# Outputs:
# 10 5 text
# the sum of a and b is 15
```

### Files

Files can be opened (i.e., opened to the Praat objects page) can be done with `Read from file`. Note that the function returns the newly added object, so you can store the output as a variable.

Writing to files is similar to print statements, but you must specify the path.

```Praat
path$ = "path/to/some/file"

writeFileLine: path$, "[text to write]", "[...]", "[...]"
appendFileLine: path$, "[text to write]", "[...]", "[...]"
```

### Directories

To read in all the files names in a directory, use

```Praat
Create Strings as file list: "path/to/directory/*.extension"
```

This will create a [list](Praat%20Scripting.md#Data%20Structures#Lists) object.
## TextGrids

### Labels

Get the label of a given interval and tier with 

```Praat
Get label of interval: [tier #], [interval #]
```

The output is a string.

### Times

Start and end times can be retrieved similarly:

```Praat
Get start time of interval: [tier], [interval]
Get end time of interval: [tier], [interval]
```