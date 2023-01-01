# Getting Started
This tutorial covers basic structure and organisation of a Go Program and how these programs are organised in a production environment

## Section-0 Setting up Go Development Environment
 Follow this awesome tutorial from the Official Go Docs. They pretty much detail everything [here](https://go.dev/doc/tutorial/getting-started#install)

## Section 1 - Basic Structure
## Section 2 - What are Packages, Modules etc..
## Section 3 - Using External Modules
## Section 4 - Basic Variables and Datatypes - Intro
Go is a statically typed and compiled language.
### Basic Datatypes in Golang  
For more information in concise form visit : [https://golangbyexample.com/all-data-types-in-golang-with-examples/](https://golangbyexample.com/all-data-types-in-golang-with-examples/)  

```go
bool

string

int  int8  int16  int32  int64 //signed integer
uint uint8 uint16 uint32 uint64 //unsigned integers
uintptr //Unsigned pointer address

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128
```
----
### Declaring a variable in Go
 The `var` statement declares a list of variables.A `var` statement can be at package or function level.
 ```go
  var variableName type = value
 ```
 ----
 ### **Declaring Multiple Variables**
 1. With Different Datatypes  
 ```go
   var(
    val1 string = "Jai Shree Ram"
    val2 bool = true
    val3 int8 = 12
   )
 ```
 2. With same datatype
 ```go
   var i ,j uint64 = 1, 20000
 ```
 ----  
 ### **Auto Type Inference**  
 In Go if a datatype is not specified then Go determines the type of variable using the type of value provided.  
 **Consider the following program:-**
 
 ```go

package main
import "fmt"

func main() {
	var x = 12
	var y = "String Value"
	var z = false

	fmt.Printf("Type of %v is %T\n", x, x)
	fmt.Printf("Type of %v is %T\n", y, y)
	fmt.Printf("Type of %v is %T\n", z, z)
}
 ```
**Output**
```
 Type of 12 is int
 Type of String Value is string
 Type of false is bool
```
----
 ### **Auto Initialization of Uninitialized values**  
 In Go we can create variables without initializing them. The Go compiler automatically assigns a `zero value` to these variables.
 `zero values` are values that are assigned to a variable if a user does not explicitly initilizes a `var`.  
 **Consider the following program:-**  
 
  ```go
package main
import "fmt"

func main() {
	var i int
	var f float64
	var b bool
	var s string
	fmt.Printf("%v %v %v %q\n", i, f, b, s)
}

 ```  
 
 **Output**  
 ```
 0 0 false ""
 ```  
 ----  
 
 ### **Shorthand Variable Declaration**  
 Inside a function, the `:=` short assignment statement can be used in place of a var declaration with implicit type.  
 Outside a function, every statement begins with a keyword (`var`, `func`, and so on) and so the `:=` construct is not available.
 
 ```go
package main

import "fmt"

func main() {
	var i, j int = 1, 2
	k := 3
	c, python, javascript := true, false, "no!"

	fmt.Println(i, j, k, c, python, javascript)
}
 ```  
 **Output**  
 ```go
 1 2 3 true false no!
 ```  
 ----  
 ### **Type conversions**  
 The expression `TypeName(v)` converts the value `v` to the type `TypeName`.
 
 ```go
  var x int = 120
  var y = uint64(x)
  i := 42
  f := float64(i)
  u := uint(f)
 ```
>**Note**: Unlike in C, in Go assignment between items of different type requires an explicit conversion.

**Consider the following program**

```go
package main
import "fmt"

func main(){
 var x = 12
 var y float32 = x
 fmt.Println(x,y)
}
```
**Output**:-  
```
./prog.go:7:18: cannot use x (variable of type int) as type float32 in variable declaration
```  
----
### Constants in Go

Constants can be character, string, boolean, or numeric values.
They are declared using `const` keyword.  
**Syntax**:-
1. **Single Constant**
```go
const CONSTANT_NAME = CONSTANT_VALUE
```
2. **Multiple Constants**

```go
 const(
   CONSTANT_1 = VALUE_1
   CONSTANT_2 = VALUE_2
   
 )
```  
or  
```go
const CONST1, CONST2 = VAL1, VAL2
```  
**Numeric Constants**  
In Go numeric constants automatically assume the datatype they are needed for.

**Consider This Example**  
```go
package main

import "fmt"

const (
	BIGINT   = 1 << 100
	SMALLINT = BIGINT >> 99
)

func z(x int) int {
	return x
}

func zu(y float64) float64 {
	return y
}

func main() {
	//fmt.Println("Invoking z :", z(BIGINT)) //Try uncommenting this causes error due to integer overflow
	fmt.Println("Invoking z :", z(SMALLINT))
	fmt.Println("Invoking zu :", zu(BIGINT))
	fmt.Println("Invoking zu :", zu(SMALLINT))
}
```  
**Output**  
```
Invoking z : 2
Invoking zu : 1.2676506002282294e+30
Invoking zu : 2
```
