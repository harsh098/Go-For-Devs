# Getting Started
This tutorial covers basic structure and organisation of a Go Program and how these programs are organised in a production environment

## Section-0 Setting up Go Development Environment
 Follow this awesome tutorial from the Official Go Docs. They pretty much detail everything [here](https://go.dev/doc/tutorial/getting-started#install)

## Section 1 - Your First Program
Let's begin with our Hello World Program. Follow along   
1. Create a folder `hello` and `cd` into it from your terminal.  
```shell
mkdir hello
cd hello
```
2. Initialize dependency tracking using `go mod init`
```bash
go mod init hello
```
3. create a `main.go` file

```go
package main
import "fmt"

func main(){
	fmt.Println("Hello World")
}

```  
4. Run The Program

```
$ go run .
Hello World
```

**You Successfully ran your first Go Program**  
This is your Go code. In this code, you:
1. Declare a `main` package (a package is a way to group functions, and it's made up of all the files in the same directory).
2. Import the popular `fmt` package, which contains functions for formatting text, including printing to the console. This package is one of the `standard library` packages you got when you installed Go.
3. Implement a main function to print a message to the console. A main function executes by default when you run the main package.

## Section 2 - What are Packages?
Every Go program is made up of packages.  
Programs start running in package `main`.  
The above program is using the packages with import paths ``"fmt"``.  

`"fmt"` provides basic formattedIO functions such as `Println`, `Printf`
>When your code imports packages contained in other modules, you manage those dependencies through your code's own module. That module is defined by a `go.mod` file that tracks the modules that provide those packages. That `go.mod` file stays with your code, including in your source code repository.

>To enable dependency tracking for your code by creating a `go.mod` file, run the `go mod init` command, giving it the name of the module your code will be in. The name is the module's module path.

>In actual development, the module path will typically be the repository location where your source code will be kept. For example, the module path might be github.com/mymodule. If you plan to publish your module for others to use, the module path must be a location from which Go tools can download your module.

The `go mod init hello` command created the `go.mod` file that keeps track of imported packages in the code.


Whenever we run our program using `go run .` the go compiler does dependency checking and updates the `go.mod` which is useful  
when we build and ship our binaries in production.

## Section 3 - Using External Packages
_Adapted from:-_ [https://go.dev/doc/tutorial/getting-started#call](https://go.dev/doc/tutorial/getting-started#call)  
When you need your code to do something that might have been implemented by someone else, you can look for a package that has functions you can use in your code.  

1. We are using a package from [pkg.go.dev](pkg.go.dev) called `rsc.io/quote`.
2. To import the package add `import "rsc.io/quote"`
3. Now, add the following lines in your file 
```go
package main

import "fmt"

import "rsc.io/quote"

func main() {
    fmt.Println(quote.Go())
}
```
4. Now sync the dependencies using `go mod tidy`
```
$ go mod tidy
go: finding module for package rsc.io/quote
go: found rsc.io/quote in rsc.io/quote v1.5.2
```
5. You will find a file `go.sum` available in your working directory. `go.sum` contains authentication information needed to verify packages during build. Also look for changes in your `go.mod` file.
6. Now run the program
```
$ go run .
Don't communicate by sharing memory, share memory by communicating.
```  

>[pkg.go.dev](pkg.go.dev) is the official repository for looking for go packages
> 
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
(**Untyped**)  
```go
const CONSTANT_NAME = CONSTANT_VALUE
```
or 
(**Typed**)
```go
const CONSTANT_NAME type= CONSTANT_VALUE
```
2. **Multiple Constants** (Untyped)

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
3. **Multiple Constants** (Typed)

```go
 const(
   CONSTANT_1 type= VALUE_1
   CONSTANT_2 type= VALUE_2
   
 )
```  
or  
```go
const CONST1, CONST2 type= VAL1, VAL2
```   

**Numeric Constants**  
In Go numeric constants automatically assume the datatype they are needed for.
unless specified explicitly.
**Consider This Example**  
>Note : Untyped Constants support Implicit Conversions 

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
