# Go Types and Variable Declaration


Go is a strongly typed language: it is necessary to specify the type for each declared variable. 
In go the basic types available to the programmer are:

```go
// Boolean [ true or false ] 
bool

// String [ "Example" ]
string

// Integer numbers [ 0, -1, 100, -1000, ... ]
int  int8  int16  int32  int64

// Unsigned integer numbers [ 0, 1, 100, 1000, ... ]
uint uint8 uint16 uint32 uint64 uintptr

// Floating point numbers [ 0.1, 0.01, -0.001, ... ]
float32 float64

// Complex numbers [ 10 + 11i, 5 + 9i, ... ]
complex64 complex128
```

The number following some integer, floating-point, and complex types represents the number of bits the compiler will dedicate to the variable.

In addition to these primary types, there are other derived types that are nothing more than aliases of the primary types. 

```go
// Simple byte value
byte // alias for uint8

// Unicode characters
rune // alias for int32
```

There are two ways to declare a variable of a specific type, you can use the complete construct:

```go
var myvar int = 1
```

or the short form:

```go
myvar := 1
```


