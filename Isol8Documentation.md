<!-- omit in toc -->
# ISOL8 Language Documentation

- [ISOL8 Dependencies](#isol8-dependencies)
- [Running the ISOL8 Compiler](#running-the-isol8-compiler)
- [Examples](#examples)
- [Language Syntax](#language-syntax)
	- [Variable Declaration](#variable-declaration)
	- [Function Declaration](#function-declaration)
	- [External Libraries](#external-libraries)
	- [Maths Operations](#maths-operations)
	- [Comparative Operators](#comparative-operators)
	- [Arrays](#arrays)
	- [Pointers](#pointers)
	- [Input / Output](#input--output)
	- [Deleting Variables](#deleting-variables)
	- [If Statements](#if-statements)
	- [For Loops](#for-loops)
	- [Comments](#comments)

## ISOL8 Dependencies
ISOL8 Compiler requires .NET 5 to be installed on the machine, it can be downloaded from [here](https://dotnet.microsoft.com/download/dotnet/5.0/runtime/).
<br>
<br>

## Running the ISOL8 Compiler
Run ``Isol8-Compiler.exe`` via the command line. It takes two arguments - first argument is the full name of the source text file, and the second argument is the name of the executable to create.

Example:
```
./Isol8-Compiler.exe my-program-source.txt my-program
```
This will run the compiler which will look at ``my-program-source.txt``, where it is expecting ISOL8 syntax, and will generate ``my-program.exe`` in the Output folder if there are no compiler errors.

## Examples
Examples showing ISOL8 syntax can be found [here](https://github.com/Isol8-Language/Isol8-Docs/tree/master/examples); these illustrate what the language is capable of but is it not an extensive list. Feel free to download and compile them to see for yourself.
<br>
<br>

## Language Syntax

### Variable Declaration
```
<VariableName> as <VariableType> <VariableValue>;
```

| Variable Type |ISOL8 Syntax | Min. Value | Max. Value |
|---|---|:---:|:---:|
|8-bit integer|``byte``|-255|255|
|16-bit integer|``short``|-65,535|65,535|
|32-bit integer|``int``|-2<sup>31</sup>|2<sup>31</sup>-1|
|64-bit integer|``long``|-2<sup>63</sup>|2<sup>63</sup>-1|
|Pointers|``ptr``|-|-|
|Strings|``string``|-|-|
|Booleans|``bool``|0|1|
<br>

Booleans can be defined in multiple ways:
```
## true/false are not case sensitive
bool_x as bool TRUE;
bool_y as bool false;

## numeric values instead of true/false
bool_a as bool 1;
bool_b as bool 0;

## range of values - values > 1 are true, values < 1 are false
bool_i as bool 4534;		## true
bool_j as bool -66;			## false
```
Variables can be reassigned a value after declaration, the syntax and use case follow:
```
<Variable> = <Value/Variable>;
```
```
intOne as int 56;
intTwo as int 677;
intThree as int null;

intThree = intOne;
```
___
### Function Declaration
```
<FunctionName>() RET <ReturnType>
{
    ret <ReturnVariable>;
}
```
The program must contain one method/function which is called ``Initial()``, this is the entry point. Failure to include this entry point will result in a fatal compiler error.
___
### External Libraries
Syntax for importing external libraries:
```
depend "<relative/absolute path to library>"
```
These should be placed at the very beginning of the file.
___
### Maths Operations

|Operator|ISOL8 Syntax|
|---|:---:|
|Addition|``+``|
|Addition Assignment|``+=``|
|Subtraction|``-``|
|Multiplication|``*``|
|Division|``/``|
<br>

Syntax of using mathematical operations in ISOL8 (expect for the addition assignment operator):
```
<Variable One> = <Variable Two> <operator> <Variable Three>;
```
This is also acceptable:
```
<Variable One> <operator> <Variable Two>;
```
This will store the result of the calculation in ``<Variable One>``.
<br>
<br>

<!-- omit in toc -->
#### Addition Assignment:
```
<VariableName> += <Value>;
```
This is equivalent to ``<VariableName> = <VariableName> + <Value>;``
```
intVar as int 1;
intVar += 1;		// 'intVar' now equals 2
```
____
### Comparative Operators

|Operator|ISOL8 Syntax|
|---|:---:|
|Less than|``<``|
|Greater than|``>``|
|Less than or equal to|``<=``|
|Greater than or equal to|``>=``|
|Is equal to|``==``|
|Is not equal to|``!=``|

Syntax for using comparative operators in ISOL8:
```
<BooleanVariable> = <Variable One> <operator> <Variable Two>;
```
____

### Arrays
Currently only array declaration is possible.

Syntax:
```
<Variable> as <ArrayType>[<ArrayLength>];
```
Example:
```
b as int[10];
```
___
### Pointers
Syntax:
```
<PointerName> = (ptr)<VariableName>;
```

Example:
```
intOne as int 3;
pointerOne as ptr null;

pointerOne = (ptr)intOne;
out(pointerOne); 	## prints '1'
```

Pointers can also point to other pointers, and therefore be nested.

___
### Input / Output
Stores the value of the input into the provided variable; syntax:
```
in(<variableName>);
```

Prints out the value of the variable; syntax:
```
out(<VariableName>);
```

To use ``in()`` or ``out()``, the required libraries must first be declared (see [external libraries](#external-libraries) for more):

```
depend "ucrt.lib"
depend "msvcrt.lib"
depend "legacy_stdio_definitions.lib"
depend "legacy_stdio_wide_specifiers.lib"
```
These libraries are provided in the release version of the compiler, and the ``template.txt`` provided has them already inserted.

Currently the ``out()`` function will treat integers as signed.<br> 
New lines can be declared using ``\n`` when using ``out()``, i.e. ``out(<variable>\n``) .
___
### Deleting Variables
```
del <VariableName>;
```
___
### If Statements
```
if <value> == <value>
{
	<action>
}
```
___
### For Loops
```
for (<count>)
{
	<action>
}
```

It is possible to break out of the for loop by using the ``break`` keyword.
___
### Comments
Syntax:
```
## this is a comment, it will be ignored by the compiler.
```

Example:
```
## a as int 43;
out(a/n);
```
This will result in a compiler error as ``a`` will not have been declared.
___
