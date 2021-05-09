<!-- omit in toc -->
# ISOL8 Test Cases and Examples

<!-- omit in toc -->
## Table of Contents
- [1. Declaring Variables](#1-declaring-variables)
- [2. Maths Operations](#2-maths-operations)
- [3. Input/Output Operations](#3-inputoutput-operations)
<br>
<br>

All code blocks have the ``Initial()`` method redacted to due to repitiion and to aid readability, unless stated otherwise.

## 1. Declaring Variables
| Test Case | Code Block | Expected Result | Actual Result | Pass? (Y/N) |
|---|---|---|---|:---:|
|Null byte|``testVar as byte null;``|Compiles successfully|System.FormatException when trying to parse|N|
|Null short|``testVar as short null;``|Compiles successfully|System.FormatException when trying to parse|N|
|Null int|``testVar as int null;``|Compiles successfully|<-|Y|
|Null long|``testVar as long null;``|Compiles successfully|<-|Y|
|Over max byte value|``testVar as byte 256;``|Fails to compile & throws error|<-|Y|
|Over short max value|``testVar as short 65536;``|Fails to compile & throws error|<-|Y|
|Over max int value|``testVar as int 2147483648;``|Fails to compile & throws error|<-|Y|
|Over max long value|``testVar as long 9223372036854775808;``|Fails to compile & throws error|<-|Y|
|Under min byte value|``testVar as byte -256;``|Fails to compile & throws error|<-|Y|
|Under short min value|``testVar as short -65536;``|Fails to compile & throws error|<-|Y|
|Under min int value|``testVar as int -2147483649;``|Fails to compile & throws error|<-|Y|
|Under min long value|``testVar as long -9223372036854775809;``|Fails to compile & throws error|<-|Y|
|Null pointer|``testVar as ptr null;``|Compiles successfully|<-|Y|
|Pointer assignment to variable|``testVar as ptr null;``<br>``testVarTwo as int 3;``<br>``testVar = (ptr)testVarTwo;``|Compiles successfully|<-|Y|
|Pointer assignment to pointer|``testVar as ptr null;``<br>``testVarTwo as ptr null;``<br>``testVar = (ptr)testVarTwo;``|Compiles successfully|<-|Y|
|Empty string|``testVar as string "";``|Compiles successfully|<-|Y|
|String with data|``testVar as string "Hello World!";``|Compiles successfully|<-|Y|
|Boolean with true/false keywords|``testVar as bool true;``<br>``testVar as bool False;``|Compiles successfully|<-|Y|
|Boolean with 0/1 values|``testVar as bool 0;``<br>``testVar as bool 1;``|Compiles successfully|<-|Y|
|Boolean with <0, >1 values<br>(see variable declaration in docs)|``testVar as bool -411;``<br>``testVar as bool 623423;``|Compiles successfully|<-|Y|

<br><br>


## 2. Maths Operations
| Test Case | Code Block | Expected Result | Actual Result | Pass? (Y/N) |
|---|---|---|---|:---:|
|int1 + int2 (addition)|``testVar as int 32;``<br>``testVarTwo as int 5;``<br>``testVar + testVarTwo;``|Correct addition of two variables|<-|Y|
|int1 - int2 (subtraction)|``testVar as int 10;``<br>``testVarTwo as int 20;``<br>``testVar - testVarTwo;``|Correct subtraction of two variables|<-|Y|
|int1 * int2 (multiplication)|``testVar as int 3;``<br>``testVarTwo as int 20;``<br>``testVar * testVarTwo;``|Correct multiplication of two variables|<-|Y|
|int1 / int2 (division)|``testVar as int 3;``<br>``testVarTwo as int 20;``<br>``testVar * testVarTwo;``|Correct division of two variables|Partially correct<sup>5</sup>|Y|
|int1 > int2 (greater than)|``testVar as int 25;``<br>``testVarTwo as int 4;``<br>``comparison as bool false;``<br>``comparison = testVar > testVarTwo;``|Correct comparison of two variables, storing correct value in boolean|<-|Y|
|int1 < int2 (less than)|``testVar as int 1;``<br>``testVarTwo as int 4;``<br>``comparison as bool false;``<br>``comparison = testVar < testVarTwo;``|Correct comparison of two variables, storing correct value in boolean|<-|Y|
|int1 == int2 (equal to)|``testVar as int 4;``<br>``testVarTwo as int 4;``<br>``comparison as bool false;``<br>``comparison = testVar == testVarTwo;``|Correct comparison of two variables, storing correct value in boolean|<-|Y|

*<sup>1</sup>Variables must be of the same type to use maths operators on them*<br>
*<sup>2</sup>Operators currently cannot have immediate operands i.e. ``result / 2`` will not work, they must be variables.*<br>
*<sup>3</sup>This portion requires software assisted testing - there are 44 possible combinations of variables and operators (mathematical & comparison) along with countless of combinations of values so it is impossible to cover every scenario manually.*<br>
*<sup>4</sup>When using the syntax ``variable1 - variable2`` (operator does not matter), the value of the calculation will be stored in ``variable1``.*<br>
*<sup>5</sup>Floats are not yet supported in ISOL8.*

<br>
<br>

## 3. Input/Output Operations
| Test Case | Code Block | Expected Result | Actual Result | Pass? (Y/N) |
|---|---|---|---|:---:|
|Output from byte|``testVar as byte 44;``<br>``out(testVar);``|Prints value correctly|Does not print numerical values.<br>printf flags are probably not set properly|N|
|Output from short|``testVar as short 32240;``<br>``out(testVar);``|Prints value correctly|Partially correct<sup>2</sup>|Y|
|Output from int|``testVar as int -238472931;``<br>``out(testVar)``|Prints value correctly|Partially correct<sup>2</sup>|Y|
|Output from long|``testVar as long 27423338472931;``<br>``out(testVar);``|Prints value correctly|Partially correct<sup>2</sup>|Y|
|Output from pointer-to-value|``testVar as int 34532;``<br>``testVarPTR as ptr null;``<br>``testVarPTR = (ptr)testVar;``<br>``out(testVarPTR);``|Prints value correctly|Outputs garbage, might even be the memory location|N|
|Output from empty string|``testVar as string "";``<br>``out(testVar);``|Prints value correctly|<-|Y|
|Output from string with data|``testVar as string "Hello World!";``<br>``out(testVar);``|Prints value correctly|<-|Y|
|Output from boolean|``testVar as bool 1;``<br>``testVarTwo as bool false;``<br>``out(testVar);``<br>``out(testVarTwo);``|Prints value correctly|<-|Y|
|Input into byte|``testVar as byte 1;``<br>``in(testVar);``|Variable is updated to input value|Not implemented exception|N|
|Input into short|``testVar as short 1;``<br>``in(testVar);``|Variable is updated to input value|Not implemented exception|N|
|Input into int|``testVar as int 1;``<br>``in(testVar);``|Variable is updated to input value|<-|Y|
|Input into long|``testVar as long 1;``<br>``in(testVar);``|Variable is updated to input value|Not implemented exception|N|
|Input into string|``testVar as string "";``<br>``in(testVar);``|Variable is updated to input value|Partially working<sup>3</sup>|N|
|Input into boolean|``testVar as bool true;``<br>``in(testVar);``|Variable is updated to input value|Not implemented exception|N|

*<sup>1</sup>There currently is no range checking implemented - users must be careful when entering values.*<br>
*<sup>2</sup>All numeric variables are treated as signed i.e. whilst ``short`` has a max possible value of 65,535, it can only print between a range of -32,768 to 32,767.*<br>
*<sup>3</sup>Input strings (e.g. ``hello world``) must not contain any spaces, otherwise the program will not work as expected.*
